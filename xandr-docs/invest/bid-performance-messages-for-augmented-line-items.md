---
title: Bid Performance Messages for Augmented Line Items
description: Learn about the top bid performance messages for augmented line items. 
ms.date: 10/28/2023
---

# Bid performance messages for augmented line items

You can access the **Troubleshooting** tab from the **Line Item Details** pane to obtain a prioritized list of top bid performance messages. These messages contain reasons and recommendations for improving your augmented line item's bid performance. Since these messages are prioritized by impact significance, you won't see every message referenced here at once when accessing the **Troubleshooting** tab.

For additional information about how to view bid performance messages for a specific augmented line item (ALI), see [Troubleshoot Your Augmented Line Item Delivery and Bid Performance](troubleshoot-your-augmented-line-item-delivery-and-bid-performance.md).

## Member targeting

For additional information about how to adjust your member targeting settings, see the following:

- [Member-Level Geography Targeting](member-level-geography-targeting.md)
- [Partner Center Guide](partner-center-guide.md)

| Potential Issue | Reason | Recommended Troubleshooting Steps |  
|:--|:--|:--|
| Member Targeting Settings | Your current member's targeting setup is reducing impression count because it excludes certain sellers in the **Partner Center**, countries/regions, and/or inventories. | - Review and adjust selected country targeting preferences from your Member Targeting settings. <br> - Review and adjust your seller preferences in the **Partner Center**. <br>- If you have inventory lists that apply to all of your ALIs, review and adjust the lists to increase available inventory. |  
| Additional Member Targeting Checks | There's additional negative impact to your impression count as a result of your current member targeting setup. | Check the **Troubleshooting** tab regularly for new bid performance updates. |  


## Augmented line item targeting

For additional information about how to adjust your ALI targeting settings, see the following:

- [Set Up Line Item Budgeting and Scheduling](set-up-line-item-budgeting-and-scheduling.md)
- [Set Up Line Item Inventory and Brand Safety](set-up-line-item-inventory-and-brand-safety.md)
- [Set Up Segment Targeting on a Line Item](set-up-segment-targeting-on-a-line-item.md)
- [Working with Segments](working-with-segments.md)
- [Set Up Line Item Optimization](set-up-line-item-optimization.md)
- [Set Line Item Frequency and Recency Caps](set-line-item-frequency-and-recency-caps.md)
- [Buy-Side Targeting](buy-side-targeting.md)

| Potential Issue | Reason | Recommended Troubleshooting Steps |
|:--|:--|:--|
| Additional ALI Targeting Checks | There's additional negative impact to your impression count as a result of your current ALI targeting setup. | - Review and adjust your ALI targeting setup. <br>- Check the **Troubleshooting** tab regularly for new bid performance updates. |
| Browser Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain browsers. | Review and adjust your ALI targeting setup by including the necessary browsers. |
| Carrier Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain carriers. | - Make sure you're targeting mobile devices. <br>- Review and adjust your ALI targeting setup by including the necessary carriers. |
| City Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain cities. It's normal for city targeting to reduce an ALI's total impression count given its restrictive nature. | Review and adjust your ALI targeting setup by including the necessary cities. |
| Cookieless User Settings | Your ALI's impression count is lower because it isn't targeting cookieless users. If your ALI has conversion pixels, segment targeting, or frequency and recency caps enabled, then cookieless users can't be targeted. | - Review and adjust your frequency caps to include cookieless users. <br> - Review and adjust conversion tracking to include cookieless users using our [Line Item Service (ALI) API](../digital-platform-api/line-item-service---ali.md). <br>- Determine whether to adjust or remove segment targeting if necessary. |
| Country Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain countries/regions. | Confirm that the inventory you're targeting isn't restricting your ALI's geography targeting settings. |
| Daypart Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain hours and/or days. | - Review and adjust your daypart targeting settings to include certain hours and/or days. <br> - Review and adjust your time zone selection (user based versus fixed time zone) within your daypart targeting settings. |
| Deal Targeting Settings | Your ALI targeting setup is currently reducing impression count because it can only bid on impressions for the deals it's targeting. This is expected when targeting deals and normally isn't considered an issue, but you may decide to take action depending on its impact to your impression count. | - Make sure the targeted deals have enough inventory available.<br> - If the available inventory isn't an issue, consider targeting additional deals to increase reach. |
| Demographic Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain users that don't meet the selected demographic or inventory criteria. Sellers typically omit demographic information in their bid requests, which can limit your ALI's available inventory. | - Review and adjust demographic targeting settings. <br> - Work with third-party data providers to get more accurate demographic data. |
| Device Make Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain device makes such as Apple or Samsung. | Review and adjust your ALI targeting setup by including the necessary device makes. |
| Device Model Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain device models such as an iPhone 8 or a Samsung Galaxy X. Targeting specific device models can reduce your available inventory, especially when using additional targeting settings. | Review and adjust your ALI targeting setup by including the necessary device models. |
| Device-Type Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain device types such as desktops, tablets, mobile, and/or CTV. | - Review and adjust your ALI targeting setup by including the necessary device types. <br> - If you're buying deals, work with the seller to align expectations for device types. |
| Domain Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain domains. | Review and adjust your ALI targeting setup by including certain domains using our [Profile Service API](../digital-platform-api/../digital-platform-api/profile-service.md). |
| Frequency Cap Settings | Your ALI’s frequency cap settings are reducing impression count because they prevent users from seeing your creatives more times than your frequency cap allows. | Review and adjust your frequency cap settings. |
| Inactive Profile | Your ALI is using an inactive profile, which is reducing impression count. | Review and adjust your ALI setup by including an active profile using our [Profile Service API](../digital-platform-api/profile-service.md). |
| Inventory Attribute Settings | Your ALI targeting setup is currently reducing impression count because it excludes inventory with certain sensitive attributes. Most inventories have at least one sensitive attribute. Feel free to target as many attributes as needed. | Review and adjust your ALI targeting setup by including inventory with certain sensitive attributes using our [Profile Service API](../digital-platform-api/profile-service.md). |
| Inventory Category Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain inventory categories. Inventory categories aren't reliable sources of contextual information because publishers manually classify them. | Review and adjust your ALI targeting setup by including inventory categories using our [Profile Service API](../digital-platform-api/profile-service.md). |
| Inventory List Settings | Your ALI's inventory list is reducing impression count because it excludes certain inventory sources such as certain members, placement groups, and/or placements. | Review and adjust your inventory list to include the necessary inventory sources such as members, placement groups, and/or placements. |
| Inventory Type Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain inventory types (web or app). | Review and adjust your ALI targeting setup to include the necessary inventory types (web or app). |
| Inventory URL Lists | Your ALI's inventory URL list is reducing impression count because it excludes certain domains. This occurs when certain domains aren't in your allowlist, or when certain domains are in your blocklist. | Review and adjust your inventory URL list by including certain domains. |
| IP Range Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain IP addresses. | Review and adjust your IP address targeting settings using our [IP Range List Service API](../digital-platform-api/ip-range-list-service.md). |
| Key Value Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes inventories that don't contain targeted key value expressions. Publishers define this information in their bid requests. | Review and adjust your ALI targeting setup by including inventories that don't contain targeted key value expressions. |
| Language Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain languages. | Review and adjust your ALI targeting setup by including the necessary languages. |
| Latitude and Longitude Targeting Settings | Your ALI targeting setup is currently reducing impression count because certain users aren't located within your ALI's targeted latitudes and longitudes, or inventories exclude this information. Latitude and longitude targeting settings are primarily used with mobile application inventory. | -  Review and adjust your latitude and longitude targeting.<br>- Target device and supply types for mobile apps. <br> - Consider using geo segments for your location targeting. |
| Media Subtypes | Your ALI's associated creatives are reducing impression count because some inventories don't accept their subtypes. | Review and adjust your targeting strategies by exposing desired media subtypes within your inventory. |
| Metro Code Targeting Settings | Your line item targeting setup is currently reducing impression count because it excludes certain radio and television markets. Since metro code targeting can be restrictive and isn't supported by all countries/regions, it's normal for it to reduce a line item's total impression count. | Review and adjust your metro code targeting settings by including the necessary radio and television markets. |
| Mobile Apps | Your ALI targeting setup is currently reducing impression count because it excludes certain mobile apps. | Review and adjust your ALI targeting setup by including certain mobile apps using our [Profile Service API](../digital-platform-api/profile-service.md). |
| Operating System (OS) Family Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain OS families. Your total impression count can be further reduced when a mismatch exists between device-type and OS-family targeting. | - Review and adjust your ALI targeting setup to include certain OS families. <br> - Review and adjust your device-type targeting settings to align more with its OS-family targeting. |
| Operating System Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain operating systems. Your total impression count can be further reduced when a mismatch exists between device-type and OS targeting. | - Review and adjust your ALI targeting setup to include certain operating systems. <br> - Review and adjust your device-type targeting settings to align more with its OS targeting. |
| Postal Code Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain postal codes. It's normal for postal code targeting to reduce a ALI's total impression count given its restrictive nature. | Review and adjust your ALI targeting setup by including certain postal codes. |
| Query String Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain query strings. Publishers define query string information in their bid requests. | Review and adjust your ALI targeting setup by including the necessary query strings. |
| Region Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain regions. Region targeting can be restrictive, especially when the targeted regions cover smaller areas. | Review and adjust your ALI setup by including certain regions. |
| Segment Settings | Your ALI's audience and/or brand safety segments are reducing impression count because they exclude certain users or inventories. | - If you're targeting brand safety segments, review the targeted inventory to ensure it's compliant. <br> - If you're targeting brand safety segments, make sure they don't interfere with your targeted inventory types (web and/or app). <br> - If you're targeting audience segments, check the selected segments to see if they've ever registered audience loads. <br> - Review and adjust your segment targeting and logic. |
| Unaudited Inventory Targeting Settings | Your ALI inventory targeting setup is reducing impression count because it excludes unaudited inventory. | Review and adjust your ALI targeting setup by including unaudited inventory using our [Profile Service API](../digital-platform-api/profile-service.md). |
| Unaudited URLs | Your ALI targeting setup is currently reducing impression count because it excludes unaudited URLs. | Review and adjust your ALI targeting setup by including unaudited URLs. |
| Video Ad Slot Position Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain ad slot positions. | Review and adjust your ALI targeting setup by including the necessary video ad slot positions. |
| Video Context Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain video contexts. | Review and adjust your ALI targeting setup by including the necessary video contexts. |
| Video Playback Method Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain playback methods. | Review and adjust your ALI targeting setup by including the necessary video playback methods. |
| Video Player Size Targeting Settings | Your ALI targeting setup is currently reducing impression count because it excludes certain video player sizes. | Review and adjust your ALI targeting setup by including the necessary video player sizes. |
| Viewability and Completion Rate Settings | Your ALI targeting setup is currently reducing impression count because it excludes viewability and/or video completion rates that are lower than your selected rate thresholds. It's common for new Microsoft Advertising inventory to not have the necessary historical data for this type of targeting. | - Review and adjust your viewability and/or video completion rates. <br> - When you're buying new inventory, enable viewability targeting on splits to start gathering and delivering viewability data. |

## Creative

For additional information about how to work with creatives, see [Working with Creatives](working-with-creatives.md).

| Potential Issue | Reason | Recommended Troubleshooting Steps |
|:--|:--|:--|
| Creative Attribute Checks | Your ALI's associated creatives are reducing impression count because they don't match sellers' Ad Quality or deals' creative requirements. Creative attribute checks also include impressions that don't match your ALI's split targeting when your creative selection is managed at the split level. | - Review your creatives' brand, category, subtype, and any other attributes. <br> - If you're targeting sellers or deals, check with the sellers regarding their creative requirements. <br> - If custom models or splits are attached, check the targeting on the models or splits. |
| Creative Requirements for Targeted Deals | Your ALI's associated creatives are reducing impression count because they don't match the seller's creative requirements for targeted deals. | - Review and adjust your creatives' brand, category, subtype, and other attributes. <br> - Check with the seller regarding their creative requirements for targeted deals. |
| Creative Sizes | Your ALI's associated creatives are reducing impression count because they don’t meet bid requests' creative size requirements, or they aren't SSL approved. | - Check associated creatives to confirm they've passed SSL audits. <br> - Review and adjust your existing creatives' sizes, or add creatives with varying sizes. |
| Split Targeting | Your ALI isn’t submitting certain bids because impressions don’t match the targeting requirements for any of your splits. If any of your splits contain associated creatives, this message appears in the Creative category instead of the Bid Value category. | Review and adjust your split targeting settings to align them more with your ALI's targeting settings. |
| Additional Creative Checks | There's additional negative impact to your impression count as a result of your current creative setup. | - Review and adjust your creatives. <br> - Check the **Troubleshooting** tab regularly for new bid performance updates. |

## Bid value

For additional information about how to adjust your ALI's revenue type, optimization, and split settings, see the following:

- [Set Up Line Item Budgeting and Scheduling](set-up-line-item-budgeting-and-scheduling.md)
- [Set Up Line Item Optimization](set-up-line-item-optimization.md)
- [Working with Programmable Splits](working-with-programmable-splits.md)


| Potential Issue | Reason | Recommended Troubleshooting Steps |
|:--|:--|:--|
| Additional Bid Value Checks | There's additional negative impact to your bid value as a result of your current buying strategy setup. | Review and adjust your buying strategy setup. |
| Advertiser Cost is Above Expected Value | Your ALI isn't submitting certain bids because its expected value, which is calculated using optimization goals or split and custom model specifications, is above the ALI's CPM revenue value. | - Review and increase your revenue value. <br> - Review and reduce your optimization goals or expected value. |
| Bid is Below Deal Price Floors | Your ALI isn't submitting certain bids because their values are below targeted deals' price floors. | Review and adjust your buying strategy. |
| Bid Modifier Model Targeting | Your ALI isn't submitting certain bids because impressions don't match the targeting requirements for your bid modifier model. | Review the targeting settings for your bid modifier model and make sure they align with your ALI's targeting settings. |
| Bid Price is Above Max AVG CPM | Your ALI isn't submitting certain bids because its optimization settings are forcing minimum bid prices to be higher than the allowed maximum average CPM. | Review and increase your ALI's maximum average CPM. |
| Bid Price is Below Max AVG CPM | Your ALI isn't submitting certain bids because its expected value, which is calculated using optimization goals or split and custom model specifications, is below the ALI's minimum average CPM. | - Review and increase your optimization goal or expected value. <br> - Review and reduce your ALI's minimum average CPM. |
| Cadence Model Targeting | Your ALI isn't submitting certain bids because impressions don't match the targeting requirements for your cadence modifier model. | Review the targeting settings for your cadence modifier model and make sure they align with your ALI's targeting settings. |
| Cold Start Bid is Outside Range | Your ALI isn't submitting certain bids because the estimated prices for inventories aren't within your ALI's average CPM range. Your ALI either has a minimum average CPM that's higher or a maximum average CPM that's lower than the inventories' estimated values. | Review and reduce your minimum average CPM. Review and increase your maximum average CPM. |
| Costs are Higher than Revenue | Your ALI isn't submitting certain bids because its aggregated costs (data costs, fees, and margin) are greater than the expected value, which is calculated based on your optimization goals or advertiser revenue. | - Review and adjust your fees and costs. <br> - If you're using optimization, increase your optimization goal value. <br> - Review and increase your revenue value. |
| CTR Threshold | Your ALI isn't submitting certain bids because inventories' historical CTRs don't meet your ALI's target CTR threshold. | Review and adjust your CTR threshold to align more with the targeted inventories' historical CTRs. |
| Missing Max AVG CPM | Your ALI isn't submitting certain bids because its revenue type requires a maximum average CPM, but it's currently unspecified. | Review and adjust your revenue settings to include a maximum average CPM. |
| Missing Viewability or Completion Rate | Your ALI isn't submitting certain bids because inventories don't have enough historical data to calculate viewability or video completion rates. Your ALI's buying strategy (Viewable CPM or CPCV) is missing a calculated rate. | Switch to a non-viewable strategy to gather historical data on the targeted inventory. |
| Revenue Minus Commissions is Negative | Your ALI isn't submitting certain bids because your ALI's partner fees are too high for its buying strategy. | Check your commissions to see why your revenue is negative after subtracting commissions. |
| Split Pacing | Your ALI's eligible split isn't submitting certain bids because it wants to prevent spending its budget too quickly. | If other splits are underdelivering, review and consider changing your split cap setting to uncapped. |
| Split Targeting | Your ALI isn't submitting certain bids because impressions don't match the targeting requirements for any of your splits. | Review your split targeting settings and try to align them more with your ALI's targeting settings. |

## Auction

| Potential Issue | Reason | Recommended Troubleshooting Steps |
|:--|:--|:--|
| Lost Auctions | Your bid prices may be too low, which could be causing you to lose bids that were submitted for internal or external auctions. There may also be other reasons as to why your bid was rejected. For additional information, see [Understanding Bid Rejections](understanding-bid-rejections.md). | - To increase your chances of winning more bids, review and increase your bid prices.<br> - When targeting deals, review the Submitted Bids grid column on the Deals screen to confirm that your bids are going through. For additional information, see [Deal Targeting (ALI)](deal-targeting-ali.md). <br> - If you're submitting bids for SSP deals, contact your publishers to determine why your bids are losing in external auctions. |

## Related topics

- [Troubleshoot Your Augmented Line Item Delivery and Bid Performance](troubleshoot-your-augmented-line-item-delivery-and-bid-performance.md)
- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
