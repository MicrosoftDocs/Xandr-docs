---
title: Microsoft Invest - In-Market Audiences
description: Learn about Microsoft Invest's In-Market audiences, which are curated groups of users who are actively thinking about buying in a particular category.
ms.date: 10/28/2023
---

# Microsoft Invest - In-Market audiences

Microsoft In-market Audiences are curated lists of users determined to be in market and ready to buy within a particular category. These segments are based on Microsoft’s unique intent signals, including search on Bing and user activity on Microsoft solutions. The power of search behavior indicates that the audiences have a high probability of conversion.

In-market Audiences are global, and available in more than 90 markets. Take a look at this [up-to-date list](https://download.microsoft.com/download/4/0/0/40099106-6f9f-4b38-8aac-0dc7567404db/In-Market-Audiences-segment-list-Invest.xlsx) for all the available in-market audience segments.

## Set up Microsoft segment targeting on a line item

1. Click on the **Audience & Location Targeting** subsection option on the left pane within the **Create New Line Item** screen or **Edit Line Item** screen.
1. An **Audience and Location Segments** panel is displayed on the right. Now, click on **Microsoft** from the targeting model.
1. Select a segment on the left to start building your audience.
1. Click **Save**.

## Special considerations for Microsoft In-Market audiences

Due to the proprietary nature of this data, there will be a set of data protections applied to line items when targeting Microsoft In-Market Audiences.

| Area of Impact | Description of Impact |
|:---|:---|
| Splits | Microsoft audiences cannot currently be targeted within splits or custom models. |
| Measurement | Integral Ad Science (IAS) viewability/verification measurement seamlessly integrates with banner and video line items targeting Microsoft In-Market Audiences. To utilize this feature, apply your IAS JavaScript pixels to the hosted banner and video creatives you wish to run. Advertiser and member-level pixels are also compatible. If your IAS pixels are already configured, no further action is required! <br><br> **Note**: Support for IAS viewability/verification for video and native creatives will be available soon. <br><br> No other measurement integrations are currently supported when using Microsoft Audiences. |
| Creative | <ul><li>Creatives must be hosted, non-HTML5. <li>Third-party pixels are restricted as follows:<ul><li>Image URL and Raw URL pixel types are supported and fired server-side. <br>**Note**: Server-side firing may result in reporting inconsistencies, as the calls come from a server rather than a user's browser/device.</li><li>IAS JavaScript pixels are now supported on banner and video creatives.</li><li>Other HTML URL, JavaScript URL and Raw JavaScript pixel types will be blocked at auction time.</li><li>Certain creative macros will be blocked at auction time (see list of LLD restricted fields below).</ul><li>Segment pixels will be blocked at auction time.</li></ul> |
| Reporting | Log level data feeds containing auction data will have the following set of fields obfuscated or removed completely: <ul><li> Time stamp</li> <li>User ID 64</li> <li> IP Address</li> <li> Operating System </li><li>Browser</li><li>Latitude</li><li>Longitude</li><li>Device ID</li><li>Extended IDs</li></ul><br>The **Advertiser Attributed Conversions** report will have the following set of fields obfuscated or removed for impression events associated with line items targeting Microsoft Audiences:<ul><li>Time stamp</li><li>Auction ID</li><ul> |
