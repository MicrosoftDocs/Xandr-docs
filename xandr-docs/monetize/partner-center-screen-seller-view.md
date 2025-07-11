---
title: Microsoft Monetize - Partner Center Screen - Seller View
description: In this article, find information about the settings that you can manage from the seller view of the Partner Center screen.
ms.date: 10/28/2023
---

# Microsoft Monetize - Partner Center screen - Seller view

On the Partner Center screen you can view your partners, search all buyers, manage your profile, manage your default buyer settings, and review impression and click statistics for each buyer.

## Getting to the Partner Center screen

Navigate to the **Partner Center** screen (**Partners** \>  **Partner Center**)

## Switching to buyers mode

If you are a network that also represents buyers, the **Buyers** and **Sellers** tabs display. Click **Buyers** to view the **Partner Center** as a seller looking for buyers.

## Managing your profile

Click the **My Profile** button to edit the information that demand partners will see on your **Partner Details** page. Your profile provides information about your company which helps demand partners understand how you could be useful as a partner. The **My Seller Profile** dialog also displays an overview of the audit quality of your inventory. You can see how much of your inventory has been self-audited (**Seller-reviewed**) and how much has been audited by Microsoft Advertising (**Platform-reviewed**).

For step-by-step instructions on customizing your profile, see [Customize Your Seller Profile](customize-your-seller-profile.md).

## Setting buyer defaults

You can establish default buyer eligibility, allowed payment types, and targeting access settings for all demand partners within the **Default Settings** dialog.

For step-by-step instructions on setting your default settings, see [Set Default Buyer Eligibility, Allowed Payment Types, and Targeting Access](set-default-buyer-eligibility-allowed-payment-types-and-targeting-access.md).

It is possible to override these settings for individual demand partners. For details, see [Edit Buyer Eligibility, Allowed Payment Types, and Targeting Access](edit-buyer-eligibility-allowed-payment-types-and-targeting-access.md).

### Setting default buyer eligibility

- **Eligible** - You can sell inventory to this partner, since the ads they would like to serve have proven trustworthy (i.e., this partner's ads meet your ad quality requirements). If you select this, you must define the payment methods you will accept and the targeting information you will provide. See the [Setting default allowed payment types](#setting-default-allowed-payment-types) and [Setting default targeting access](#setting-default-targeting-access) sections below.

- **Blocked** - You will **not** sell any inventory to this member for any number of reasons. For example, you may have a direct relationship with a buyer, and you wish to avoid allowing them access to your inventory at a potentially lower price via RTB.

  This setting is similar to banning or trusting members in [Working with Ad Quality](working-with-publisher-ad-quality.md). If you ban a buyer there or in Partner Center, that member will be banned. A member does not need to be banned in both places.

### Setting default allowed payment types

This indicates the types of payment you accept from eligible partners.

If you allow CPC and CPA payment, you must also set up publishers to accept CPC and CPA payment types as described in [Create a Publisher](create-a-publisher.md).

For more information, see [CPC and CPA Payment Types](cpc-and-cpa-payment-types.md).

### Setting default targeting access

This indicates the information each member receives when targeting your inventory. Members cannot report on this information; it is only used for targeting. The more information you give buyers, the more easily they can target your inventory.

- **URLs** - Expose your domains to allow members using allowlists to more easily target your inventory. You will have the option to expose domains or full URLs to some external buyers.
- **Category (Universal)** - Expose information you provide to allow the buyer to target via universal categories. For more information on assigning categories when creating a placement, see [Create a Placement](create-a-placement.md).
- **Category (Custom)** - Expose custom categories to grant the buyer the ability to target customized slices of inventory that you have collected into a category. For more information on adding a placement to a custom category, see [Create a Placement](create-a-placement.md).
- **Age** - Expose information you provide to allow the buyer to target via age. For more information on using an age macro when exporting your placement, see [Placement Tag Parameters](placement-tag-parameters.md).
- **Gender** - Expose information you provide to allow the buyer to target via gender. For more information on using a gender macro when exporting your placement, see [Placement Tag Parameters](placement-tag-parameters.md).
- **Placements** - Expose the placement name to allow the buyer to more easily target a specific placement.
- **Publishers** - Expose a publisher's name and ID to allow the buyer to more easily target a specific publisher.

## Viewing buyers

The **Buyers** tab will list all buyers, both Monetize members and external bidders. Each buyer's member name and ID will display along with statistics. The statistics reflect your transactions with the buyer over the time period indicated in the **Show Transactions From** drop-down. Search for buyers (see the [Searching for buyers](#searching-for-buyers) section below) to find a specific type of buyer and then review the statistics to determine if you'd like to partner with the buyer.

### Transactions with buyer

- **Imps** - Number of impressions that the buyer has purchased from you.
- **Clicks** - Number of clicks that were generated from inventory that was purchased from you.
- **CTR** - Buyer's click-through rate on your inventory.
- **Revenue** - Amount of revenue that you earned from the buyer.
- **Profit** - Amount of profit that you earned from the buyer, calculated by subtracting media cost from revenue.

## Searching for buyers

Use the filters to search the **Buyers** list for a buyer that meets your partnership needs. You can filter the list of buyers by:

- **Name/ID** - A specific buyer's name or member ID.

- **Primary Market** - The country in which the buyer purchased 50% or more of their total RTB impressions. Buyers who do not purchase 50% or more in a single country will not have a primary market.

- **Buyer Eligibility** - Eligibility settings you have defined for buyers.

- **Allowed Payment Types** - Payment types you have allowed for buyers. Select **Any Type** to search for buyers from whom you accept any of the payment types you have checked. Or, select CPM Only to search for buyers from whom you only accept CPM payment.

- **Targeting Access** - Targeting access you have exposed to buyers.

  Click the **Hide Search Filters** icon ("**<**") to collapse the section and provide more viewing space for your partner lists.

## Viewing partnership details

Click on a buyer's name to view the Partner Details screen for that buyer. You can then review and manage your relationship with the buyer, view spending trends, and access any active or upcoming deals.

See [Partnership Details Screen - Seller View](partnership-details-screen-seller-view.md) for more information.

## Related topics

- [Edit Buyer Eligibility, Allowed Payment Types, and Targeting Access](edit-buyer-eligibility-allowed-payment-types-and-targeting-access.md)
- [Managing Relationships with Buyers](managing-relationships-with-buyers.md)
- [Partnership Details Screen - Seller View](partnership-details-screen-seller-view.md)
- [Set Default Buyer Eligibility, Allowed Payment Types, and Targeting Access](set-default-buyer-eligibility-allowed-payment-types-and-targeting-access.md)
