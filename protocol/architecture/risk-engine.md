---
description: For makers and takers
---

# Risk Engine

The risk engine is the heart of the RFQ protocol. It is a crucial component because it enables requests and responses to be under-collateralized. This means that trades can be executed without requiring full collateralization, making the system more capital efficient. The risk engine helps to assess the risk associated with each trade, taking into account factors such as market volatility and credit risk. By doing so, it allows the exchange to determine the appropriate level of collateral required for each trade, based on the specific risk profile of that trade.

In addition, the risk engine also helps to ensure that the exchange is able to maintain its financial stability and manage its overall risk exposure. By carefully monitoring and managing risk, the exchange can reduce the likelihood of financial losses or instability, while also providing a secure and reliable platform for traders to execute their trades.

## Collateral Calculation

A sophisticated algorithm is used to assess the potential risk of the trade based on various factors, including the market conditions, the volatility of the asset, and the position of the maker and taker. Based on this assessment, the risk engine determines the appropriate amount of collateral that must be held in the collateral accounts to cover any potential losses that may occur during the settlement process. By ensuring that trades are fully collateralized, the risk engine helps to mitigate risk and ensure the stability and security of the Convergence platform.

The risk calculator is used on an RFQ containing various types of instruments such as spot, options, term futures, and perpetual futures. It takes the portfolio, configuration weights, base assets, current prices, scenarios, and current timestamp as input.

Here is an overview of how the risk is calculated:

1. **Base assets statistics:** For each base asset in an RFQ, the biggest loss, profit and the absolute value of the legs is calculated.
2. **RFQ statistics:** This computes the overall RFQ statistics by summing up the biggest losses and profits for each base asset. A safety price shift factor is then applied and an overall risk factor to the total losses and profits.
3. **RFQ risk:** RFQ risk is calculated by taking into account the portfolio inversion and leg multiplier. The result is the total risk for the given case.
4. **Scenario risk:** PnL (profit and loss) for each leg under various scenarios is calculated. It considers the base asset price change, volatility change, and the risk category.
5. **Asset value:** The value of an asset in the RFQ is calculated based on the current price, volatility, interest rate, and current timestamp.
6. **Asset unit value:** Unit value of an asset in the portfolio based on the instrument type (spot, option, term future, or perpetual future) and the associated parameters is calculated.

Overall, the risk calculation process involves analyzing the portfolio under different scenarios, taking into account various market factors such as price, volatility, and interest rates. The risk calculator helps determine the potential losses and profits that could occur under these scenarios, allowing for better decision-making and risk management in the RFQ.
