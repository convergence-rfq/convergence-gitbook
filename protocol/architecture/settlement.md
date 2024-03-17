---
description: For makers and takers
---

# Settlement

## Prepare Settlement

This is the first stage of the settlement process, where both makers and takers deposit the necessary tokens to perform the trade. This ensures that there is sufficient collateral available to cover any potential losses that may occur during the settlement process. The collateral is held in the appropriate collateral accounts until the trade is settled.

## Settle

This is the second stage of the settlement process, where the trade actually occurs. Once the necessary collateral has been deposited, the RFQ is executed and the tokens are exchanged between the maker and taker. If both parties meet their obligations, the trade is settled successfully.

## Counterparty Defaults

If a maker or taker fails to prepare the settlement in time, they are considered to be in default, and a penalty fee may be assessed against them. This penalty fee helps to ensure that trades are executed in a timely and efficient manner, and that parties are held accountable for their actions.

## Revert Settlement

In the event of a default, the trade is reverted, meaning that any tokens that were deposited for the trade are returned to their respective collateral accounts, and the trade is canceled. If both parties default, the penalty fee is paid to the protocol, which helps to maintain the integrity of the Convergence platform.

## Cleanup

This is the final stage of the settlement process, where any remaining collateral is returned to the appropriate collateral accounts, and the trade is considered complete. This ensures that the collateral is available for future trades and helps to maintain the stability of the Convergence protocol.
