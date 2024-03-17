---
description: Automating the squawk box
---

# Overview

## Vision

Our vision at Convergence RFQ is to create and support the best fully-decentralized, on-chain RFQ protocol for the next generation of digital asset makers and takers. Convergence will realize this vision for our financial primitive by focusing on the following.

**Capital efficiency**

* Under-collateralized thanks to a state-of-the-art risk engine
* Zero slippage and legging risk
* Tokenomics that correctly incentivize makers and takers

**Transparency**

* Fully on-chain protocol
* Open Source Software (OSS) with publicly available audits
* Decentralized governance

**Composability**

* Modular architecture based on atomic operations that leverage a discrete order book
* Standardized interface providing a common language across chains
* Interoperability through connecting the best makers and takers in a on-chain ecosystem providing access to endless assets and instrument types

## **Motivation**

The protocol design specification is optimized for write-first, highly parallelized and distributed decentralized systems, namely the Solana blockchain. Important strategic considerations incorporated into the exchange architecture focus on mitigating exchange and counter-party risk in a non-custodial manner, improving capital efficiency, and creating a proper incentive structure via tokenomics that utilizes fees and penalties. We address each of these considerations a few different ways. First and foremost, the exchange is de-risked using under-collateralized RFQ and escrow. That is, we require escrow in order to make fees and penalties in the event of a default, but avoid custody in trade settlement by allowing both takers and makers to perform the settlement process on-chain. Second, we increase capital efficiency by under-collateralizing each RFQ and response using an adaptable risk engine. Finally, and perhaps most importantly, tokenomics align incentives in a way that make it attractive for investors, builders and traders to participate efficiently and effectively in the ecosystem.

## Considerations

### **Non-custodial**

Custody of funds presents a large risk factor for exchange counterparties. Additionally, locking funds for any period of time, in our example — from RFQ initialization to settlement — presents additional capital inefficiency. Settlement takes place in three steps: trade preparation, trade execution, and an optional trade cleanup.

### **Integration Bottlenecks**

Integration bottlenecks are a core problem both makers and takers face. The protocol aims to solve this and it has led to some interesting design decision-making when looking at the tradeoffs between messaging and execution layer-based systems. The protocol is designed in a way that takes advantage of composability. The message bus approach means trust is not required between counterparties.

### Collateral

How do makers and takers collateralize their RFQs? The protocol does not require makers and takers to put up collateral for a full position yet there needs to be enough incentives for the maker or taker to not default. The risk engine is responsible for determining the amount and type of collateral needed to initialize and respond to an RFQ.

### **Iceberg Orders**

Iceberg orders occur when a taker wants to confirm multiple responses to an RFQ. Collateral is deposited for each RFQ leg. When confirming multiple RFQ responses, the taker must post additional collateral for each confirmable response. This additional collateral may be posted upon RFQ initialization as well as after.

### **Cancellations**

RFQs and responses may effectively be canceled in two ways. First, if a taker does not want to make a trade they can avoid confirming any maker responses and wait for the RFQ to expire. This still involves posting collateral. The taker may also simple cancel the RFQ. However, if a maker is unwilling to make a trade they should not respond to an RFQ — if their response is confirmed by the taker and they chose not to make the trade they will be penalized. They can still cancel a response if it has not yet been confirmed. Ultimately, if a taker and maker cannot make a trade or decide they do not want to _after_ responding and confirming, they can simply choose to not post the remaining collateral to execute the trade and lose their initially posted collateral.

### **Penalties and Fees**

The protocol makes money through penalties and maker and taker fees. Basis points are set on a protocol level.
