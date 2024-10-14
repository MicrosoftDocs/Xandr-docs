---
title: Microsoft Invest - Understand Payment Conversion Rates
description: In this article, learn about payment conversion rates, auction outcome prediction, market-making fees, and their calculations.
ms.date: 10/28/2023
---

# Microsoft Invest - Understand payment conversion rates

For eligible impressions, (see [Guaranteed Outcomes Auction Mechanics](guaranteed-outcomes-auction-mechanics.md)), the Exchange calculates an outcome-based bid-to-CPM conversion rate before sending the bid request. The conversion rate is a percentage that represents the predicted likelihood of an outcome on a given impression once the market-making fee has been withheld.

The resulting conversion rate is sent as part of the bid request. If any outcome-based bids are returned, this conversion rate is used to determine the impression-based CPM price paid to the seller.

## Auction outcome prediction

The accuracy of the pre-bid outcome prediction plays a crucial role in the balance of the marketplace; that is, how much is billed to Guaranteed Outcomes buyers versus how much is paid to sellers. Given this critical role, it is important to note that pre-bid outcome predictions are managed as an independent feature of the Exchange and are publicly available.

Pre-bid outcome predictions are freely available in OpenRTB bid requests from Microsoft Advertising's exchange to all bidders and DSPs. Additionally, these predictions are generally available as an Engineered Feature of Microsoft Advertising's exchange. Buyers can use them as building blocks to develop custom algorithms using custom models (APB). Outcome predictions are also used for view-rate and completion-rate threshold targeting and vCPM optimization, both available as features of the Augmented Line Item.

The outcome predictions are modeled across the entire platform as accurately as possible. For more information on the prediction, see [Engineered Features](engineered-features.md) and our tech blog post.

## Market-making fee

Microsoft Advertising provides a service of creating liquidity between buyers and sellers. In doing so, we incur risk, as well as costs from external measurement partners. Thus, we charge a Market-Making Fee for this service. The target Market-Making Fee for Guaranteed Outcomes is 10%. However, the actual Market-Making Fee may vary slightly due to Prediction Variability.

## Market-making fee calculation

Market-Making Fee = Fixed Percentage + Prediction Variability

The Market-Making Fee charged for Guaranteed Outcomes is made up of two components:

- Fixed Percentage: A fixed 10% is taken during the outcome-based bid to impression-based CPM conversion and, implicitly, only charged for when impressions have achieved the buyer's desired outcome.
- Prediction Variability: A positive or negative percentage, depending on the accuracy of the outcome prediction. Because Microsoft Advertising's exchange acts as a financial buffer between buyer and seller, it may have a positive or negative balance over time. A negative balance means that Microsoft Advertising has over-predicted the likelihood of an outcome, and a positive balance means that Microsoft Advertising has under-predicted its likelihood.

In the scenario where there is perfect prediction and all else is equal, the exchange will have a net zero balance, making the Fixed Percentage equal to the Market-Making Fee. There is no promise that the prediction is perfect, and in fact it's almost impossible. As such the Market-Making Fee, or final net balance due to Microsoft Advertising, is still a function of the Prediction Variability.

For transparency, Microsoft Advertising publishes aggregate results for Prediction Variability externally each month. You can find these results at [Monthly Prediction Variability Data](monthly-prediction-variability-data.md).

## Related topics

- [Guaranteed Outcomes](guaranteed-outcomes.md)
- [Guaranteed Outcomes Auction Mechanics](guaranteed-outcomes-auction-mechanics.md)
