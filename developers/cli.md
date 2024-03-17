---
description: Interacting with Convergence RFQ via the command line
---

# CLI

The command line utility for Convergence RFQ is a powerful tool designed for traders and developers who want to interact with the Convergence RFQ protocol from a command line interface. This utility provides users with a wide range of functionality, including the ability to create RFQs, respond to RFQs, and manage collateral accounts. With its intuitive interface and powerful features, the command line utility is a versatile tool that can be used to execute trades and manage trading strategies on the Convergence RFQ protocol with ease. Whether you are a seasoned trader or a developer looking to build on the Convergence RFQ platform, this utility is an essential resource for exploring the full potential of the protocol.

## Installation

```
npm install -g @convergence-rfq/cli
```

## Usage

```
Usage: convergence [options] [command]

Convergence RFQ CLI

Options:
  -V, --version                                   output the version number
  -h, --help                                      display help for command

Commands:
  airdrop:sol [options]                           Airdrops SOL to the current user
  airdrop:devnet-tokens [options]                 Airdrops Devnet tokens
  token:create-mint [options]                     Creates a token mint
  token:create-wallet [options]                   Creates a token wallet
  token:mint-to [options]                         Mints tokens to wallet
  protocol:initialize [options]                   Initializes protocol
  protocol:get-config [options]                   Gets protocol config
  protocol:add-instrument [options]               Adds protocol instrument
  protocol:add-base-asset [options]               Adds protocol base asset
  protocol:get-base-assets [options]              Gets protocol base assets
  protocol:register-mint [options]                Registers protocol mint
  protocol:get-registered-mints [options]         Gets protocol registered mints
  risk-engine:initialize [options]                Initializes risk engine
  risk-engine:get-config [options]                Gets risk engine config
  risk-engine:update [options]                    Updates risk engine
  risk-engine:set-instrument-type [options]       Sets risk engine instrument type
  risk-engine:set-risk-categories-info [options]  Sets risk engine risk categories info
  collateral:initialize-account [options]         Initializes collateral account
  collateral:fund-account [options]               Funds collateral account
  rfq:create [options]                            Create RFQ
  rfq:get-all [options]                           Get all RFQs
  help [command]                                  display help for command
```
