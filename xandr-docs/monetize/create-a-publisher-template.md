---
title: Create a Publisher Template
description: In this article, find step-by-step instructions on how to create and set up a publisher template.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Create a publisher template

A Publisher Template is a collection of ad quality settings created by a network administrator. Publisher Templates ease publisher creation and set-up by allowing a network administrator to define common ad quality settings for a number of publishers at once. When a template is edited, all publishers using that template will be updated with those settings. Use a Publisher Template if you want to maintain a group of publishers' ad quality settings together.

> [!NOTE]
> Associating a publisher with a Publisher Template is optional.

For more information on the relationship between Publisher Templates and Network Profiles, see [Working with Ad Quality](working-with-publisher-ad-quality.md).

## Step 1. Create a new publisher template

To create a new Publisher Template, navigate to the **Network** tab's **Ad Quality** section and click the **Create a Template** button.

> [!TIP]
> You can edit an existing Publisher Template by clicking on its name, then clicking the **Full Edit** button.

The **Create a new ad quality template** dialog will appear. This is where you'll enter the template's name and add any notes you'd like to include. After saving, you'll return to the **Ad Quality** screen, where you'll edit each of the available options as described in Step 2.

## Step 2. Determine which creatives are eligible to serve on your inventory

> [!IMPORTANT]
> The **Ad Servers** option below is in **beta** and not widely available to all customers. We plan to release this feature to all users at a future date.

You can determine which creatives will be eligible to serve on your inventory based on one or more of the following attributes:

- [Bidders](#bidders)
- [Buyers](#buyers)
- [Categories](#categories)
- [Technical Attributes](#technical-attributes)
- [Brands](#brands)
- [Languages](#languages)
- [Ad Servers](#ad-servers)
- [Frequency Caps](#step-3-apply-frequency-caps-to-attributes)

### Bidders

You can manage bidders and individual bidder seats that serve on your inventory by defining trust level settings here. Choose from the following levels:

| Trust Level | Description |
|---|---|
| Banned | Ban all creatives from this buyer. |
| High | Bypass ad quality standards, require platform audit. |
| Maximum | Bypass ad quality standards, do not require platform audit. |
| Medium | Apply ad quality standards, trust buyer self-classification. |
| Standard | Apply ad quality standards, require platform audit. |

The bidders and their seats are mapped to the existing buyer IDs, and all trust settings are inherited by both. Updating trust settings to either one of the sections (Buyers or Bidders) will update trust settings for the same bidder or seat in both sections.

> [!NOTE]
> Updating the trust level for Bidders will apply the same trust level to all Seats. However, Bidder trust can be overridden by updating Seat-level trust settings from **Use Bidder** to another trust level.

The default trust setting for Bidders is inherited from the **Buyers** section and any adjustments to the trust settings should be made in the Buyer’s section. To know more about Buyer Seat IDs, see [Understanding Buyer Seat IDs](understanding-buyer-seat-ids.md).

### Buyers

In the **Buyers** section, click the **Edit** button. You'll be presented with a dialog where you can edit the trust level associated with individual buying members. The buyer trust levels and their descriptions are as follows:

| Trust Level | Description |
|---|---|
| Banned | Ban all creatives from this buyer. |
| High | Bypass ad quality standards, require platform audit. |
| Maximum | Bypass ad quality standards, do not require platform audit. |
| Medium | Apply ad quality standards, trust buyer self-classification. |
| Standard | Apply ad quality standards, require platform audit. |

### Categories

Depending upon the category the creative falls into, you may choose to mark it as:

- **Eligible**: The creative will serve.
- **Banned**: The creative will not serve.
- **Default**: Reuse the default settings (i.e., mark as **Eligible**).

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

> [!IMPORTANT]
> This option is not available to all customers at this time.

You can choose to serve only those creatives that are hosted on a specific set of ad server domains. All ad servers are eligible by default. If you want to allow or ban creatives based on the ad server called by that creative, click **Edit** under **Ad Servers**. This will take you to the **Ad Server** screen. See [Ad Server Settings](ad-server-settings.md) for information on using the **Ad Server** screen to create collections of eligible or banned ad servers.

## Step 3. Apply frequency caps to attributes

You can apply per-user frequency caps to particular creatives based on one or both of the following attributes:

- **Sensitive Categories**: The creative may belong to a sensitive category such as "Dating" or "Politics".
- **Technical Attributes**: The creative may have undesirable technical attributes, such as whether it plays audio.

By default frequency caps are turned off, in which case you'll see **No limit per user** in the upper right corner of the section. To change this, click **No limit per user**. (If frequency caps have already been set, this area will show the frequency, such as **2 imps per day**, rather than **No limit per user**.) This will expand an area where you can set the frequency caps for the attributes and categories to which they're applied.

For more information on frequency caps, see [Frequency and Recency Caps](frequency-and-recency-caps.md).
