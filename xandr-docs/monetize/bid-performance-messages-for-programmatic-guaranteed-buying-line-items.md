---
title: Microsoft Monetize - Bid Performance Messages for Programmatic Guaranteed Buying Line Items
description: Learn about Bid Performance Messages and how to access them. This page also provides a link to get information about how to view bid performance messages for a specific programmatic guaranteed buying line item.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Bid performance messages for programmatic guaranteed buying line items

You can access the **Troubleshooting** tab from the **Line Item Details** pane to obtain a list of bid performance messages. These messages contain reasons and recommendations for improving your programmatic guaranteed buying line item's bid performance.

Please note that you may not see every message referenced here at once when accessing the **Troubleshooting** tab. For additional information about how to view bid performance messages for a specific programmatic guaranteed buying line item, see [Troubleshoot your Programmatic Guaranteed Buying Line Item Bid Performance](troubleshoot-your-programmatic-guaranteed-buying-line-item-bid-performance.md).

| Recommendation | Reason | Recommended Troubleshooting Steps |
|--|--|--|
| Ensure there are eligible creatives appended to this campaign. | Active creatives may not be currently associated with your programmatic guaranteed buying line item. If that isn't the case, then your creatives may be ineligible because they failed Microsoft Advertising's [Auditing Creatives](auditing-creatives.md) process, they're unaudited, or the deal's settings restrict your creatives' types or technical attributes from serving. | Ensure that eligible creatives have been associated with this line item. If eligible creatives have been associated, then make sure that:<br>- they've successfully passed Microsoft Advertising's audit process.<br>- the deal's settings aren't preventing the creatives or technical attributes from serving. |
| Re-activate the line item. | Your programmatic guaranteed buying line item isn’t bidding on all available impressions for the targeted deal. Since the line item’s bid rates have fallen even further after the initial deactivation warning was issued, the line item has been deactivated. | Change the line item's state to active after you've adjusted the line item's bidding behavior. |

## Related topics

- [Troubleshoot your Programmatic Guaranteed Buying Line Item Bid Performance](troubleshoot-your-programmatic-guaranteed-buying-line-item-bid-performance.md)
- [Programmatic Guaranteed Buying Line Items](programmatic-guaranteed-buying-line-items.md)
- [Create a Programmatic Guaranteed Buying Line Item](create-a-programmatic-guaranteed-buying-line-item.md)