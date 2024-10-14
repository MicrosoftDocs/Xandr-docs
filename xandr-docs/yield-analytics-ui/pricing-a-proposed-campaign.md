---
title: Price a Proposed Campaign
description: In this article, learn information about the pricing of a proposed campaign.
ms.date: 10/28/2023
ms.custom: yield-analytics-ui 
---

# Price a proposed campaign

Unlike consumption data (which comes directly from ad server logs), working with pricing requires more diligence on the part of the publisher. This is to ensure their revenue data in Yield Analytics is correct, since that data relies on manual input. Many times, publishers input contracted revenue as their rate, or input SOV as the impression goal. Both of these create extreme outliers (in terms of eCPM data) and can misrepresent the truth. Once you feel confident in the quality of your revenue data, you can extract valuable pricing insights with the following path.

**High Level Path**:

1. Use reporting to pull a view on the products you are looking to price, and set the baseline context for comparison. Do you want to look at pricing in the context of a particular timeframe, industry, agency, advertiser, or contract type?
1. Compare your proposal to the historical or future baseline you’ve set. From this point, it’s up to you and your own internal business rules on when you choose to intervene and adjust the pricing.

**Detailed Path**:

1. Typically, two primary dimensions in Yield Analytics are helpful when working with pricing: product and sold as product. ‘Product’ dimensioning (product is an ad server concept) will let you understand yield based on how your inventory is consumed, regardless of how you sold it. In comparison, ‘sold as product’ (which is an order management concept) will let you understand yield based on how your inventory is sold, regardless of how you consume it. Most of the time, publishers simply use ‘sold as product’ dimensioning, since that is easier to map to how a plan is proposed.
1. The view that is most common is to set sold as product as the primary dimension, earned revenue as the primary metric, and then add consumed impressions and eCPM as additional metrics. This will give you a sense of how much is being sold, how much is being earned, and at what price - based on how a customer actually buys. You can then filter down to a particular advertiser, industry, agency, contract type, and various timeframes to set the right context for your analysis. If you provide preferential rates to a particular advertiser for example, it may not be helpful to look at your overall average, but rather that specific advertiser’s historical rates. Similarly, if your demand (and therefore pricing power) is radically different from quarter to quarter, you may want to look at that quarter’s historical rates, rather than your annual average.
1. You can also filter to just the specific sold as products you need, or export the entire view to Excel, where you may find the data easier to work with than the UI.
1. When to intervene in a proposal’s pricing is really up to you the publisher, and your internal business rules.

## Related topic

[Common Journey Maps](common-journey-maps.md)
