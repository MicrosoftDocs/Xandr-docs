---
title: Troubleshoot Deals with Augmented Line Items 
description: In this article, explore detailed steps to troubleshoot and enhance Augmented Line Item (ALI) delivery, bid performance, and impression count.
ms.date: 02/23/2025
---

# Troubleshoot deals with augmented line items 

> [!NOTE]
> This feature is currently in Alpha and may undergo changes without notice. To enable this feature, contact your Microsoft Advertising Account Representative. 

You can access the **Troubleshooting** tab in the [Line item Details](view-line-item-details.md) pane to view a prioritized list of bid performance messages. These messages provide reasons and recommendations to improve the bid performance of an Augmented Line item. The system prioritizes messages by impact, so not all messages appear at once when accessing the **Troubleshooting** tab. 

For additional information about how to view bid performance messages for a specific augmented line item (ALI), see [Troubleshoot Your Augmented Line Item Delivery and Bid Performance](troubleshoot-your-augmented-line-item-delivery-and-bid-performance.md).

## Troubleshoot undelivered deals 
If a **Deal** targeted by a Line Item is not being monetized, follow these steps to diagnose the issue: 

1. You must confirm the **Deal ID, Deal state,** and **flight dates** to determine the expected behaviour. 
    1. If the deal state is **Active** and the current date falls within the flight dates, the deal can serve.  
    1. If the deal state is **Pending** or **Inactive,** or if the flight dates are out of range, the deal will not serve. You can resolve the above issues by making the necessary adjustments: 
        1. In the **Inventory** tab, select **Deals** and select **Accept the Deal** to move the state to **Active.**
        1. In the **Inventory** tab, select **Deals** to verify the Deal’s flight dates are correct and align the flight dates with the intended Line item delivery window. You can coordinate with the seller if necessary. 
1. You can use the **Deal Metrics** screen or the [Buyer Deal Metrics](buyer-deal-metrics.md) report to verify that the Deals have completed four key stages before serving: 
    - **Imps Matched:** In the **Inventory** Tab, select **Deals** to check the number of eligible impressions matched. This is based on available impressions from seller inventory that align with the deal's targeting profile. 
        - If the impressions are low (<1MM), coordinate with the seller to verify the inventory being sent through the Deal and request an increase if needed. 
        - If there is a discrepancy between seller data and Microsoft Invest, contact Customer Support and submit a request through the Customer Support Portal. 
    - **Bid requests:** Bid requests represent number of eligible impressions matched which is then sent to the buyer. The buyer's bidder profile settings control these requests, determining the supply received from Xandr. 
        - This metric is not visible in the **Deals** tab. 
        - You can access the [Buyer Deal Metrics](buyer-deal-metrics.md) report to review the bid requests and ensure the bid request count is similar to the **Imps Matched** value. 
    - **Bids:** Bids represent the number of responses the buyer sends to bid requests. Buyers submit bids only if the bid request aligns with their Line item's targeting criteria.
        - If there is a significant drop from **Imps Matched** to **Bids**, this could indicate a mismatch between the seller’s Deal inventory and the buyer’s targeting settings. 
        - You can verify with the seller that the Deal includes the intended inventory. 
    - **Imps Won:** Imps Won represents the number of bids the buyer successfully won in the auction. Buyers may lose auctions due to several factors, including: 
        - Competing bids based on price or priority. 
        - Ad quality considerations (For example, buyer trust, eligible creative categories, or technical attributes).
        - Bidding below the auction floor.
        - If there is a significant drop from **Bids** to **Imps Won**, you can verify with the seller to check if any of these factors are contributing to bid losses. 
1. If the Deal is still underdelivering, access the **Deals Troubleshooting Report** to identify bid performance blockers and gain deeper insights. Follow these steps to diagnose and resolve potential issues: 
    - You can review the **Line item Troubleshooting** tab to check for Deal-related blockers in the **Creative** or **Valuation** stages. 
    > [!NOTE]
    > Failures in the Line Item stage are expected, as bid requests blocked at this stage do not fall under the targeted Deals.
    - Verify if there are any blockers in the Creative or Valuation stages related to Deals. 
    - Identify the specific Deal IDs associated with errors. For more information, refer to the [Troubleshooting Deal failures](#troubleshooting-deal-failures) section below. 
1. Compare the specific Deal ID from the [Analytics](network-analytics-report.md) report or [Buyer Deal Metrics](buyer-deal-metrics.md) report to verify if any bidding progresses beyond the Creative and Valuation stages of the buying funnel. 
    - You can pull data for the relevant time period and check for impressions on targeted Deals. 
    - Apply the following filters and dimensions: 
        - **Filters:** Add the **Line item ID** 
        - **Dimensions:** Include **Deal**
1. If impressions remain low and the Deals Bid Failure Report does not provide insights, examine the **Auction** stage in the **Troubleshooting** tab.
    - If a significant drop-off occurs, generate a Buyer Bid Error Report to diagnose potential mismatches between the Deal and Creative settings.
    - Apply the following filters and dimensions: 
        - **Filters:** Add the **Creative IDs** and **Deal IDs.**
        - **Dimensions:** Include **Deal, Creative, Error ID, and Error Message.**  
1. If all of the above does not help identify the underlying issue, please contact Customer Support and submit a request through the [Customer Support Portaal](https.help.xandr.com)
 
## Troubleshooting deal failures
The **Deals Troubleshooting Report** provides details on failure reasons that may impact Deal performance. Below are common failure types, explanations of their causes, and recommended steps to investigate or resolve them. 
- **Bid below deal price floors** 
    - **Cause:** The Line item did not submit certain bids because the calculated bid values fall below the price floor(s) of the targeted Deal(s). 
    - **Steps to diagnose and resolve the issue:** You can review the Details section of the affected Deal on the Deals page to confirm the floor and suggested bid amount. Then, check the Line item settings and adjust bid amounts accordingly. 

- **Deal creative sizes** 
    - **Cause:**
        - The Seller has set size restrictions in the Deal settings.  
        - At least one creative does not meet the allowed sizes. 
    - **Steps to diagnose and resolve the issue:** You can confirm with the Seller that the creative sizes comply with the Deal’s requirements.

- **Deal tag creative sizes**
    - **Cause:**    
        - Deals are sourced from Placements or Tags within the seller's inventory. Sellers define the allowed creative sizes for each Placement or Tag, which then determines the inventory available for the Deal.  
        - At least one creative did not meet the allowed size requirements of the assigned Placement or Tag. 
    - **Steps to diagnose and resolve the issue:** You can confirm and verify with the Seller that the creative sizes align with the tag’s allowed sizes. 

- **Deal creative media types** 
    - **Cause:**
        - The Seller has restricted the types of media allowed in the Deal.  
        - At least one creative does not meet the permitted media type. 
    - **Steps to diagnose and resolve the issue:** You can review and confirm with the Seller that the creative media types comply with the Deal’s requirements. 

- **Deal segments on view**
    - **Causes**
        - The Seller controls whether the Deal allows users to be added to segments after a view event is recorded by a pixel.  
        - At least one creative does not meet this requirement.  
    - **Steps to diagnose and resolve the issue:** You can verify with the Seller that the segment targeting methodology aligns with the Deal’s settings. 

- **Deal segments on click 
    - **Causes**
        - The Seller controls whether the Deal allows users to be added to segments after a click event is recorded by a pixel.  
        - At least one creative does not meet this requirement. 
    - **Steps to diagnose and resolve the issue:** You can verify with the Seller that the segment targeting methodology aligns with the Deal’s settings. 
 

## Related topics

- [Bid Performance Messages for Augmented Line Items](bid-performance-messages-for-augmented-line-items.md)
- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
- [Buyer Deal Metrics Report](buyer-deal-metrics.md)
