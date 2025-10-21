---
title: Query String Targeting via Placement Tags and Segments
description: In this article, find information about how to create and use query strings to target users or placements.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Query string targeting via placement tags and segments

> [!IMPORTANT]
> This form of targeting is only available to Standard Line Items. For an overview of which targeting options are available to Standard versus Augmented Line items, see [Buy-Side Targeting](buy-side-targeting.md).

Placement tag query strings can be used to pass additional information about the user, the inventory they're visiting, or both. This information can be used in several ways, including:

- Putting the user in a segment based on the contents of the query string
- Targeting a user based on the contents of the query string
- Targeting specific inventory based on the contents of the query string

This page describes:

- How to create query string segments
- How to target users and/or inventory based on those query string segments
- How to target placements based on query string parameters

For more information about segment targeting in general, see [Segment Targeting](segment-targeting.md).

For instructions on how to put users in a segment when they view or click a creative, see [Associate Segment Pixels with Creatives](associate-segment-pixels-with-creatives.md).

## What is a query string segment

A query string segment is a type of segment that is defined by a particular parameter or key-value pair that is passed on the query string of the ad call. Types of query string segments include:

- **Query string segments** - These segments make it easier to manage unique segment values. For example, a gaming site might want to place users in a segment based on experience level: a page could be focused for beginners and a user visiting the page would be added to the beginner segment. When a user visits a more advanced page, the user is moved to the advanced segment and is automatically removed from the beginner segment. Multiple values can be provided for this type of query string.

- **Query string key value segments** - These segments allow you to reuse the same key in multiple segments. For example, a music sharing site might want to place users in multiple segments, each of which reflect a diverse music preference (such as rock, pop, or jazz) but which reuses the same key (`music_pref`). Users can be placed in multiple segments, one for each type of music, e.g.,

- `music_pref=rock`
- `music_pref=jazz`

## Creating query string segments

Depending on the type of query string segment you need, follow the instructions in one of the sections below.

- [Add a Query String Segment](#adding-a-query-string-segment)
- [Add a Query String Key Value Segment](#adding-a-query-string-key-value-segment)

### Adding a query string segment

1. Select **Network** > **Segment** or **Advertisers** > **Segment Pixels**.

1. Click **Create Segment**. Provide the following information:
    - **Name**: Type a descriptive name for your reference (for example, user gaming experience).

      > [!WARNING]
      > If the Parameter (Key) name begins with `kw_`, the segment will not be eligible/identified in auctions.

    - **Type**: For this type of segment pixel, select **Query String**.
    - **Parameter**: Type the name of the parameter used to map the segment (for example, `user_experience`). A parameter can only be mapped with one segment at a time, so be sure to give each segment pixel a unique parameter. Parameters are case-insensitive.
    - **Values**: Select **Text**, **Numeric**, **Custom**, or **None**, and provide the specific values (if any) for this parameter. Enter parameter values separated by commas (for example: `beginner,intermediate,expert`). Parameter values are case-insensitive.

      > [!IMPORTANT]
      > - Query string parameters have the following restrictions:
      >
      >   - Parameters and values are case-insensitive
      >   - You can pass up to 40 parameter-value pairs, each of which can have up to 60 characters.
      >   - Each parameter-value pair must follow the `parameter=value` format.
      >   - Microsoft Advertising does not universally support non-Unicode characters. When passing this information, we recommend that you use only Unicode characters to ensure maximum data compatibility.
      >
      > - When you choose the **Custom** option, no text area appears, since values for this segment will always be defined at time of targeting on a line item or campaign.
      > - If a segment is targeting values `0` as well as any negative number, the Impbus will consider the segment as a default value that means no value is actually being passed.
      > [!TIP]
      > You can use an asterisk at the end of the value as a wildcard when entering parameter values, such as `10*` for postal codes beginning with `10`, or `new_york*` to include regions such as `new_york_city`, `new_york_state`, and `new_york_tristate`.

    - **Keep user in segment**: Choose how long you want the user in this segment:
      - Select **Indefinitely** to keep the user in the segment with no specific end time, or choose an end time. With this option, the user is not targetable in the ad call in which this query string was called, but is targetable on each subsequent impression until the specified expiration (if any).
      - Select **Do not keep user in segment** to allow the user to be targetable in the same ad call in which the query string has been called, but then be immediately forgotten. This replicates the behavior described in [Targeting with Query String Placement Tags](#targeting-placement-tag-query-strings) below.
    - **Apply to Inventory**: If you want to only target query string values when they come from specific publishers or sites, choose the **Selected Publishers...** option and add them to the **Selected Items** list.

> [!NOTE]
> For a single query string segment, you should not target both publishers and placement groups. If you target across these inventory tiers, for example, targeting a publisher and placement groups from another publisher, your campaign will not serve.

### Adding a query string key value segment

1. Select **Network** > **Segment** or **Advertisers** > **Segment Pixels**.

1. Click **Create Segment**. Provide the following information:

    - **Name**: Type a descriptive name for your reference (for example, rock music fans).

      > [!WARNING]
      > If the Parameter (Key) name begins with `kw_`, the segment will not be eligible/identified in auctions.

    - **Type**: For this type of segment pixel, select **Query String Key Value**.
    - **Parameter**: Type the name of the parameter used for this segment (for example, `music_pref`). If you want to create multiple segment pixels with the same parameter, simply retype an existing parameter name. Parameters are case-insensitive.
    - **Value**: Type a single value for the parameter for this segment (for example: `rock`). Remember, if you want to add more values for the same parameter, you must create a new segment pixel. Parameter values are case-insensitive and should be Unicode characters only.

> [!TIP]
> You can reuse a query string key value parameter multiple times. To do this, save this segment pixel and then create another one and type the same parameter name. In our example, after we save this segment pixel with the parameter `music_pref` and the value `rock`, we can create a new segment pixel with the parameter `music_pref` and the value `jazz`. Users can be placed in both segments for later targeting.
> [!NOTE]
> Unlike query string parameters, query string key value parameters can only apply to all inventory.

## Targeting query string segments

Follow the instructions below to target query string segments.

- [Getting to Segment Targeting](#getting-to-segment-targeting)
- [Targeting a Text Query String Segment](#targeting-a-text-query-string-segment)
- [Targeting a Custom Query String Segment](#targeting-a-custom-query-string-segment)

### Getting to segment targeting

Once you've created the segment, go to the **Targeting** > **Segment** section of the line item or campaign. You will now be able to target any or all of the specific query string parameters you entered when creating the segment.

> [!TIP]
> This section describes how to target query string segments. For more general information about segment targeting, see [Segment Targeting](segment-targeting.md).

### Targeting a text query string segment

To target a **Text** Query String Segment, drag it to the right side of the segment targeting dialog. Click the pencil icon on the segment to edit the segment's targeting. If you have a lot of values to choose from, you can use the search box next to **Value** to find the ones you want to target.

For more information, see [Segment Targeting](segment-targeting.md).

### Targeting a custom query string segment

To target a **Custom** Query String Segment, drag it to the right side of the segment targeting dialog. Click the pencil **Edit** icon on the segment to edit the segment's targeting. A **Value** text area will appear where you can enter as many comma- or line-separated values as you'd like to target.

For more information, see [Segment Targeting](segment-targeting.md).

## Targeting placement tag query strings

You can target placements based on the query string passed in on the ad request:

1. When creating or editing your line item or campaign, select **Targeting** > **Page Properties**.
1. Under **Query String**, select whether to **Include** or **Exclude** either all or any of a series of query strings.
    - For query string parameters, target just the parameter (for example, `user_experience`). You cannot target individual parameter values. All values for the specified parameters are included.
    - For query string key-value parameters, you can target either the key (`music_pref`), the value (`rock`), or both. If you target both, you must write the key-value pair with the equals sign, e.g. `music_pref=rock`.

:::image type="content" source="media/page-properties-query-string.png" alt-text="Screenshot of the Page Properties dialog that shows the Query String fields to be filled.":::

For an example of how this might work in practice, imagine that a music publisher labels its articles to indicate the type of music discussed in each article. The publisher can then configure its site so that when a placement tag loads in the article, the labels on that article are added to the placement tag's query string. Here's what the placement tag's URL could look like:

```
https://ib.adnxs.com/ttj?id=4976&size=728x90&music_pref=rock 
```

## Related topics

- [Segment Targeting](segment-targeting.md)
- [Export Placement Tags](export-placement-tags.md)
- [Placement Tag Parameters](placement-tag-parameters.md)
- [Create a Segment Pixel](create-a-segment-pixel.md)
- [Create a Placement](create-a-placement.md)
- [Associate Segment Pixels with Creatives](associate-segment-pixels-with-creatives.md)
- [Mobile User Segment Targeting](mobile-user-segment-targeting.md)
