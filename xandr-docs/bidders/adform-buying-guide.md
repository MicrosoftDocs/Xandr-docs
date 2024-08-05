---
title: Adform Buying Guide
description: In this article, find information on how Xandr publishers communicate with their buyers about accessing and targeting Microsoft Monetize's publisher inventory using Adform as their DSP. 
ms.author: shsrinivasan
ms.date: 07/22/2024
---

# Adform buying guide

In partnership with Adform, Microsoft has created this guide to help Monetize publishers communicate with their buyers about accessing and targeting Monetize’ publisher inventory using Adform as their DSP. This information has been created in collaboration with and approved by the Adform team. Note that platforms can and will change regularly. We will do our best to update this guide as needed. 

We recommend that if buyers are having issues, or if they need help using the Adform platform, their first point of contact should be the Adform team.


## Terminology mapping

In some cases, Adform and Microsoft (Monetize) use different terminology, as shown in the following table.

| Adform | Xandr |
|--|--|
| Agency Seat ID or Advertiser Seat ID | Buyer Seat ID |
| Tracked Ads | Impressions |
| Publisher | Seller member |
| Inventory Source | See [Inventory source](#inventory-source) section. |

### Inventory source

Most publishers are accessible by targeting the main inventory source “**Xandr – Monetize SSP (AppNexus)**”. Below is the list of Monetize sellers that are displayed as separate inventory sources.

| Inventory Source Name |
|--|
| 33Across |
| Admixer |
| Baltic Adexchange |
| CPX Interactive |
| Canadian Programmatic Marketplace |
| Dailymotion |
| Adform Xandr |
| FigaroMedias |
| Hi-Media |
| IDG Tech Network |
| IPadex |
| InteractiveMedia CCSP GmbH |
| Intermarkets |
| L'Agora |
| MediaSquare Full Transparent |
| MediaSquare Semi Blind |
| Microsoft Ad Exchange |
| NRC Media |
| Netsprint: Premium Native & Video |
| NextDayMedia (AppNexus) |
| Orange Ad Market |
| Premio – Websystem |
| Prime Real Time BV |
| PubStream Advertising |
| Rossel |
| Schibsted Classified Media |
| Schibsted Media Group |
| Schibsted Media Group Norway |
| Schibsted Media Group Sweden (9943) |
| Semilo |
| Seznam.cz |
| Stailamedia |
| The Moneytizer |
| Viber |
| Webedia Exchange |
| Zodiak Active |
| bRealTime Select |

The above list will help buyers check the Xandr publisher they are trying to deliver on and what inventory source it is included under. For example, if a buyer wants to deliver on Seznam and Microsoft on the open exchange, they should ensure that Seznam.cz and Microsoft Ad Exchange inventory sources are targeted in their line item. 

For deal inventory source targeting, please refer to the [Targeting deals](#targeting-deals) section.

> [!NOTE]
> All inventory sources are enabled by default and buyers can access all open auction inventory available.

## Targeting Xandr inventory on Adform

In the **Inventory tab**, you can manage your inventory sources, deals, domains, and apps by including or excluding them from your targeting list, as well as setting bid multipliers and bid prices in order to achieve the best campaign performance results.

:::image type="content" source="media/adform-a.png" alt-text="Screenshot of the Inventory tab on Adform.":::

In the **Inventory sources** section, you can see the count of all the inventory sources that are selected for your line item. By default, all inventory sources are selected. You can edit the list of inventory sources by clicking on the **Update Selection** button.

Once you click on this button, a side panel with the Inventory Marketplace opens, where you can see the list of all the available inventory sources. In this list, the main inventory source “**Xandr – Monetize SSP (AppNexus)**” will be displayed.

:::image type="content" source="media\adform-b.png" alt-text="Screenshot of the Inventory Sources section on Adform.":::

## Targeting deals

In the **Deals** section, you can see the count of all the deals selected for your line item. You can edit the list of deals by clicking on the **Update Selection** button.

:::image type="content" source="media\adform-c.png" alt-text="Screenshot of the deal count in the Deals section on Adform.":::

The following deal types will be automatically synchronised within the buyer account once they have been created by the seller:

- **Single-buyer deals**: deals will be synced to the selected seat.
- **Multi-buyer deals**: deals will be synced to the selected seats.
- **Bidder level deals**: deals are public and accessible to everyone. So, any clients can accept the deal in Deal Management UI and add it to line item.

The following deal types need to be created manually:

- Curated deals
- Automated deal types (can be manually created if the automatic sync fails)

### Deal Sync (automated deal creation)

If you work with publishers that use Microsoft Monetize, preferred deals, PG, and private auction deals might be available in your Adform DSP account automatically through Deal Sync (please see [Manually Created Deals](#manually-created-deals-including-curated-deals) for exclusions).

#### Targeting deal syncs

1. The publisher sets up the deal in Microsoft Monetize.
1. The publisher assigns the deal to the Adform seat.
1. The publisher sends you the deal name and ID.
1. Adform automatically imports all the deals.
1. Search the **Deal list** to find the deal ID that the publisher has provided to you.
1. Approve the deal.
1. Add the deal to your programmatic line item.

You won't be able to select the deal in your programmatic line item unless it has an "**Approved”** status. If you are unable to find the deals, reach out to [Adform support](mailto:support@adform.com).

### Manually created deals (including Curated deals)

Curate deals and deals under the "**Xandr – Monetize SSP (AppNexus)**” source need to be created manually.

#### Creating a deal manually

1. Click **Inventory** > **Deals**.

1. At the top of the Deals list, click **Create**.

1. In the **Create Deal** panel, enter a relevant **Name** for this deal.

    The name can include up to 255 characters including spaces.

1. In the **Deal ID** box, insert the deal ID provided by the publisher.

    The deal ID can be up to 100 characters.

    > [!IMPORTANT]
    >
    > - You can’t change the deal ID once you save the deal.
    > - Deal IDs are always unique across all SSPs and exchanges.

1. Specify an **Inventory Source** in the list.

    You can start typing to see relevant sources. If you type Xandr, the list shows all inventory sources related to Xandr.

1. To specify a single advertiser that can access the deal, click on **Select** and then choose the advertiser. By default, Adform selects **All**.

1. In the **Pricing** section, specify the **Type** of deal: **Private** or **Preferred**.

    This is for your information only. The type of the deal is agreed upon with the publisher.

1. In the **Price** field, enter the agreed floor price. This is for your information only.

1. Click **Create**.

After you create the deal, Adform shows it in the **Deals** list as an accepted deal.

> [!IMPORTANT]
>
> - The only information you can change once you create a deal is the deal’s name.
> - You can’t delete a deal after you've created it, but you can reject it in the Deals list.

#### Targeting manually created deals

Once you create the deal, you can add it to your programmatic line item targeting setup.

1. On the deal section page, click on the Update Selection button. A side panel with the Marketplace opens, where you can see the list of all available deals.

    :::image type="content" source="media/adform-d.png" alt-text="Screenshot of the list of available deals in the Deals section on Adform.":::

1. Select the deals you want to add to your programmatic line item.

1. Once all deals have been selected, click on the “**Apply Changes**” button to save.

> [!IMPORTANT]
> The Xandr Monetize Inventory Source limitation for deal sync is aimed to be resolved in 2024.

## Programmatic guaranteed (PG) line items

To successfully run PG line items, follow these steps:

1. If a line item has been previously created, pause the line item.

    :::image type="content" source="media/adform-e.png" alt-text="Screenshot of setting the line item status to Paused on Adform.":::

1. Negotiate a deal, offline or online using Xandr's UI.

1. Set up a line item in Adform DSP and make sure to have separate line items per PG deal.

    Please follow the below requirements:
    - Line item pacing should be set as **ASAP** to buy every PG impression.

        :::image type="content" source="media/adform-f.png" alt-text="Screenshot of the line item spend pacing on Adform.":::

    - Line item pricing model should be
        - set as **CPM**,
        - higher than the agreed CPM,
        - include all the fees that may apply.
    No optimisation should be added to the line item.

        :::image type="content" source="media/adform-g.png" alt-text="Screenshot of the line item pricing model on Adform.":::

    - Line item budget needs to be large enough to buy all the agreed impressions.
    - Line item should not have any targeting, Brand Safety or Contextual Targeting selected.
    - Line item should not have any frequency capping set at the line item, order, or campaign level.
    - There can be many line items set to target the deal, but at least one must buy every impression.

1. Create tags for approval at least 48 hours before the campaign start date.

    Tags should include all banner sizes that the deal was negotiated for.

1. Add received deal ID(s) to the line item setup and disable **Open Exchange**.

    :::image type="content" source="media/adform-h.png" alt-text="Screenshot of the deal targeting selection on Adform.":::

    :::image type="content" source="media/adform-i.png" alt-text="Screenshot of the deal inventory source listing on Adform.":::

    :::image type="content" source="media/adform-j.png" alt-text="Screenshot of the deal type listing on Adform.":::

1. Activate the line item only after the tags are approved. See [Approval status of RTB tags](#check-approval-status-of-rtb-tags) for more information.

    :::image type="content" source="media/adform-k.png" alt-text="Screenshot of setting the line item status to Active on Adform.":::

> [!NOTE]
> For requests regarding PG campaigns, please reach out to [Adform support](mailto:support@adform.com).

## Check approval status of RTB tags

All created RTB tags for creatives are sent to inventory sources for approval. Whether you just created a new RTB tag or want to troubleshoot already created tags, you can check RTB Approval Status from the right-side panel in the **Tags Overview** page. A creative gets submitted for Xandr’s approval when it gets assigned to a line item that is actively targeting Xandr inventory.

Here are the different statuses you might see: 

- **Not Supported** - status shown for ad types that are not supported.
- **Not Sent** - initial status for supported banner types. The tag can be sent.
- **In Progress** - once the tag is sent for approval, the status is set to In Progress.
- **Approved** - tag was approved by inventory source.
- **Rejected** - if the ad does not comply with specific inventory source requirements, it cannot be used in bidding. The ad must be modified and re-sent for approval.

> [!NOTE]
> When Third Party Ads are used, the tag approval process can take longer because tags have to go through additional auditing measures in order to verify that no malicious content is being served. This process can take up to 24 hours.
>
> It is highly recommended to assign the creatives to corresponding line items a few days prior to campaign start.

## Buyer identification using buyer seat IDs

Adform supports Xandr's Buyer Seat ID feature. Member breakouts and virtual seats are no longer used for each Adform buyer.

Deals should be set up using Adform Agency or Advertiser Seat IDs. Buyers should confirm their buyer seat ID when requesting a deal from a publisher. If buyers are not aware of their seat id, please contact [Adform support](mailto:support@adform.com).

If a seller is unable to find the seat ID shared by the buyer in the SSP, submit a request to [Xandr Support](https://help.xandr.com/s/) for the buyer seat ID to be added.

To check the RTB tag approval status in Adform Platform:

1. Click **Campaigns** > **Tags** in the left sidebar.
1. Select the tags to check their approval status.
1. Review the information in the five tag status categories in the **RTB Approval Status** widget on the right side of the page:
    1. **Rejected:** The tag doesn't comply with the inventory source's requirements and can't be used in bidding. Remove the banner associated with this tag or resend it for approval.
    1. **Approved:** The inventory source has approved the tag.
    1. **In Progress:** Adform has sent the tag to the inventory source and is awaiting approval.
    1. **Not Supported:** The ad type or the tag isn't supported by the inventory source.
    1. **Not Sent:** This is the initial status of the tag before sending it for approval.
    <br>
    You can view the percentage and number of inventories that have assigned this status to your tags.
1. Click the bottom arrow to expand each status category and view the list of inventories that assigned this status.

Using third-party ads extends the tag approval process, as tags must undergo additional auditing to ensure no malicious content is served. This process can take up to 24 hours. Since some exchanges may take up to 48 hours to approve tags, assign banners to corresponding line items few days before the campaign starts.

## Resend tags for approval

To resend your tags to the publisher for approval after making adjustments, follow these steps:

1. Go to the Tags page and select the tags you want to resend.
1. Click Email button.
1. Choose one of the following options:
    1. Send to all inventory sources: Resends your tags to all publishers, regardless of their approval status.
    1. Send to inventory sources that returned the following status: Resends your tags to publishers that rejected the tag or are still in progress of approving it.
1. Click Send.

> [!NOTE] 
> Contact [Adform support](mailto:support@adform.com) if your tag is approved but statistics aren't collected.

## FAQ(s) and Troubleshooting

### FAQ(s)

1. What should I consider when using complex banners?
If you are running your campaigns in an open auction and your tag is not working, it might be due to using a complex banner. Banners such as expanding, floating, or 3D banners typically require a separate agreement with the publisher. To resolve this, set up an individual deal with the publisher instead of bidding in an open auction. By creating a deal, you can agree on specific placements that support your banners, ensuring that your banner will be displayed properly.

1. Why Aren't My Banner Changes Being Applied?
Once you make changes to a banner and save it, you must republish it to apply those changes. Depending on the type of banner you are creating, to publish the banner, click the **Submit** or "Email" button.

1. Why Were Banners Removed From My Line Item?
Third-party and HTML ads are automatically removed from inactive line items that haven't been scheduled to run for the past three days (72 hours). This is done because these ad types use more resources and can slow down the platform. To get them running again, reassign the ads to your line items and create new tags.

### Troubleshooting

If an Adform buyer has issues serving on Xandr inventory, we recommend that they:

1. Reach out to [Adform support](mailto:support@adform.com) as the first step. Please include deal ID, campaign ID, line item IDs, and creative IDs where available and relevant.
1. If they cannot resolve the issue using Adform, Adform will open a ticket with Xandr platform support.
1. Sellers can reach out to [Xandr Support](https://help.xandr.com/s/) or to their Xandr account manager.

## Buyer identification using buyer seat IDs

- Adform supports Xandr's Buyer Seat ID feature. Member breakouts and virtual seats are no longer used for each Adform buyer.
- Deals should be set up using Adform Agency or Advertiser Seat IDs. Buyers should confirm their buyer seat ID when requesting a deal from a publisher. If buyers are not aware of their seat id, please contact [Adform support](mailto:support@adform.com).
- If a seller is unable to find the seat ID shared by the buyer in the SSP, submit a request to [Xandr Support](https://help.xandr.com/s/) for the buyer seat ID to be added.


## Adform and TCF compliance

Adform only supports TCF 2.0 traffic. Non-TCF 2.0 traffic will be treated as no consent given. Adform is still able to bid on non-TCF 2.0 traffic but only with non-personalised ads.
