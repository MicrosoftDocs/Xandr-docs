---
title: Create Publisher Ad Quality Rules
description: In this article, find instructions on how to create publisher base and conditional rules to determine ad quality settings.
ms.date: 10/28/2023
---

# Create Publisher ad quality rules

Publisher base and conditional rules give you the ability to determine which collection of ad quality settings you would like to apply to a particular impression based on attributes such as creative size, placement, or user frequency. The base rule (also called the default rule), is chosen when no conditional rules exist, or when the conditional rules' targeting requirements are not met by an impression.

Only two rules can apply. Since the network rule always applies, these are the possible combinations:

- Network and base rule
- Network and conditional rule

> [!NOTE]
> Configuring ad quality settings beyond the Network Profile is optional. If you choose to configure ad quality settings at the publisher level, you are required to have a Publisher Base Rule. See [Base and Conditional Rules](base-and-conditional-rules.md) for more information on how these rules are applied.
>
> Because Network Profile settings are always enforced, Publisher-level settings will always be more strict than the Network Profile, never less.

## Step 1. Create a publisher base rule

Publisher base rules are created when you create the publisher, unless you select **Use the network ad quality only** on the **Create Publisher** screen. (See [Create a Publisher](create-a-publisher.md) for more information.) When user selects **Use the network ad quality only**, the **Ad Quality (AQ) rules** value under the **Associated Rules** should be **0**, whereas when user selects another option **AQ Rule** value under the **Associated Rules** should be **1**. In that case, when you navigate to the **Ad Quality** screen you'll see a prompt under Publisher Base Rule to **Add base rule**. If you select another option, a base rule gets created and **Default Publisher Ad Quality Rule** appears under the Publisher Base Rule. Keep in mind that the base rule does not employ any targeting because it can potentially be applied to any impression.

To create a publisher base rule:

1. Go to the **Publisher Ad Quality** screen by selecting **Publishers** > **Ad Quality**.

    Alternatively, from the **Publishers** screen, click on or hover over the publisher you want to work with. Select **Ad Quality** from the **Go to** menu for that publisher.

1. Click **Add base rule** (or click **Default rule** under the **Create New** button). The **Create New Base Rule** window will display.

    You can change the name of the default rule, it will still act as the default.

To create a publisher:

1. Select the default option for ad-quality template i.e., the **Network Template**.

1. Select a **Profile Kind**:

    - **Template**: Templates are used to apply ad quality rules to one or more publishers. They are created and updated in Network Ad Quality. When changes are made to a template, those changes are applied to publisher ad quality rules associated with that template. Select this option if you want to manage ad quality settings for a number of publishers at once. Click **Edit** to see a list of templates associated with this Network from which you can choose. See [Create a Publisher Template](create-a-publisher-template.md) for more information.
    - **Custom**: Custom profiles allow you to create a new set of ad quality rules for one publisher. A custom profile may use an existing template as a starting point. Note that changes to templates will not be applied to custom profiles. Check **Copy settings from a template?** and select a template from the list to base your custom profile off an existing template. See [Create a Custom Profile](create-a-custom-profile.md) for more information.

1. Click **Save**.

## Step 2. Create a publisher conditional rule

From the **Publisher Ad Quality** screen, click on **Create Conditional Rule** button.

The **Create New Conditional Rule** dialog will display. Enter a name for the rule, then select a **Profile Kind**. (See Step 1 above for the **Profile Kind** options.) Click **Next**.

> [!NOTE]
> Rules are checked for matches against an impression in priority order. Conditional rules range in priority from 1 to 10, with 10 being the highest. The default priority is 5.
>
> For an example of how conditional rules are matched against an impression, see [Base and Conditional Rules](base-and-conditional-rules.md).

## Step 3. Set targeting for the publisher conditional rule

On the **Targeting** tab of the **Create New Conditional Rule** dialog you can define target settings for the creatives to which this rule applies. After you've created the rule, you can apply additional ad quality standards (see [Explore Publisher Ad Quality](explore-publisher-ad-quality.md)).

> [!NOTE]
> You can not employ any **Profile Information Targeting**, **Inventory Targeting**, or **Geography Targeting** in the network rule or the base rule.

### Frequency

You can apply ad quality settings based on how frequently a user has seen a creative. For example, you might want to have stricter ad quality requirements for the first impression shown to a user on any given day, but after that the settings in the Publisher Base Rule might suffice. See [Frequency and Recency Caps](frequency-and-recency-caps.md) for more information.

### Page Properties (Tags)

You can apply ad quality settings based on where the tag (i.e., placements) is located on the page, or a specific query string passed in the URL.

### Size
You may have different ad quality rules for different creative sizes. 

### Inventory Targeting 

You may have different ad quality requirements for different placements or placement groups, for example, stricter ad quality for a home page.

### Key Value Targeting

You may have different ad quality requirements based on key value pairs. Learn more about [Key Value Targeting](key-value-targeting.md).

### Geography

You may have different ad quality restrictions based on different countries (for example, varying legal restrictions by country). Depending upon which geographic targeting options you choose, you may significantly reduce the likelihood of matching an impression. When more than one targeting type is selected (for example, both Region and Zip Code), the set of matching impressions is reduced, sometimes significantly.

- Example 1: If both the Boston MA-Manchester NH Metro Code and the City of Manchester, NH are selected, only users who are located in both will be targeted. Therefore, users in the City of Boston will not be included at all.
- Example 2: If both the California Region and Chicago, IL Metro Code are selected, then NO users will be targeted since the Chicago metro code does not overlap with California.

> [!NOTE]
> When geographic targeting by IP address, you should expect some degree of inaccuracy; though targeting by country is highly accurate, the more specific the targeting, the more imprecise the results. This is especially true when targeting cities, metro codes, and zip codes. Microsoft Advertising uses the IP lookup service provided by [Digital Envoy](https://www.digitalelement.com/geolocation/). For more information, [contact Digital Envoy directly](http://www.digitalelement.com/contact-us/).

#### Country

You can include all countries, include United States only, or choose to include/exclude specific countries.

#### Region

Regions are based on the method that a country uses to divide itself, such as by states, provinces, territories, etc. You can include/exclude regions in your targeting.

#### Designated Market Area (DMA)

Metro codes are only available for US inventory. Available metro codes range from large cities such as New York, NY and Chicago, IL to smaller cities such as Rochester, NY, Birmingham, AL, and Pittsburgh, PA. You can include/exclude metro codes in your targeting.

#### City

A city differs from a metro code. Unlike metro codes, cities are not limited to US inventory. Cities from around the world are represented. You can include/exclude cities in your targeting.

#### Zip code

Zip codes only apply to US inventory. Targeting by zip code is include only. You can enter up to 4000 zip codes in a 5-digit format (for example, 06514), separated by a comma or new line.

If your list of zip codes is formatted incorrectly, you will be presented with an error message and given the chance to edit and resubmit your zip codes. Some common formatting errors include:

- Excel-Truncated Zeros: Excel may truncate leading zeros from zip codes when copy-pasting, for example, '06514' becomes '6514'.
- Postal Codes, Zip+4: Only 5-digit numeric US zip codes are accepted, for example, '12804'.
- Colons in Ranges: Use hyphens rather than colons to denote ranges, for example, '10001-10010'.
- Descending Ranges: Descending ranges of zip codes are not supported. Use ascending ranges instead, for example, '12561-12804'.

### Size

You may have different ad quality rules for different creative sizes.

