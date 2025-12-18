---
title: Create a Custom Profile
description: Explore creating a distinct Ad Quality Profile for a publisher, either from scratch or using a template, ensuring immunity to future template modifications.
ms.date: 12/17/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Create a custom profile

A Custom Ad Quality Profile contains a collection of ad quality settings for one publisher. You can create a Custom Profile from scratch or you can use an existing [publisher template](create-a-publisher-template.md) as a starting point. If you base your Custom Profile off of an existing template, keep in mind that future changes to that template
will not be applied to the Custom Profile. Use a Custom Profile if you want to maintain unique ad quality settings for one publisher.

## Step 1. Create or update a Base or Conditional rule

To create a new Custom Profile, select **Publishers \>  Ad Quality** from the top navigation menu. This will take you to the Publisher Ad Quality screen. To edit an existing rule, click on a rule from the list at the upper left-hand side of the screen. When the rule is highlighted, click the Full Edit button on the lower right. To create a new rule, follow the directions in [Create Publisher Ad Quality Rules](create-publisher-ad-quality-rules.md).

In the rule editing dialog that appears, under **Profile Kind**, click **Custom**. If you don't want to base this rule off an existing template, uncheck the **Copy settings from a template?** checkbox. If this checkbox is checked, you'll be able to base this Custom Profile on one of your available Publisher Templates. Note that updates to a Publisher Template are not applied to Custom Profiles inheriting from that template, since Custom Profiles are used to maintain a single publisher's ad quality. If you would like to create ad quality settings that can be applied to more than one publisher, see [Create a Publisher Template](create-a-publisher-template.md).

Click **Save** to update your settings.

After saving, you'll return to the Publisher **Ad Quality** screen. Note that your currently highlighted rule is
now marked as "Custom".

## Step 2. Determine which creatives are eligible to serve on your inventory

You can determine which creatives will be eligible to serve on your inventory based on one or more of the following attributes:

- [Bidders](create-a-custom-profile.md#bidders)
- [Buyers](create-a-custom-profile.md#buyers)
- [Bidders and Buyers](create-a-custom-profile.md#bidders-and-buyers) (Limited Beta)
- [Categories](create-a-custom-profile.md#categories)
- [Technical Attributes](create-a-custom-profile.md#technical-attributes)
- [Brands](create-a-custom-profile.md#brands)
- [Languages](create-a-custom-profile.md#languages)
- [Ad Servers](create-a-custom-profile.md#ad-servers) (Not available to all customers)

### Bidders

> [!NOTE]
> This feature is currently in Closed Beta.

You can manage bidders and individual bidder seats that serve on your inventory by defining trust level settings here. Choose from

| Trust Level | Description |
|---|---|
| Standard | Apply ad quality standards, require platform audit. |
| Medium | Apply ad quality standards, trust buyer self-classification. |
| High | Bypass ad quality standards, require platform audit. |
| Maximum | Bypass ad quality standards, do not require platform audit. |
| Banned | Ban all creatives from this buyer. |

The bidders and their seats are mapped to the existing Xandr Member IDs. Updating trust settings to either one of the sections (Buyers or Bidders) will update trust settings for the mapped bidder or seat in both sections. 

> [!NOTE]
> Updating the trust level for Bidders will apply the same trust level to all Seats. However, Bidder trust can be overridden by updating Seat-level trust settings from Use Bidder to another trust level.

The default trust setting for Bidders is inherited from the default trust setting for Buyers. To know more about Buyer Seat IDs, see [Understanding Buyer Seat IDs](understanding-buyer-seat-ids.md).

### Buyers

In the Buyers section, click the Edit button. You'll be presented with a dialog where you can edit the trust level associated with individual buying members. The buyer trust levels and their descriptions are as follows:

| Trust Level | Description |
|--|--|
| Standard | Apply ad quality standards, require platform audit. |
| Medium | Apply ad quality standards, trust buyer self-classification. |
| High | Bypass ad quality standards, require platform audit. |
| Maximum | Bypass ad quality standards, do not require platform audit. |
| Banned | Ban all creatives from this buyer. |

### Bidders and Buyers

> [!NOTE]
> The combined Bidders and Buyers feature in Ad Quality rules is currently in Limited Beta.

You can manage bidders, their associated members, and individual buyer seats that serve on your inventory by configuring trust level settings.

**Trust levels**

Choose from the following trust levels:

| Trust level  | Description                                                     |
| ------------ | --------------------------------------------------------------- |
| **Standard** | Apply ad quality standards and require platform audit.          |
| **Medium**   | Apply ad quality standards and trust buyer self-classification. |
| **High**     | Bypass ad quality standards and require platform audit.         |
| **Maximum**  | Bypass ad quality standards and don’t require platform audit.   |
| **Banned**   | Block all creatives from this buyer.                            |

**Inheritance and overrides**
- **Bidders** inherit the **Default Trust** by default. You can set the Default Trust to **Standard**, **Medium**, or **Banned**, and override trust levels for specific bidders.
- **Members** inherit the trust level of their parent bidder. You can configure member-level overrides to apply a different trust level.
- **Buyer seats** inherit the trust level of their parent member. You can configure seat-level overrides to apply a different trust level.

**Important information**

- Every bidder is mapped to at least one **Microsoft Monetize Member ID**. A bidder can be mapped to multiple Member IDs.
- If a bidder has transitioned to bidding with buyer seats, those buyer seat IDs are also mapped to an existing Microsoft Monetize Member ID.
- A Microsoft Monetize Member ID can be mapped to multiple buyer seats, but each buyer seat ID maps to only one Member ID.
- Sellers participating in this **Limited Beta** won’t see separate **Bidders and Buyers** sections.

> [!NOTE]
> Not all bidders define buyers using buyer seat IDs. Some bidders define buyers only through Microsoft Monetize Member IDs.
> For more information, see [Understanding buyer seat IDs](understanding-buyer-seat-ids.md).



### Categories

Depending upon the category the creative falls into, you may choose to mark it as:

- **Eligible**: The creative will serve.
- **Banned**: The creative will not serve.
- **Default**: Reuse the default settings (i.e., mark as **Eligible**).

For more details, see [Ad Quality Models](ad-quality-models.md).

### Technical attributes

You may allow or disallow certain creatives based upon technical attributes such as whether the creative is an expandable, or whether it plays audio. Choose from:

- **Eligible**: The creative will serve.
- **Banned**: The creative will not serve.
- **Default**: Reuse the default settings (i.e., mark as **Eligible**).

### Brands

There may be creatives associated with certain brands that you would prefer don't serve on your inventory. You can define those settings here. Choose from:

- **Eligible**: The creative will serve.
- **Banned**: The creative will not serve.
- **Default**: Reuse the default settings (i.e., mark as **Eligible**).

You can enter a list of brands with the **Bulk Search** option.

You can also filter and show only those brands that are new in the last 7 days.

### Languages

Your inventory may interest users who speak certain languages; you can choose to allow creatives using those languages here. You may also exclude creatives using certain languages. Choose from:

- **Eligible**: The creative will serve.
- **Banned**: The creative will not serve.
- **Default**: Reuse the default settings (i.e., mark as **Eligible**).

### Ad servers

You can choose to serve only those creatives that are hosted on a specific set of ad server domains. All ad servers are eligible by default. If you want to allow or ban creatives based on the ad server called by that creative, click **Edit** under **Ad Servers**. This will take you to the **Ad Server** screen. See [Ad Server Settings](ad-server-settings.md) for information on using the **Ad Server** screen to create collections of eligible or banned ad servers.

## Step 3. Apply frequency caps to attributes

You can apply per-user frequency caps to particular creatives based on one or both of the following attributes:

- **Sensitive Categories**: The creative may belong to a sensitive category such as "Dating" or "Politics".
- **Technical Attributes**: The creative may have undesirable technical attributes, such as whether it plays audio.

By default frequency caps are turned off, in which case you'll see **No limit per user** in the upper right corner of the section. To change this, click **No limit per user**. (If frequency caps have already been set, this area will show the frequency, such as **2 imps per day**, rather than **No limit per user**.) This will expand an area where you can set the frequency caps for the attributes and categories to which they're applied.

For more information on frequency caps, see [Frequency and Recency Caps](frequency-and-recency-caps.md).

## Related topics

- [Working with Ad Quality](working-with-publisher-ad-quality.md)
- [Explore Publisher Ad Quality](explore-publisher-ad-quality.md)
- [Create Publisher Ad Quality Rules](create-publisher-ad-quality-rules.md) 
- [Base and Conditional Rules](base-and-conditional-rules.md)
- [Network Ad Quality Screen](network-ad-quality-screen.md)
- [Update Your Network Profile](update-your-network-profile.md)
- [Create a Publisher Template](create-a-publisher-template.md)
- [Ad Quality Order of Operations](ad-quality-order-of-operations.md)
