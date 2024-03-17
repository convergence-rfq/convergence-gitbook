---
description: For makers
---

# Responses

## Respond to RFQ&#x20;

A response is created by a market maker in response to an RFQ request from a taker. The response contains the market maker's quote for the requested asset or instrument, including the price and any other relevant terms. The response is transmitted to the taker, who can review and accept the quote if they choose to do so.

## Confirm Response

When a taker receives a response from a market maker, they can review the quote and confirm the trade if they agree with the terms. Confirming the trade means that the taker accepts the market maker's quote and is willing to proceed with the trade. Once the taker confirms the trade, the settlement process begins, and the required collateral is moved into the appropriate collateral accounts.

## Cancel Response

RFQ requests and responses can be canceled if there are no live responses. Responses can be canceled only by the maker and it cannot be canceled between the confirmation and settlement steps. If a taker decides not to accept a market maker's quote, they can cancel the request, and the quote will no longer be valid. A market maker cannot cancel their response if they are unable or unwilling to honor their quote. Cancelling a request or response ensures that no trades are executed without the full consent of both parties.

