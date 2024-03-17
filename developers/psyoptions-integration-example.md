---
description: >-
  In this example guide we will show you how to create your own instrument
  program using the PsyOptions European protocol in our example
---

# PsyOptions Integration Example

### Instrument Program

The spot instrument program is the most basic example of a Convergence RFQ instrument program. The following is an example based on Anchor.

```rust
use crate::errors::PsyoptionsEuropeanError;
use crate::state::AuthoritySideDuplicate;
use anchor_lang::prelude::*;
use anchor_spl::associated_token::get_associated_token_address;
use anchor_spl::token::{
    close_account, transfer, CloseAccount, Mint, Token, TokenAccount, Transfer,
};
use rfq::states::{AuthoritySide, ProtocolState, Response, Rfq};

declare_id!("94sxcX64yqe1s7zY2Hx8tEN8tqisK86dASfizAKkxK7A");

const ESCROW_SEED: &str = "escrow";

#[program]
pub mod psyoptions_european_instrument {
    use super::*;

    pub fn validate_data(
        ctx: Context<ValidateData>,
        data_size: u32,
        mint_address: Pubkey,
        euro_meta: Pubkey,
        option_type: OptionType,
    ) -> Result<()> {
        let euro_meta_acc = &ctx.accounts.euro_meta;
        require!(
            data_size as usize == std::mem::size_of::<Pubkey>() * 2 + 
                std::mem::size_of::<OptionType>(),
            PsyoptionsEuropeanError::InvalidDataSize
        );
        require!(
            euro_meta == euro_meta_acc.key(),
            PsyoptionsEuropeanError::PassedMintDoesNotMatch
        );
        let expected_mint = match option_type {
            OptionType::CALL => euro_meta_acc.call_option_mint,
            OptionType::PUT => euro_meta_acc.put_option_mint,
        };
        require!(
            mint_address == expected_mint,
            PsyoptionsEuropeanError::PassedMintDoesNotMatch
        );
        Ok(())
    }

    pub fn prepare_to_settle(
        ctx: Context<PrepareToSettle>,
        leg_index: u8,
        side: AuthoritySideDuplicate,
    ) -> Result<()> {
        let PrepareToSettle {
            caller,
            caller_tokens,
            rfq,
            response,
            mint,
            escrow,
            token_program,
            ..
        } = &ctx.accounts;
        let leg_data = &rfq.legs[leg_index as usize].instrument_data;
        let expected_mint: Pubkey = \
            AnchorDeserialize::try_from_slice(&leg_data[..32])?;
        require!(
            expected_mint == mint.key(),
            PsyoptionsEuropeanError::PassedMintDoesNotMatch
        );

        let token_amount = response.get_leg_amount_to_transfer(rfq,
                                                               leg_index,
                                                               side.into());

        if token_amount > 0 {
            let transfer_accounts = Transfer {
                from: caller_tokens.to_account_info(),
                to: escrow.to_account_info(),
                authority: caller.to_account_info(),
            };
            let transfer_ctx = CpiContext::new(token_program.to_account_info(),
                                               transfer_accounts);
            transfer(transfer_ctx, token_amount as u64)?;
        } 

        Ok(())
    }

    pub fn settle(ctx: Context<Settle>, leg_index: u8) -> Result<()> {
        let Settle {
            rfq,
            response,
            escrow,
            receiver_tokens,
            token_program,
            ..
        } = &ctx.accounts;

        response
            .get_leg_assets_receiver(rfq, leg_index)
            .validate_is_associated_token_account(
                rfq,
                response,
                escrow.mint,
                receiver_tokens.key(),
            )?;

        transfer_from_an_escrow(
            escrow,
            receiver_tokens,
            response.key(),
            leg_index,
            *ctx.bumps.get("escrow").unwrap(),
            token_program,
        )?;

        Ok(())
    }

    pub fn revert_preparation(
        ctx: Context<RevertPreparation>,
        leg_index: u8,
        side: AuthoritySideDuplicate,
    ) -> Result<()> {
        let RevertPreparation {
            rfq,
            response,
            escrow,
            tokens,
            token_program,
            ..
        } = &ctx.accounts;

        let side: AuthoritySide = side.into();
        side.validate_is_associated_token_account(rfq,
                                                  response, 
                                                  escrow.mint, 
                                                  tokens.key())?;

        if side == response.get_leg_assets_receiver(rfq, leg_index).revert() {
            transfer_from_an_escrow(
                escrow,
                tokens,
                response.key(),
                leg_index,
                *ctx.bumps.get("escrow").unwrap(),
                token_program,
            )?;
        }

        Ok(())
    }

    pub fn clean_up(ctx: Context<CleanUp>, leg_index: u8) -> Result<()> {
        let CleanUp {
            protocol,
            rfq,
            response,
            first_to_prepare,
            escrow,
            backup_receiver,
            token_program,
            ..
        } = &ctx.accounts;

        require!(
            get_associated_token_address(&protocol.authority, &escrow.mint)
                == backup_receiver.key(),
            PsyoptionsEuropeanError::InvalidBackupAddress
        );

        let expected_first_to_prepare = response.leg_preparations_initialized_by
            [leg_index as usize]
            .to_public_key(rfq, response);
        require!(
            first_to_prepare.key() == expected_first_to_prepare,
            PsyoptionsEuropeanError::NotFirstToPrepare
        );

        transfer_from_an_escrow(
            escrow,
            backup_receiver,
            response.key(),
            leg_index,
            *ctx.bumps.get("escrow").unwrap(),
            token_program,
        )?;

        close_escrow_account(
            escrow,
            first_to_prepare,
            response.key(),
            leg_index,
            *ctx.bumps.get("escrow").unwrap(),
            token_program,
        )?;

        Ok(())
    }
}

fn transfer_from_an_escrow<'info>(
    escrow: &Account<'info, TokenAccount>,
    receiver: &Account<'info, TokenAccount>,
    response: Pubkey,
    leg_index: u8,
    bump: u8,
    token_program: &Program<'info, Token>,
) -> Result<()> {
    let amount = escrow.amount;
    let transfer_accounts = Transfer {
        from: escrow.to_account_info(),
        to: receiver.to_account_info(),
        authority: escrow.to_account_info(),
    };
    let response_key = response.key();
    let leg_index_seed = [leg_index];
    let bump_seed = [bump];
    let escrow_seed = &[&[
        ESCROW_SEED.as_bytes(),
        response_key.as_ref(),
        &leg_index_seed,
        &bump_seed,
    ][..]];
    let transfer_ctx = CpiContext::new_with_signer(
        token_program.to_account_info(),
        transfer_accounts,
        escrow_seed,
    );
    transfer(transfer_ctx, amount)?;

    Ok(())
}

fn close_escrow_account<'info>(
    escrow: &Account<'info, TokenAccount>,
    sol_receiver: &UncheckedAccount<'info>,
    response: Pubkey,
    leg_index: u8,
    bump: u8,
    token_program: &Program<'info, Token>,
) -> Result<()> {
    let close_tokens_account = CloseAccount {
        account: escrow.to_account_info(),
        destination: sol_receiver.to_account_info(),
        authority: escrow.to_account_info(),
    };

    let response_key = response.key();
    let leg_index_seed = [leg_index];
    let bump_seed = [bump];
    let escrow_seed = &[&[
        ESCROW_SEED.as_bytes(),
        response_key.as_ref(),
        &leg_index_seed,
        &bump_seed,
    ][..]];

    let close_tokens_account_ctx = CpiContext::new_with_signer(
        token_program.to_account_info(),
        close_tokens_account,
        escrow_seed,
    );

    close_account(close_tokens_account_ctx)
}

#[derive(Accounts)]
pub struct ValidateData<'info> {
    /// protocol provided
    #[account(signer)]
    pub protocol: Account<'info, ProtocolState>,

    /// user provided
    pub euro_meta: Account<'info, EuroMeta>,
}

#[derive(Accounts)]
#[instruction(leg_index: u8, side: AuthoritySide)]
pub struct PrepareToSettle<'info> {
    /// protocol provided
    #[account(signer)]
    pub protocol: Account<'info, ProtocolState>,
    pub rfq: Box<Account<'info, Rfq>>,
    pub response: Account<'info, Response>,

    /// user provided
    #[account(mut)]
    pub caller: Signer<'info>,
    #[account(
        mut,
        constraint = caller_tokens.mint == mint.key()
            @ PsyoptionsEuropeanError::PassedMintDoesNotMatch)]
    pub caller_tokens: Account<'info, TokenAccount>,

    pub mint: Account<'info, Mint>,

    #[account(
        init_if_needed,
        payer = caller, 
        token::mint = mint, 
        token::authority = escrow,
        seeds = [ESCROW_SEED.as_bytes(), response.key().as_ref(), &[leg_index]],
        bump
    )]
    pub escrow: Account<'info, TokenAccount>,

    pub system_program: Program<'info, System>,
    pub token_program: Program<'info, Token>,
    pub rent: Sysvar<'info, Rent>,
}

#[derive(Accounts)]
#[instruction(leg_index: u8)]
pub struct Settle<'info> {
    /// protocol provided
    #[account(signer)]
    pub protocol: Account<'info, ProtocolState>,
    pub rfq: Box<Account<'info, Rfq>>,
    pub response: Account<'info, Response>,

    /// user provided
    #[account(
        mut,
        seeds = [ESCROW_SEED.as_bytes(), response.key().as_ref(), &[leg_index]],
        bump
    )]
    pub escrow: Account<'info, TokenAccount>,
    #[account(mut, constraint = receiver_tokens.mint == escrow.mint
        @ PsyoptionsEuropeanError::PassedMintDoesNotMatch)]
    pub receiver_tokens: Account<'info, TokenAccount>,

    pub token_program: Program<'info, Token>,
}

#[derive(Accounts)]
#[instruction(leg_index: u8)]
pub struct RevertPreparation<'info> {
    /// protocol provided
    #[account(signer)]
    pub protocol: Account<'info, ProtocolState>,
    pub rfq: Box<Account<'info, Rfq>>,
    pub response: Account<'info, Response>,

    /// user provided
    #[account(
        mut,
        seeds = [ESCROW_SEED.as_bytes(), response.key().as_ref(), &[leg_index]],
        bump
    )]
    pub escrow: Account<'info, TokenAccount>,
    #[account(mut, constraint = tokens.mint == escrow.mint
        @ PsyoptionsEuropeanError::PassedMintDoesNotMatch)]
    pub tokens: Account<'info, TokenAccount>,

    pub token_program: Program<'info, Token>,
}

// Duplicate required because anchor doesn't generate IDL for imported structs
#[derive(AnchorSerialize, AnchorDeserialize, Copy, Clone, PartialEq, Eq)]
pub enum AuthoritySideDuplicate {
    Taker,
    Maker,
}

impl From<AuthoritySideDuplicate> for AuthoritySide {
    fn from(value: AuthoritySideDuplicate) -> Self {
        match value {
            AuthoritySideDuplicate::Taker => AuthoritySide::Taker,
            AuthoritySideDuplicate::Maker => AuthoritySide::Maker,
        }
    }
}

#[derive(Debug, AnchorSerialize, AnchorDeserialize, PartialEq)]
#[repr(u8)]
pub enum OptionType {
    CALL = 0,
    PUT = 1,
}

#[derive(AnchorDeserialize, AnchorSerialize, Clone)]
pub struct EuroMeta {
    pub underlying_mint: Pubkey,
    pub underlying_decimals: u8,
    pub underlying_amount_per_contract: u64,
    pub stable_mint: Pubkey,
    pub stable_decimals: u8,
    pub stable_pool: Pubkey,
    pub oracle: Pubkey,
    pub strike_price: u64,
    pub price_decimals: u8,
    pub call_option_mint: Pubkey,
    pub call_writer_mint: Pubkey,
    pub put_option_mint: Pubkey,
    pub put_writer_mint: Pubkey,
    pub underlying_pool: Pubkey,
    pub expiration: i64,
    pub bump_seed: u8,
    pub expiration_data: Pubkey,
    pub oracle_provider_id: u8,
}

impl AccountSerialize for EuroMeta {
    fn try_serialize<W: std::io::Write>(&self, writer: &mut W) -> Result<()> {
        if writer
            .write_all(&[143, 142, 75, 68, 96, 251, 84, 36])
            .is_err()
        {
            return Err(error::ErrorCode::AccountDidNotSerialize.into());
        }
        if AnchorSerialize::serialize(self, writer).is_err() {
            return Err(error::ErrorCode::AccountDidNotSerialize.into());
        }
        Ok(())
    }
}

impl AccountDeserialize for EuroMeta {
    fn try_deserialize(buf: &mut &[u8]) -> Result<Self> {
        if buf.len() < [143, 142, 75, 68, 96, 251, 84, 36].len() {
            return Err(error::ErrorCode::AccountDiscriminatorNotFound.into());
        }
        let given_disc = &buf[..8];
        if &[143, 142, 75, 68, 96, 251, 84, 36] != given_disc {
            return Err(error::ErrorCode::AccountDiscriminatorMismatch.into());
        }
        Self::try_deserialize_unchecked(buf)
    }
    
    fn try_deserialize_unchecked(buf: &mut &[u8]) -> Result<Self> {
        let mut data: &[u8] = &buf[8..];
        AnchorDeserialize::deserialize(&mut data)
            .map_err(|_| error::ErrorCode::AccountDidNotDeserialize.into())
    }
}

impl Owner for EuroMeta {
    fn owner() -> Pubkey {
        ID
    }
}

#[error_code]
pub enum PsyoptionsEuropeanError {
    #[msg("Invalid data size")]
    InvalidDataSize,
    #[msg("Passed mint account does not match")]
    PassedMintDoesNotMatch,
    #[msg("Passed euro meta account does not match")]
    PassedEuroMetaDoesNotMatch,
    #[msg("Passed account is not an associated token account of a receiver")]
    InvalidReceiver,
    #[msg("Passed backup address should be an associated account of protocol owner")]
    InvalidBackupAddress,
    #[msg("Passed address is not of a party first to prepare for settlement")]
    NotFirstToPrepare,
}

#[derive(Accounts)]
#[instruction(leg_index: u8)]
pub struct CleanUp<'info> {
    /// protocol provided
    #[account(signer)]
    pub protocol: Account<'info, ProtocolState>,
    pub rfq: Box<Account<'info, Rfq>>,
    pub response: Account<'info, Response>,

    /// user provided
    /// CHECK: is an authority first to prepare for settlement
    #[account(mut)]
    pub first_to_prepare: UncheckedAccount<'info>,
    #[account(
        mut,
        seeds = [ESCROW_SEED.as_bytes(), response.key().as_ref(), &[leg_index]], 
        bump
    )]
    pub escrow: Account<'info, TokenAccount>,
    #[account(mut, constraint = backup_receiver.mint == escrow.mint
        @ PsyoptionsEuropeanError::PassedMintDoesNotMatch)]
    pub backup_receiver: Account<'info, TokenAccount>,

    pub token_program: Program<'info, Token>,
}
```

### Add Instrument to Protocol Whitelist

The RFQ protocol maintains a list of available instruments using programs ids. Additional instrument integrations must have the program id added to the protocol list through the DAO.
