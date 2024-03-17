---
description: For takers
---

# Requests

## Order Types

### Buy

A buy request is a request to purchase a particular structure at a fixed base or quote price, or for open size. Buy requests are important for traders who want to enter a long position, or bet that the value of the security will increase over time.

### Sell

A sell request is a request to sell a particular structure at a specified price. Sell requests are important for traders who want to exit a long position or enter a short position, which is a bet that the value of the security will decrease over time.

### Two-way

A two-way request is a request that allows the counterparty to respond with either a buy or a sell quote. Two-way requests are important for traders who want to explore different trading strategies or who want to take advantage of market conditions in real-time. By offering both a buy and a sell quote, traders can quickly adjust their trading strategy to take advantage of changing market conditions, such as fluctuations in price or market volatility.

## **Sizes**

### **Fixed**

Fixed size RFQs are where a specific amount of the base or quote asset is specified upon creation. This means that the collateral engine can determine the necessary collateral required for the trade based on the specified amount. Fixed size RFQs are useful when traders know the exact amount of asset they want to buy or sell, as it allows for efficient and accurate collateralization.

### **Open**

On the other hand, open size RFQs do not specify a specific amount of asset to be bought or sold. Instead, traders request quotes from counterparties without specifying the size of the trade. This type of RFQ is useful when traders want to explore the market and obtain quotes for a specific asset without committing to a particular size or trade. Open size RFQs can be useful for traders who want to explore different trading strategies and risk profiles, allowing them to adjust their positions based on market conditions and changing risk profiles. However, open size RFQs can be less capital efficient than fixed size RFQs, as they may require a higher level of collateralization to accommodate the uncertainty in trade size.

{% hint style="info" %}
_A taker may want to create a fixed base buy RFQ for 10 BTC and where the quote asset is USDC. If makers respond and the taker receives quotes for 220,000 USDC and 210,000 USDC, the taker may confirm the first response before the RFQ expires. After the response is confirmed, the taker must prepare to settle by depositing 10 BTC and the maker must deposit 220,000 USDC. Counterparties may then execute the settlement. Note that makers may quote for sizes less than 10 BTC._
{% endhint %}

## Legs

The ability to support multi-leg structures is important for the Convergence RFQ protocol because it allows traders to create more complex and sophisticated trading strategies. This can provide traders with greater flexibility in pursuing their investment goals and managing their risk exposure. By allowing takers to create RFQs for individual spots and more complex structures like covered calls, the Convergence RFQ protocol supports a wide range of trading strategies, allowing traders to take advantage of different market conditions and maximize their returns. Additionally, the ability to support multi-leg structures also enables the protocol to accommodate a wider range of trading use cases, making it more versatile and applicable to different types of traders and trading strategies.

## Windows

### Active

The active window is the period of time during which an RFQ is active, meaning that makers are able to respond to the RFQ with their quotes. The length of the active window is typically determined by the taker when they create the RFQ. The active window is an important period for the taker, as it is the time when they can obtain quotes from potential counterparties and negotiate the terms of the trade.

{% hint style="info" %}
Makers and takers may settle during the active as long as the maker response has been confirmed.
{% endhint %}

### Settlement

The settlement window, conversely, is the period of time that both the maker and the taker have to prepare and settle the trade after the RFQ expires. The length of the settlement window is also determined by the taker when they create the RFQ. During this period, both the maker and the taker prepare the necessary collateral and execute the trade. The settlement window is an important period for both parties, as it provides them with the necessary time to ensure that the trade is settled accurately and securely.
