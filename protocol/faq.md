# FAQ

**Where is maker and taker collateral stored?**

User collateral is stored in the user collateral account, a token account Program Derived Address (PDA) derived from the user wallet public key and the token mint address. As a PDA the collateral account is non-custodial. Users may add or remove unlocked collateral as needed.

#### **What happens to on-chain data when an account gets closed out. Is it lost?**

Yes and no. Quants need terabytes of data which is why companies like Alpeh and Solana FM index it and make it available in a centralized manner. Data is logged on-chain, improving resiliency, but ultimately centralized indexers take RPC node snapshots to mitigate the need for this.

#### **How much collateral is needed for open size RFQs, that is, orders without size?**

There is a minimum collateral requirement for two-way RFQs. The minimum is decided by governance. Every asset would have its own minimum collateral requirement based on the risk engine.

#### **How can takers determine the maximum size they can accept for a request?**

The risk engine determines the amount of collateral needed for fixed-size orders. The UI has a collateral calculator that shows the maximum amount of size they can accept in the RFQ creation screen.

#### **Are RFQs sometimes used for information and price discovery purposes?**

Yes, RFQs are commonly used for price discovery in financial markets. When a trader or an organization needs to buy or sell a particular security or financial instrument, they can send an RFQ to potential counterparties to request a price quote. The counterparties respond with their quotes, providing information on the current market prices for the requested security or instrument.

Through this process, the RFQ helps to facilitate price discovery by providing market participants with transparent and up-to-date pricing information. The RFQ process allows buyers and sellers to compare prices and terms from multiple potential counterparties, enabling them to make informed decisions about their trades. This can help to ensure that trades are executed at fair market prices, which ultimately benefits both buyers and sellers.

In addition, the multi-leg functionality of the RFQ can be used for more complex price discovery. For example, traders can request quotes for multi-leg trades that involve a combination of spot, options, and futures contracts, allowing them to explore different trading strategies and pricing scenarios. By providing a flexible and efficient way to request and compare price quotes, RFQs are an important tool for price discovery in financial markets.

#### **Is maker and taker collateral taken in the quote asset?**

The risk engine always uses the collateral token mint set in the protocol, that is, USDC, which may or may not be different than the quote asset.

#### **How does the protocol make money?**

The protocol is made profitable through fees and penalties. It has the ability to collect a maker and taker fees separately. Maker fees are currently zero while the taker fee is set to 5 basis points.
