---
title: Create a Bias Rule
description: Optimize auctions:, apply bias, set buyer rules, use conditional impressions. Define biases (frequency, geography, placement) without altering winning bids.
ms.date: 10/21/2024
---

# Create a bias rule

> [!NOTE]
> This feature is not available by default. If you are interested in gaining access or discussing potential use cases that may apply to your business, reach out to your Microsoft Advertising representative.

You can create bias rules to make bids appear higher or lower than they actually are, thereby influencing the outcome of an auction.

Create a base rule to affect bids from a specific buyer or buyer group on all of the publisher's inventory.

Create a conditional rule to affect bids from a single buyer or buyer group on specific impressions.

You can define a per-buyer bias by impression frequency, geography, segment, specific placement, category, or placement size. Biases affect the way that the auction operates, but not the amount the winner pays.

For more information on biases and how they work, see [Working with Yield Management](working-with-yield-management.md).

## Create a base bias rule

> [!NOTE]
> The legacy Bias Rules UI has been deprecated. To create your base rule, use the [Yield Management Bias Service](../digital-platform-api/yield-management-bias-service.md).

Create a base rule to affect specific buyer's or buyer group's bids on all of the publisher's inventory.

<!-- ### Getting there

**Publisher-only clients:** Select **Partners** \>  **Yield Management** \>  **Floor rules** in the menu bar, and then select a publisher if you are prompted.

**All other clients:** Select **Publishers** \>  **Floor Rules** in the menu bar, and then select a publisher if you are prompted.

### Step 1. Get started with Bias Rule Manager

Select a publisher when you are prompted. This opens the **Bias Rule Manager**.

### Step 2. Open the create new base rule dialog

Click **Create New \>  Base Rule**, or click on the **Create a base rule** link within the **Bias** section of the screen to open the **Create New Base Rule** dialog. -->

> [!NOTE]
> You can only create one base rule. If a base rule exists, you will not be able to create a new base rule. Instead, you can edit or delete the existing rule.

### Base rule details

Enter the basic details for the base rule.

- **Name** - Enter a name for your rule. It is recommended to select a name that aligns with your business strategy for ease of use.
- **Priority** - The base rule is automatically set to Priority 1 (lowest). This means any existing conditional rules will take precedence over the base rule.
- **Description** - Enter a rule description for reference.
- **Additional Options: Code** - If you click **Additional Options (Advanced)** you will have the option of entering a code. Codes may be helpful for networks with distinct internal names/IDs, so that the names/IDs can be associated in Monetize and then extracted for reporting purposes via our API.

<!-- ### Step 4. Save the base bias rule

Once you have entered the rule details, click **Save**. The rule will then display under **Bias Rule** on the **Bias Rule Manager** screen. The base rule will be selected and the **Buyers** and **Buyer Groups** tables will display in the **Bias Settings** section. -->

### Define bias amounts

You can define bias values for specific buyers and for specific buyer groups.

- Define bias amounts for specific buyers
- Define bias amounts for buyer groups

Biases can either be positive (preference) or negative (deterrent) values and defined as either a percentage or CPM.

- Percentage - The buyer's bids will be modified by a certain percent.
- CPM - The buyer's CPM bid will be modified by a specific amount.

<!-- ### Define bias amounts for specific buyers

Click **Edit** in the **Buyers** table to display the **Buyer Bias Settings** dialog. Use the name and bias type filters to locate the desired buyer, and then click **edit**
near the buyer.

> [!IMPORTANT]
> To streamline the process of editing multiple buyer's bias settings, you can display the edit tools for all buyers within the list by clicking **Mass edit**.

Select a bias type from the dropdown in the **Bias Type** column, and then enter a value in the field in the **Bias Value** column. You can enter a positive (preference) or negative(deterrent) value for either of the bias types.

- **Percentage** - The buyer's bids will be modified by a certain percent.
- **CPM** - The buyer's CPM bid will be modified by a specific amount.

When you have entered the desired bias amount for the buyer, click the **Save** button within the row.

When you have entered all of the needed bias amounts per buyer, click **Close** to finish editing the base rule.

### Define bias amounts for buyer groups

Click **Edit** in the **Buyer Groups** table to display the **Buyer Group Bias Settings** dialog. Use the name and bias type filters to locate the desired buyer group, and then click edit near the buyer group. You can create buyer groups under **Network** \> **Partners** \> **Demand Partners** \> **Add New Group**.

> [!IMPORTANT]
> To streamline the process of editing multiple buyer group's bias settings, you can display the edit tools for all buyer groups within the list by clicking **Mass edit**.

Select a bias type from the dropdown in the **Bias Type** column, and then enter a value in the field in the **Bias Value** column. You can enter a positive (preference) or negative (deterrent) value for either of the bias types.

- **Percentage** - Bids from buyers in the group will be modified by a certain percent.
- **CPM** - CPM bids from buyers in the group will be modified by a specific amount.

When you have entered the desired bias amount for the buyer group, click the **Save** button within the row.
When you have entered all of the needed bias amounts per buyer group, click **Close** to finish editing the base rule. -->

## Create a conditional bias rule

Create a conditional rule to affect buyer's or buyer group's bids on specific impressions. You can define a per-buyer bias by impression frequency, geography, segment, specific placement, category, or placement size.

## Bias rule targeting

You can target bias rules using profiles created via the [Profile Service](../digital-platform-api/profile-service.md). The following targeting parameters are applicable to a Bias Rule.

### Frequency

You can choose whether to exclusively serve to users with known identifiers or also serve to anonymous (cookieless) users.

### Geography

You can target specific countries, regions, metro codes, cities, or zip codes.

> [!WARNING]
> Be careful which geographic targeting options you choose; you may significantly reduce the likelihood of matching an impression. For more information, see the note below.
> [!IMPORTANT]
> **A note on the accuracy of geographic targeting by IP address**
>
> Users of geographic targeting should expect some degree of inaccuracy; though targeting by country is highly accurate, the more specific the targeting, the more imprecise the results. This is especially true when targeting locations as granular as cities, metro codes, and zip codes.
>
> Microsoft Advertising uses the IP lookup service provided by [MaxMind](https://www.maxmind.com). For more information, read about their [GeoIP Technology](https://www.maxmind.com/en/geolocation_landing) or [contact MaxMind directly](https://www.maxmind.com/company/contact-us).
>
> **Geographic targeting and boolean logic**
>
> When more than one targeting type is selected (e.g. both **Region** and **Zip Code**), the set of matching impressions is reduced, sometimes significantly. For example, if both the Boston MA-Manchester NH **Metro Code** and the **City** of Manchester, NH are selected, only users who are located in both will be targeted. Therefore, users in the **City** of Boston will not be included at all. Another example: if both the California **Region** and Chicago, IL **Metro Code** are selected, then NO users will be targeted  since the Chicago metro code does not overlap with California.

- Regions are a more granular target than Country. Generally speaking, regions are based upon whatever method the country in question uses to divide itself into parts. For example, regions within the United States are states. Canada is divided into its provinces, and India is divided into its states and union territories.
- Metro codes are smaller than regions and are only available for US inventory. Available metro codes range from large cities such as New York, NY and Chicago, IL, to smaller cities such as Rochester, NY, Birmingham, AL, and Pittsburgh, PA.
- A City is different than a Metro Code. It may be larger or smaller, depending upon your selection. Unlike metro codes, cities are not limited to US inventory. Cities from all around the world are represented, ranging from Tel Aviv, Israel to Kuala Lumpur, Malaysia.

### Segments

By default, if you are targeting multiple segments, users must be associated with **all** of the targeted segments in order for the rule to apply. You can change this to **any** of the targeted segments via the [Profile Service](../digital-platform-api/profile-service.md). For more information, see [Segment Targeting](../digital-platform-api/profile-service.md#segment-targets).

For segments, you can also define the length of time users have to belong to the segment in order for the rule to apply.

### Supply

You can target specific placements, content categories, or placement sizes.

> [!NOTE]
> If you target a specific placement, this rule will only apply to bids on that placement.

For content categories, you can specify if you want to allow unknown content categories for inventory that hasn't been categorized.

<!-- ### Getting there

**Publisher-only clients:** Select **Partners \> Yield Management \> Floor rules** in the menu bar, and then select a publisher if you are prompted.

**All other clients:** Select **Publishers \>  Floor Rules** in the menu bar, and then select a publisher if you are prompted.

### Step 1. Get started

Select a publisher when you are prompted. This opens the **Bias Rule Manager**.

### Step 2. Open the Create New Conditional Rule dialog

Click **Create New \>  Conditional Rule** to open the **Create New Conditional Rule** dialog.

### Step 3. Enter rule details

Enter the basic details for the conditional rule.

- **Name** - Enter a name for your rule. It is recommended to select a name that aligns with your business strategy for ease of use.
- **Priority** - Select the desired priority for the rule, Priority 5 is selected by default. It is recommended to leave lower priorities (1-4)
  for network-wide rules and use higher priorities (5-9) for your publisher-specific rules. It is a good idea to reserve priority 10 for special cases that may arise, such as emergencies or blockers.
- **Description** - Enter a rule description for reference.
- **Additional Options: Code** - If you click **Additional Options (Advanced)** you will have the option of entering a code. Codes may be helpful for networks with distinct internal names/IDs, so that the names/IDs can be associated in Monetize and then extracted for reporting purposes via our API. -->

<!-- ### Step 4. Set audience targeting (optional)

In the **Audience Targeting** tab, you can select the types of users (audience) you would like the rule to apply to.

### Target frequency

Check the **Apply browser session frequency range** checkbox to create a bias rule that applies to bids from creatives the user has viewed a certain number of times. Enter the frequency range that you would like the rule to apply to. Then select the **Scope**, which indicates if you would like frequency to be calculated based on views on inventory across the entire platform (**Platform-wide**), or only views on the publisher's inventory (**Publisher**).

Check the **Show to users without cookies** to have the rule also apply to bids from creatives that have been shown to cookieless users. When this option is selected, you may violate the frequency rang you have set since it's difficult to track views for cookieless users.

### Target geography

Select **Audience Targeting \> Geography** to create a bias rule that applies to impressions in certain geographic regions. You can target specific countries, regions, metro codes, cities, or zip codes.

> [!WARNING]
> Be careful which geographic targeting options you choose; you may significantly reduce the likelihood of matching an impression. For more information, see the note below.
> [!IMPORTANT]
> **A note on the accuracy of geographic targeting by IP address**
>
> Users of geographic targeting should expect some degree of inaccuracy; though targeting by country is highly accurate, the more specific the targeting, the more imprecise the results. This is especially true when targeting locations as granular as cities, metro codes, and zip codes.
>
> Microsoft Advertising uses the IP lookup service provided by [MaxMind](http://www.maxmind.com). For more information, read about their [GeoIP Technology](http://www.maxmind.com/en/geolocation_landing) or [contact MaxMind directly](http://www.maxmind.com/app/contact).
>
> **Geographic targeting and boolean logic**
>
> When more than one targeting type is selected (e.g. both **Region** and **Zip Code**), the set of matching impressions is reduced, sometimes significantly. For example, if both the Boston MA-Manchester NH **Metro Code** and the **City** of Manchester, NH are selected, only users who are located in both will be targeted. Therefore, users in the **City** of Boston will not be included at all. Another example: if both the California **Region** and Chicago, IL **Metro Code** are selected, then NO users will be targeted  since the Chicago metro code does not overlap with California.

**Target countries:**

Click the **Edit** link for **Country**, and then select one of the three options: **Include all countries**, **Include United States only**, or **Include/Exclude a specific list of countries**.... If you select **Include/Exclude a specific list of countries**..., select countries in the **Available List** area and then click **Add** to add them to the **Chosen List**. The rule will apply to impressions in any of the countries within the **Chosen List**.

**Target regions:**

Click the **Edit** link for **Region**, and then select one of the two options: **Include all regions** or **Include/Exclude specific list of regions**.... If you select **Include/Exclude specific list of regions**..., click **Add** near regions in the **Available Regions** area to add them to the **Targeted Regions** area. The rule will apply to impressions in any of the regions within the **Targeted Regions** area.

Region is a more granular target than Country. Generally speaking, regions are based upon whatever method the country in question uses to divide itself into parts. For example, regions within the United States are states. Canada is divided into its provinces, and India is divided into its states and union territories.

**Target metro codes:**

Click the **Edit** link for **Metro Code**, and then select one of the two options: **Include all metro codes** or **Include/Exclude specific list of metro codes**.... If you select **Include/Exclude a specific list of metro codes**..., select metro codes in the **Available List** area and then click **Add** to add them to the
**Chosen List**. The rule will apply to impressions in any of the metro codes within the **Chosen List**.

Metro codes are smaller than regions and are only available for US inventory. Available metro codes range from large cities such as New York, NY and Chicago, IL, to smaller cities such as Rochester, NY, Birmingham, AL, and Pittsburgh, PA.

**Target cities:**

Click the **Edit** link for **City**, and then select one of the two options: **Include all cities** or **Include/Exclude specific list of cities**.... If you select
**Include/Exclude a specific list of cities**..., click **Add** near cities in the **Available List** area to add them to the **Chosen ist**. The rule will apply to impressions in any of the cities within the **Targeted Cities** area.

A City is different than a Metro Code. It may be larger or smaller, depending upon your selection. Unlike metro codes, cities are not limited to US inventory. Cities from all around the world are represented, ranging from Tel Aviv, Israel to Kuala Lumpur, Malaysia.

**Target zip codes:**

Click the **Edit** link for **Zip Code**, and then enter or paste the list of comma-separated or newline-separated 5-digit zip codes that you would like to target in the **Zip Codes** field. Click **Validate** and the system will verify that your zip codes are formatted correctly. The rule will apply to impressions in any of the entered zip codes. If your list of zip codes is formatted incorrectly, you will be presented with an error message and given the chance to edit and resubmit your zip codes. Those zip codes that failed the formatting validation will be listed above the line marked **See Errors Above** inside the text area. If you hover over the help bubble to the right of the text area, you will be presented with a list of the most common errors:

- **Excel-Truncated Zeros**: Excel may truncate leading zeros from zip codes when copy-pasting, e.g. `06514` becomes '6514'. To prevent this from happening, set the cell formatting of your spreadsheet to Zip Code under the Numbers header of the Format Cells dialog.
- **Postal Codes, Zip+4**: Only 5-digit numeric US zip codes are accepted, e.g. `12804`.
- **Colons in Ranges**: Use hyphens rather than colons to denote ranges, e.g. `10001-10010`.
- **Descending Ranges**: Descending ranges of zip codes are not supported. Use ascending ranges instead, e.g. `12561-12804`.

Unlike the other settings listed here, targeting by Zip Code is include-only. Exclude certain zip codes by entering only those you want to target. Like metro codes, zip codes only apply to US inventory.

### Target segments

Select **Audience Targeting** \> **Segment** to create a bias rule that applies to impressions seen by users in certain segments. Check the checkboxes near the segments you would like to target in the **Available Segments** area to add them to the **Targeted Segments** area.

When targeting multiple segments, impressions must be associated will **all** of the targeted segments in order for the rule to apply by default. You can select **any** from the **Target all of the following segments:** dropdown in order for the rule to apply to impressions associated with any of the targeted segments.

In the **Require/Exclude** dropdown, select **Require** to target users that belong to the segment, or **Exclude** to target users that do not belong to the segment.

Click **edit** in the **Segment Age** column to define the length of time users have to belong to the segment in order for the rule to apply.

Check the **Show segment codes** checkbox to display an additional **Code** column within the table. If you entered a code when creating the segment, it will display in this column.

Check the **Show values** checkbox to display an additional **Value** column within the table where you can specify portions of the segment that the rule should apply to. Click **edit** in the **Value** column, select a value type from the **Value** dropdown, enter the value(s), and then click **Set**. This feature is only relevant if the segment you are targeting is a query string segment where parameters have been defined. For example, let's say you have defined a travel segment that has 2 travel_location parameters: US and Canada. If you would like the floor rule to apply to the users within the segmentintending to travel to the US, you can select **equal to** in the **Value** dropdown and then enter US in the text field.

Rather than targeting any or all of the selected segments, you can click on the **Boolean Logic** header to apply more complex logic. -->

<!-- ### Step 5. Set supply targeting (optional)

In the **Supply Targeting** tab, you can select specific inventory you would like the rule to apply to. You can target specific placements, content categories, or placement sizes.

### Target placements

Select **Include specific placements only**... to create a bias rule that applies to specific placements. Click on a publisher in the **Available List** area to
display that publisher's exposed placements. Then click **Add** near placements to add them to the **Selected List**. You can also click **Add** near a publisher in the
**Available List** area to add all of the publisher's exposed placements at once.

> [!NOTE]
> If you target a specific placement, this rule will only apply to bids on that placement.

### Target content categories

Select **Include a specific list of content categories**... to create a bias rule that applies to inventory within a specific category. Click on a category type in the **Available Content Categories** area to display the list of available categories. If you have selected **Universal Content Categories**, click on a category name to display the list of available subcategories. Then click **Add** near categories to add them to the **Targeted Content Categories** area. You can also click **Add** near a universal category in the **Available Content Categories** area to add all of the subcategories at once. Check the **Allow unknown content categories** checkbox for the rule to apply to inventory that has not been categorized.

> [!NOTE]
> Universal content categories apply to platform-wide inventory, while custom content categories are applied only to your managed inventory.

### Target sizes

Select **Specific sizes**... to create a bias rule that applies to inventory of a specific size. Click on a size to select it for targeting. You can shift+click or command+click to select multiple sizes within the list. You can also enter a custom size by entering the dimensions in the **Add a new size target for this rule** fields, and then clicking
**Add Size**. The size you have added with then display at the bottom of the list under the **Custom Sizes** header.

### Step 6. Save the conditional bias rule

Once you have defined the rule targeting, click **Save**. The rule will then display in the conditional rules section on the **Bias Rule Manager** screen. -->

### Related topics

- [Understanding Yield Management](understanding-yield-management.md)
- [Create a Floor Rule](create-a-floor-rule.md)
- [Update Bias Rules](update-bias-rules.md)
- [Update Floor Rules](update-floor-rules.md)
- [Segment Targeting](segment-targeting.md)
- [Query String Targeting via Placement Tags and Segments](query-string-targeting-via-placement-tags-and-segments.md)
