---
title: Microsoft Monetize - Data Marketplace FAQ(s)
description: In this article, find answers to frequently asked questions regarding the Data Marketplace.
ms.date: 10/28/2023
---

# Microsoft Monetize - Data Marketplace FAQ(s)

**What happens when I activate a data provider?**

Microsoft Advertising will automatically set up standard pricing and clearing for that data provider and shares all public segments to your seat. Segments may take up to 2 hours to populate the UI but in some instances, you will be able to immediately start targeting that data provider's segments.

**Does the data marketplace support custom segments?**

Yes, we provide the same reporting and clearing services for custom segments as long as there is a CPM associated with the segment and if the data provider has opted to offer them through our data marketplace. Once the data provider has been activated in the UI, the data provider will be able to expose your custom segments to your Microsoft account. You will know everything is properly set up when the segment is available for targeting and there is a price associated with the segment.

**What if I have better rates than what Microsoft Advertising provides?**

Please reach out to the relevant Data Provider to make sure these better rates are reflected in our system.

**What if I have a monthly flat-rate deal with a data provider?**

Microsoft Advertising will not be able to clear that cost for the buyer. The data provider will have to continue invoicing your organization directly.

**Do you support custom rate cards in non-USD currencies?**

Yes, we support all currencies listed in our [Currency Support](currency-support.md) documentation.

**How will this look on my invoice?**

In most cases, the cost of data will be an extra line item in your invoice. If you receive invoices in a non-USD currency, the cost of data will be invoiced in the same currency as your cost of media. The invoice will not be broken out by data provider. However, we provide a data usage report for that level of granularity.

**Do I have to change anything about my line item to make this work?**

If your in-flight line item is targeting a segment supported by the data marketplace, then there is nothing on the line item that you have to change. Once the data provider is activated for clearing, Microsoft Advertising will immediately start clearing the cost of data on your behalf.

**The data provider I need isn't supported by the Data Marketplace. What should I do?**

Please reach out to your account representative.

**I am having issues with the data marketplace features. How can I get support?**

Submit a support ticket via our [Customer Support Portal](https://help.xandr.com/) and our team will provide assistance shortly.

**What are the metrics "Imps" and "Users" in the data marketplace exactly? How is the reach estimation made?**

Users and Impressions are determined over time as segments participate in auctions, and may not be available initially for newer segments created. The reach metrics are estimates based on a 24 hour sample of auction data:

- **"Users"**: Daily estimated global user reach
- **"Imps"**: Daily estimated global impression reach

**Are "Imps" and "Users" metrics supported for contextual targeting segments?**

Yes, reach metrics are currently supported for both types of segments. A limited number of real-time data providers are supported today, and will continue to expand in the future:

- Peer39
- comScore
- DoubleVerify
- Integral Ad Science
- Adloox
- Foursquare (FKA Factual)
- Qwarry
- Digiseg

**How are ad type, device type, and geography filters calculated?**

Segments that are seen in auctions are logged and their environments are tracked to use as a filter. This may not be available initially for newer segments created.

**Why don’t users or impressions change for a segment when applying a filter?**

Filtering helps identify environment-compatible segments and does not change the reach metrics. We recommend using campaign planner to preview the reach of one or more audiences in specific environments.

**What is the difference between the "My Segments", "Shared Segments", "Microsoft" and the "Data Marketplace" tab?**

| Tab(s) | Description |
|---|---|
| **My Segments** | These are segments which have been created within the own member seat |
| **Shared Segments** | These are segments privately shared with the member by another member, such as a Data Provider or data on-boarder/DMP. These segments are not part of the Data Marketplace, and are managed directly between the buyer and member who owns the segment(s) shared. |
| **Microsoft** | These are Microsoft In-Market Audiences identified as being actively in the market and ready to make a purchase within a specific category. These segments are formulated using Microsoft's distinctive intent signals, including search on Bing and user activity on Microsoft solutions. For more information please refer to the following page: [Microsoft In-Market Audiences](../invest/microsoft-in-market-audiences.md) |
| **Data Marketplace** | These are all segments in our Data Marketplace where Data Providers make their segments available for purchase, including custom segments. |

**How should brand safety segments be targeted (positively/negatively)?**

It depends on the brand safety segment provider whether you should be targeting their segments positively or negatively and what Boolean Logic is supported. Please refer to the following overview:

| Brand Safety Provider | Segment Type | Supported Boolean Logic |
|---|---|---|
| **Double Verify** | Authentic Brand Safety = **Include** ![Check mark.](media/check.png) | AND |
| **Double Verify** | Standard Brand Safety = **Include** ![Check mark.](media/check.png) | AND |
| **IAS** | **Include** ![Check mark.](media/check.png) | AND |
| **GumGum** | **Exclude** ![Exclude mark.](media/exclude.png) | OR |
| **ComScore** | "Brand Suitability” and “Fact Check” = **Exclude** ![Exclude mark.](media/exclude.png) | AND |
| **ComScore** | Brand Protection Safe from” and “Content Ratings” = **Include** ![Check mark.](media/check.png) | AND |
| **Peer 39** | Safe from = **Include** ![Check mark.](media/check.png) | AND |
| **Peer 39** | Negative = **Exclude** ![Exclude mark.](media/exclude.png) | AND |

**What is the IAB audience taxonomy in Segment taxonomy filters?**

The IAB audience taxonomy is a “common nomenclature for audience segment names to improve comparability of data across different providers… (that) designates whether the segment describes attribution that are demographic, interest-based, or purchase-intent based” (see [IAB tech lab](https://iabtechlab.com/standards/audience-taxonomy/) for more details).

**How are the filters determined in Segment taxonomy filters?**

We leverage the tier 1 and tier 2 categorizations in our taxonomy filter and use modeling techniques to categorize segments using their name on behalf of our 3P data partners. Contextual data partners are not included in filter calculations.

> [!NOTE]
> We do not allow data providers to customize this currently.

| Segment Name | Segment Taxonomy |
|---|---|
| **Travel Intent > Hotel Preference > Choice hotels** | - Interest \| Travel <br> - Purchase Intent \| Travel and Tourism |
| **Sports - Interest - Events - Winter Olympics** | - Interest \| Healthy Living <br> - Interest \| Sports <br> - Interest \| Television <br> - Purchase Intent \| Recreation and Fitness Activities <br> - Purchase Intent \| Sporting Goods |
