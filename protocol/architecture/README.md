---
description: For makers and takers
---

# Architecture

At its core, the RFQ protocol involves a set of key concepts, including [requests](requests.md), [collateral accounts](collateral-accounts.md), [responses](responses.md), [risk engine](risk-engine.md), and [settlement](settlement.md). When a trader or an organization needs to buy or sell a particular security or financial instrument, they can send an RFQ request to potential counterparties to request a price quote. The counterparties respond with their quotes, which are assessed by a risk engine that helps determine the appropriate level of collateral required for each trade. Once the trade is agreed upon, the response is confirmed and it is settled through a three-step process that involves pre-funding the collateral accounts, executing the trade, and settling the accounts after the trade is completed.

## Diagram

This diagram shows the main components of the Convergence RFQ protocol and their relationships:

1. **Protocol Initialization**: This is the starting point, where the protocol is initialized with fees and other settings.
2. **Instrument & Base Asset Management**: After initialization, instruments and base assets are added and managed. Instruments are the financial assets traded in the protocol, and base assets represent the underlying assets.
3. **Collateral Management**: In this stage, collateral accounts are initialized, funded, and withdrawn as needed for the protocol's operation.
4. **RFQ Creation & Management**: Here, the request for quote is created by adding legs (individual trades) and finalizing the RFQ structure.
5. **RFQ Response Management**: Market makers respond to the RFQ with bid and ask quotes, and users can confirm, modify, or cancel responses.
6. **Settlement Preparation & Execution**: Once the RFQ is confirmed, the protocol prepares and executes the settlement of trades between parties.
7. **Collateral Unlocking & Cleanup**: After the settlement, collateral is unlocked and the protocol performs cleanup operations to release resources.
8. **Default Settlement & Cancellation**: In case of a default or cancellation, this stage handles the process of settling defaults and canceling RFQs.

This diagram provides an overview of the protocol flow and main components, illustrating the sequence of actions for managing RFQs, collateral, and settlements.

<figure><img src="../../.gitbook/assets/mermaid-diagram-2023-03-14-162049 (1).png" alt=""><figcaption></figcaption></figure>
