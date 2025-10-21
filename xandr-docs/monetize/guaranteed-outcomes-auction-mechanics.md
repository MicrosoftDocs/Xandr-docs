---
title: Microsoft Monetize - Guaranteed Outcomes Auction Mechanics
description: In this article, find information about how an auction works when a buyer submits a bid using Guaranteed Outcomes.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Guaranteed outcomes auction mechanics

This topic describes how an auction works when a buyer submits an outcome-based bid using Guaranteed Outcomes. Buyers submit vCPM bids to buy Guaranteed Views, and CPCV bids to buy Guaranteed Completes.

## Ad call

When an ad call is received, the Exchange first predicts the likelihood that the impression will yield the desired outcome. If a prediction cannot be determined, the impression is ineligible for outcome-based bids. There may be other reasons outcome-based bids aren't supported. For example, monitoring may indicate that the prediction for the given placement is inaccurate, which may lead the placement to be marked ineligible. In addition, outcome-based bids are not accepted when clearing directly with the seller. For more information on pre-bid outcome predictions, see Outcome Prediction.

If an outcome prediction is available, and all other eligibility checks pass, then the Exchange will calculate an outcome-based bid-to-CPM conversion rate. This rate is calculated by multiplying the outcome prediction by a market-making fee. For more information on the conversion rate, see the sections on Understanding Payment Conversion Rates and the Market Making Fee.

## Bid request

On each bid request, the Exchange indicates if it will accept outcome-based bids (vCPM and/or CPCV). If outcome-based bids are acceptable, the Exchange also provides the bidder which outcomes the exchange will accept along with the applicable conversion rate for each.

## Bid response

On the bid response, if the bidder has chosen to submit an outcome-based bid, the bid includes the outcome and the bid price. The bid price is then treated as an outcome-based price.

It is possible for the outcome-based bid to be rejected. In addition to standard rejection reasons (such as failing seller ad quality rules), monitoring may indicate that the prediction for the given creative is inaccurate, resulting in the creative being marked ineligible, or the buyer may have a direct clearing relationship with the seller, which is not supported.

If the bid passes these checks, then, for the purposes of running the auction, the Exchange converts the outcome-based bid to CPM using the provided conversion rate.

## Auction

After all bids are received, and any outcome-based bids are converted to CPM, the auction is executed according to standard RTB mechanics, including, where applicable, second-price logic, private marketplaces, publisher floors, etc.

If a CPM bid representing a buyer's Guaranteed Outcomes bid is the winner in the auction, the winning price will be adjusted post-auction in accordance with our auction mechanics (for example, in a second price auction, it would be price-reduced to the second highest bid + $.01), and the seller will receive this amount as revenue (minus standard auction fees).

The price-reduced CPM bid is then converted back to an outcome-based price using the conversion rate. The buyer will be notified that it won the auction at the price-reduced outcome-based price, but the buyer will not be charged at this point.

## Post-auction

The buyer's creative is served to the page. If the Exchange determines that the creative achieved the buyer's desired outcome, an event is sent to the Exchange indicating that the buyer should be billed for the impression at the price-reduced outcome-based price. The Exchange will log the transaction and send notification to the buyer.

If the Exchange determines that the ad did not achieve the buyer's desired outcome, or if it is unable to make the measurement, then the buyer is not billed for the impression.

## Related topics

- [Guaranteed Outcomes](guaranteed-outcomes.md)
- [How Guaranteed Outcomes Work](how-guaranteed-outcomes-work.md)
