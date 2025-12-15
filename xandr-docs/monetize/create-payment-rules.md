---
title: Create Payment Rules
description: In this article, find step-by-step instructions on how to create and set up payment rules.
ms.date: 12/15/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Create payment rules

Payment Rules represent a financial agreement between a network and a publisher. A network may have a single payment rule for all impressions from a publisher, or it might have a **Base rule** that serves as a default. More specific **Conditional rules** that apply to individual impressions based on geography, frequency, or other targeting can be defined.

For each publisher, you will create one base rule specifying either revenue sharing or CPM payment terms. This rule will apply when no more specific conditional rule applies. For more information about base rules, see [Base and Conditional Rules](base-and-conditional-rules.md).

## Step 1. Set a base payment rule

When you create a publisher, you must create a base payment rule. Navigate to the **Payment Terms** tab and choose one of the **Pricing Type** options from the dropdown:

- **Revenue share**: Indicate the percentage of network revenue that you will give to the publisher.
- **CPM**: Indicate the dollar amount that you will give to the publisher when a creative is served (as a CPM amount). Also, you can  indicate that you will pay this amount even when a default creative is served by checking the checkbox for **CPM payment should be applied when a default is served**.

You cannot create nor edit a publisher's base payment rule from the [Update Payment Rules](update-payment-rules.md) screen.

## Step 2. Set conditional payment rules (Optional)

From the main menu, select **Publisher** > **Payment Rules** > **Publisher Tab** to create a conditional payment rule. Conditional rules are like base rules except you may adjust the priority of the rules, they have start and end dates, and they have targeting options. For more information, see [Base and Conditional Rules](base-and-conditional-rules.md).

### Enter payment rule details

- **Name**: Enter a name for the rule.
- **State**: Indicate whether this rule is **Active** or **Inactive**.
- **Priority**: Select the order in which this rule will be considered when compared to other active payment rules.Priorities can be from **1** to **10**, with **1** being the lowest priority and **10** being the highest priority. In general, rules with a higher number of conditions should be assigned a higher priority, especially if there are matching conditions in both rules, to ensure that the most detailed rule is applied. For more details, see [Base and Conditional Rules](base-and-conditional-rules.md).
- **Date Range**: In the **Start Date** fields, enter the date and time when this rule will become active. In the **End Dates** fields, you can either select **Run Indefinitely** to have no end date, or you can enter the date and time that the rule will expire. You can set dates to coordinate with specific campaigns so as to turn them on when a campaign begins, or to turn them off when a campaign ends.
- **Pricing Type**: Choose one of the **Pricing Type** options from the dropdown:
  - **Revenue share**: Indicate the percentage of network revenue that you will give to the publisher.
  - **CPM**: Indicate the dollar amount that you will give to the publisher when a creative is served (as a CPM amount). Also, you can indicate that you will pay this amount even when a default creative is served by clicking the checkbox for **CPM payment should be applied when a default is served**.

### Setting targeting

#### Frequency

You may apply payment rules based on the frequency and recency with which a user sees the publisher's placements. You can cap the frequency by day or over the payment rule's lifetime, and you can cap recency (the amount of time between each view) by minutes, hours, or days. You may also apply browser session frequency caps. For more information, see [Frequency and Recency Caps](frequency-and-recency-caps.md).

#### Geography

You may target by Country, Region, Metro Code, City, or Zip Code. Learn more about each of these options below.

> [!WARNING]
> Depending upon which geographic targeting options you choose, you may significantly reduce the likelihood of matching an impression. For more information, see [Geographic Targeting and Boolean Logic](#geographic-targeting-and-boolean-logic) below.

##### Accuracy of geographic targeting by IP address

Users of geographic targeting should expect some degree of inaccuracy; though targeting by country is highly accurate, the more specific the targeting, the more imprecise the results. This is especially true when targeting locations as granular as cities, metro codes, and zip codes.

Microsoft Advertising uses the IP lookup service provided by [Digital Envoy](https://www.digitalelement.com/geolocation/). For more information, [contact Digital Envoy directly](http://www.digitalelement.com/contact-us/).

##### Geographic targeting and boolean logic

When more than one targeting type is selected (e.g. both **Region** and **Zip Code**), the set of matching impressions is reduced, sometimes significantly. For example, if both the Boston MA-Manchester NH **Metro Code** and the **City** of Manchester, NH are selected, only users who are located in both will be targeted. Therefore, users in the **City** of Boston will not be included at all.

Another example: if both the California **Region** and Chicago, IL **Metro Code** are selected, then NO users will be targeted since the Chicago metro code does not overlap with California.

For more information about Boolean Logic, see [Segment Targeting](segment-targeting.md).

##### Country

You may **Include all countries**, **Include United States only**, or choose to include or exclude specific countries. Choose from the list of countries in the **Available List** area to the left, and click **Add** to add them to the **Chosen List**.

##### Region

**Region** is a more granular target than **Country**. Generally speaking, regions are based upon whatever method the country in question uses to divide itself into parts. For example, regions within the United States are states. Canada is divided into its provinces, and India is divided into its states and union territories. You may include or exclude regions by choosing from the **Available Regions** list on the left for addition to the **Targeted Regions** on the right.

##### Metro codes

**Metro codes** are smaller than regions; are only available for US inventory. Available metro codes range from large cities such as New York, NY and Chicago, IL, to smaller cities such as Rochester, NY, Birmingham, AL, and Pittsburgh, PA. You may include or exclude metro codes by choosing from the **Available List** on the left for addition to the **Chosen List** on the right.

##### City

A **City** is different than a **Metro Code**. It may be larger or smaller, depending upon your selection. Unlike metro codes, cities are not limited to US inventory. Cities from all around the world are represented, ranging from Tel Aviv, Israel to Kuala Lumpur, Malaysia. You may include or exclude cities by choosing from the **Available Cities** list on the left for addition to the **Targeted Cities** list on the right.

##### Zip code

Unlike the other settings listed here, targeting by **Zip Code** is include-only. Exclude certain zip codes by entering only those you want to target. Like metro codes, zip codes only apply to US inventory. You may enter lists of 5-digit zip codes in the **Zip Codes** text area in one of the following formats:

- Comma-separated
- Newline-separated

For more information about common formatting errors, see the [Zip Code Formatting Errors](#zip-code-formatting-errors) section.

###### Enter zip codes

You may paste up to 4000 zip codes into the text area. As noted above, it accepts lists of zip codes using several different delimiters. Press **Validate**, and the system will verify that your zip codes are formatted correctly. For more information about what to do if the system detects a formatting error, see the [Zip Code Formatting Errors](#zip-code-formatting-errors) section.

###### Zip code formatting errors

If your list of zip codes is formatted incorrectly, you will be presented with an error message and given the chance to edit and resubmit your zip codes. Those zip codes that failed the formatting validation will be listed above the line marked "See Errors Above" inside the text area. If you hover over the help bubble to the right of the text area, you will be presented with a list of the most common errors:

- **Excel-Truncated Zeros**: Excel may truncate leading zeros from zip codes when copy-pasting, e.g. '06514' becomes '6514'. To prevent this from happening, set the cell formatting of your spreadsheet to **Zip Code** under the **Numbers** header of the **Format Cells** dialog. For more details, see the [Excel Zip Code Formatting](#excel-zip-code-formatting) section.

- **Postal Codes, Zip+4**: Only 5-digit numeric US zip codes are accepted, e.g. '12804'.

- **Colons in Ranges**: Use hyphens rather than colons to denote ranges, e.g. '10001-10010'.

- **Descending Ranges**: Descending ranges of zip codes are not supported. Use ascending ranges instead, e.g. '12561-12804'.

###### Excel zip code formatting

Under the Number tab of the **Format Cells** dialog, select a **Category** of **Special** and a **Type** of **Zip Code**.

#### Size

You may create different publisher rules based on the size of the placement (standard or unique).

#### Placements

You may include or exclude particular placements from being covered by the payment rule.

> [!TIP]
> You can associate a placement group or individual placements with a payment rule. Select the placement group to see an expanded list of individual placements.

#### Demand filtering

Demand filtering can be a useful targeting capability, but it’s important to understand how it works before using it in payment rules or placements.

##### Key considerations #####

1. Applies only to managed demand: Demand filtering in payment rules or placements applies only to managed demand. If a placement is enabled for reselling, campaigns from third-party demand sources are not affected by demand filtering.
2. One payment rule applies per impression: Each impression uses a single payment rule, which is selected at the start of the auction. Once selected, the payment rule determines which demand is eligible to participate.
Because of this behavior, you can’t use payment rule demand filtering to adjust publisher payouts based on which demand source wins the auction. Specifically:
  - Including a line item: 
    If a payment rule _includes_ a specific line item, that line item is excluded from the auction when the payment rule is applied. Only other managed line items are eligible     to serve. For example, if you include line item `1234`, line item `1234` will not be eligible to bid when this payment rule is selected.
  - Excluding a line item:
    If a payment rule _excludes_ a specific line item, only that line item is eligible to bid from managed demand. All other managed line items are excluded, while RTB demand      remains eligible. For example, if you exclude line item `1234`, only line item `1234` can bid from managed demand when this payment rule is selected. If that line item         reaches its frequency cap, is pacing, or is otherwise ineligible, no managed demand will be able to serve as long as the payment rule remains selected.
3. Placement-level filtering takes precedence: Demand filtering configured at the placement level overrides demand filtering set at the payment rule level. If a placement includes demand inclusions or exclusions, all payment rule–level demand filtering is ignored. For more information, see [Placement demand filtering](https://learn.microsoft.com/xandr/monetize/create-a-placement#step-7-apply-advanced-settings-to-your-placement-optional).

## Step 3. Edit base or conditional rules (Optional)

You may edit your base or conditional rules at any time in the **Payment Rules** section located within the **Publishers** tab.

## Related topics

- [Working with Payment Rules](working-with-payment-rules.md)
- [Update Payment Rules](update-payment-rules.md)
- [Base and Conditional Rules](base-and-conditional-rules.md)
