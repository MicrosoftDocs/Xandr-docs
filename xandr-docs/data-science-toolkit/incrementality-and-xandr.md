---
title: Data Science Toolkit - Incrementality and Xandr
description: In this page, learn what is incrementality and how Xandr offers clients with data science capabilities, like the ability to measure incrementality. 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-science-toolkit
ms.author: shsrinivasan
---


# Data Science Toolkit  - Incrementality and Xandr

## Measure incrementality

The basic idea behind measuring incrementality is to split users into test and control groups and only show ads to users in the test group. The goal is to see if the users in the test group spend more money on the advertiser's products than the users who were not exposed to ads.

:::image type="content" source="./media/datascience-d.png" alt-text="Screenshot showing how Incrementality is Measured.":::

### Control group testing options

There are several options for control group testing, each comes with varying costs and degrees of accuracy.

- **PSA Banners**  - One way to do this is to serve a PSA/Charity banner to the Control group, but this option requires spending a percentage of the campaign budget on advertising that will not drive any business results for you, or your advertiser.
- **Holdout Group**  - Another way is to arbitrarily create a first-party data audience group, which you will negatively target in your line item settings and use as your control group. Though not costing any money this option will likely not lead to very accurate results. Excluding the control group will prevent the return of any bid request information, such as domain or device, which means it might be difficult to ensure that your Test & Control Groups are statistically similar.
- **Ghost Bidding** - An improved approach is to not serve an ad to the user but log that we could have served an ad to them. Analysis can then be performed on the resulting data set. This is the best and the most accurate approach that will allow your Data Science team to design a clean test and does not require wasting a percentage of your budget on PSA Banners.

### Xandr ghost bidding and incrementality feed

Xandr offers clients with data science capabilities the ability to measure incrementality. We provide the mechanism in Invest to split an audience into a test group (the group exposed to ads) and a control group (the group not exposed to ads). The test uses the same targeting and bidding approach for each group. This enables advertisers t analyze the revenue driven by users from each group to determine incremental lift from users exposed to ads. We provide the necessary data in a Log-Level Incrementality feed that logs DSP auctions won by each of the audience groups. In the case of the control groups, the “winning” bid is pulled from the auction so that the audience is not exposed to the ad. The feed contains one row per impression.

## Audience segmentation

You can split your target audience into a test and control group by one of two methods:

### Randomized by Xandr

This is the default method. Xandr splits the target audience into test and control groups based on the settings you placed in the Incrementality section of the Line Item setup in Invest. Those settings will include a custom key that you set up which will enable Xandr to create unique user segments for the test and control groups in a deterministic way. For a unique key, the audience will be distributed uniquely into test and control groups. This enables you to portion audiences differently for different tests. To have the same user segmentation on different line items simply use the same unique key.  The other setting is a percentage that will determine the number of users that will be included in the control group.  

> [!NOTE]
> Setting the same key on different line items means that the same test and control groups will be used for these line items.

### Set up a line item for incrementality

1. Go to  **Line Item \> Basic Setup \> Incrementality** and select **“Use control group”**.
1. Assign a key and a percentage of users to assign to the control group.
    - A key can be any string of characters and creates unique User Segmentation between Test & Control Groups. You can set the same key across multiple line items to ensure that they all have use the same user segmentation - this will help ensure no cross-contamination across line items. See more below.
    - Control Group Percentage will determine the percentage of users that you target that fall in the Control Group.

### Client-controlled

You can also choose to create your own grouping of test and control users using a pre-created segment. This is a single segment that determines test or control using the segment's `value` field.

> [!NOTE]
> This option is only available through the Xandr API.

**The following values can be used**:

- Set the value to `0`  to create a test group that will be served ads as usual.
- Set the value to `1` or any non-zero value to create a control group. This segment setting will create a row in the Incrementality feed and then skip to the next result.

For additional information on working with Segment Values see [Batch Segment Service](../bidders/bss-avro-file-format.md).

**Why custom groupings are beneficial?**

- You have your own subset of the Xandr total audience pool and want to have more oversight into how the test and control groups are split.
- You have insights about how Xandr cookie IDs map to individual consumers. If Xandr is unaware of this mapping when determining which users end up in test/control, we will contaminate your measurement with cookies that cross from test/control that should be aligned to a mapped consumer.

## Considerations for planning incrementality tests

### Begin with a well-framed hypothesis

Ensure you are starting with a well-framed hypothesis. The testing of incrementality should be done to answer a hypothesis on incremental lift for a specific campaign. A hypothesis that is too general will not provide adequate test results and not enable you to have actionable responses to those results.  

### Minimize contamination

Contamination can be defined as a situation where users in the control group are unintentionally exposed to advertising. Minimizing contamination is crucial for a clean test. When you are designing your test, consider the following to help minimize contamination:

### Ensure control group is not exposed to external buyers or DSPs running a similar campaign

It is important to ensure that users that are assigned to the control group in our platform are not exposed to ads from external buyers, or other DSPs running the same campaign.

**How to mitigate?**

- The ideal scenario is to ensure that Xandr is the only DSP running a particular campaign. It is important to think about this during your test planning and control group setup.
- If it is not possible to isolate users in the control group then consider geofencing your campaign. To do this, run your campaign exclusively on Xandr in certain geographical locations, while other buyers/DSPs on the plan target a different region. For example, if the campaign is to run in the United States, give Xandr exclusivity in certain states and have other buyers/DSPs run in the remaining states.
  - **How to determine which geolocations to ring-fence to ensure no bias in the test?**  
    In the above example, the recommendation would be to select a list of states that have similar Conversion Rates as the United States in general. This should make the results of the lift test representative of the United States as a whole.

### The campaign may run on other channels

It is likely that the marketing budget for a campaign will not be isolated to programmatic activity and there will be other channels, such as television, radio, search, or others being utilized for the particular campaign. In this situation, incrementality is the measurement of the impact for the campaign you are testing, in the context of all related advertising. The resulting lift will be smaller but your analysis will present a real-world measurement.

**How to mitigate?**

Ensure that the "background" advertising is the same for the test and control groups.

### Line item cross-contamination

If your campaign has multiple line items, for example, one for prospecting and another for retargeting, it is important to ensure that there is no cross-contamination between them.

**How to mitigate?**

Setting the same key across all of your line items in the test will ensure that they all use the same user segmentation, making it impossible for one line item to target control group users from a different line item.

### Users on multiple devices

It is important to note that the default, randomized user segmentation does not account for multiple devices. This means that the same user can be both in a test and a control group depending on which device they are using.

**How to mitigate?**

- If you are able to build a cross-device graph using first-party data, then you can upload your own user segmentation via the API.
- Apply your own cross-device graph retrospectively, when cleaning up the data.
- You can also limit the test to just one device type and assume that one person would typically only own one device of the same type. This is the most intrusive way and will likely have an impact on campaign performance.

### Effectively compare test and control groups

In ghost bidding, the randomization of users into test and control groups, either by the client or by Xandr, happens offline before bids are submitted. This means that not all of the test users will be exposed to an ad and the portion of users exposed to an ad in the test group are subject to a win bias.

The test group can now be thought of as being split into two subsets, exposed and not exposed to an ad. The table below provides a means of categorizing the three groups.

| User Group | Description |
|--|--|
| Control Group (Not Exposed) | Users you see in the Incrementality Feed with `is_control = 1` (you would never see these users in the Standard Feed, as we pull our bids and never actually want to transact those impressions). |
| Test Group (Exposed) | Users you see in the Incrementality Feed with `is_control = 0`, who are also in the Standard Feed. |
| Test Group (Not Exposed) | Users you see in the Incrementality Feed with `is_control = 0`, who do not appear in the Standard Feed. They are not in the Standard Feed because we have not transacted any imps with them.  We did not end up winning the bid somewhere down the line in an auction. This could be for a variety of reasons such as a buyer using a different DSP won it. |

> [!NOTE]
> Because they likely are not statistically similar you cannot just compare:
>
> - Test Group (Exposed) vs Control Group (Not Exposed).
> - Test Group (Exposed) vs Control Group + Test Group (Not Exposed).

For example, it is likely that a user in the Test Group (Not Exposed) might be highly valuable to other buyers. This means that the win bias could produce a negative lift measurement if not considered carefully.

### Ensure that test and control groups you compare are statistically similar

We generally recommend doing the following to ensure that the Test & Control Groups that you are comparing are statistically similar. Keep in mind how you make your groups statistically similar will likely depend on your hypothesis, the goals you're trying to achieve, and your data science team's approach:

- Use historical data to identify features, which correlate highly with your desired outcomes, for example, you may have noted in the past that users on a certain device and on a certain domain are much more likely to convert on average.
- Take a subset of the exposed and unexposed users to create the test and control group that you will be comparing. Ensure a comparable distribution of users that have these important features across both the test and control groups.

### Control group nuances

As with test groups having some percentage of their users that will not be served ads, the same is true for members of the control group. The withdrawn bids could lose in the downstream auction. The Control Logs reflect which users could have won, rather than which would have won.

To estimate the number of impressions that the control group would have actually won, you might want to look at Win Rate for the test group.

> [!NOTE]
> Xandr logs winning bids in the internal auction, but there are instances where it is possible to win a final auction on price but lose on another metric set up by the publisher. This means that test users will have impressions that were won at lower ranks (not all auction_ids in the standard feed will be found in the incrementality_feed).

It might be helpful to review how an auction works for an Incrementality Line Item:

1. An ad slot in a web browser sends out a bid request.
   - Bid request is enriched with user and contextual data through ImpBus.
1. Bid request is sent to AppNexus Bidder and External Demand.
1. Bidder internal auction happens – all LI on console.
1. If the bid from a LI associated with an Incrementality Segment is the top auction rank then this impression is logged in the Incrementality Feed
    - If the user is in the Control group (1), the bid is pulled from the bid list
    - If the user is in the Test group (0), the bid continues as normal
1. Top ranked test bids are sent on to Imp Bus from Console, and External Bidders respond to Imp Bus.
1. Imp Bus applies seller ad quality rules and holds a final auction.
1. The ad is sent back to the web page
    - If this ad request is coming from external supply, then the winner is sent to an SSP where the true final auction happens
1. Ad sends back a render signal to Imp Bus.
1. Impression is logged in standard_feed.

### Think about statistical significance

Statistical significance is the likelihood that a relationship between two or more variables is caused by something other than chance. You use statistical significance to determine the plausibility of a null hypothesis. A null hypothesis assumes that any difference between the chosen characteristics that you see in a set of data is due to chance. Rejecting the null hypothesis presents a stronger case for your hypothesis.

It is important to think of the statistical significance levels that you are comfortable with ahead of the test. This will help you get an idea of how many impressions you need to serve and users to reach.

Use your historical data to determine, which features, such as domains or device types statistically correlate with high success rate (i.e. conversion rate).

These two formulas can help you determine the sample rate needed:

:::image type="content" source="./media/datascience-e.png" alt-text="Diagram of sample rate - 1.":::

:::image type="content" source="./media/datascience-f.png" alt-text="Diagram of sample rate - 2.":::

### Statistic test

Once you receive a metric such as a conversion rate for both the control and test groups, use either a T-test or a Z-test to determine whether the incrementality difference is statistically significant or not.  

Follow these steps to determine the incrementality difference:

1. Calculate the T-value.
1. Get the P-value for the T-value.
1. Compare the P-value to the predefined significance level α (typically set to 5%).

### Required sample size

The sample size required for acceptance/rejection of the null hypothesis for KPI such as the conversion rate or conversion number depends on the following parameters.

- The standard deviation of the outcome variable.
- Minimum detectable effect (the minimum difference between the KPIs of the test group and control group).
- Desired level of statical significance α.
- Desired power β.
- Type of the test: [one-tailed or two-tailed test](https://stats.oarc.ucla.edu/other/mult-pkg/faq/general/faq-what-are-the-differences-between-one-tailed-and-two-tailed-tests/).

### Set control group percentage

The control group percentage, whether it is set through the Line Item settings in Microsoft Invest or the platform's API, cannot exceed 20 percent.  We recommend a percentage between 10 and 20 for best results.

## Additional considerations

### Optimization behaviour

It is important to understand how optimization can behave differently between bidding for the test and control groups.

Since the control group users bids are pulled and they never served ads, [frequency and recency](../invest/frequency-and-recency-caps.md) measurements will always be different for them.  This means that the Cadence Modifier will behave differently between test and control groups. See the image below for an overview of how the Cadence Modifier impacts Bid Value.

:::image type="content" source="./media/datascience-g.png" alt-text="Diagram of how the Cadence Modifier impacts Bid Value.":::

**How to mitigate?**

- Use Custom Models to override the Cadence Modifier and set it to one. This will ensure the same bidding behavior for both test and control groups.
- Use a flat bid for your test and optimize manually.

> [!NOTE]
> These approaches can potentially impact your campaign performance.

### Excluded sellers

We are currently unable to run Incrementality Tests on **Verizon's** and **MoPub's**  inventory, so the following Seller Member IDs have to be excluded in Line Item's targeting:

| Seller Name | Seller ID |
|--|--|
| MoPub | 1813 |
| Verizon Media (O&O Display) | 273 |
| Verizon Media (O&O Video) | 11665 |
| Verizon Media Exchange | 11664 |
| Verizon Media Video Exchange | 3292 |
