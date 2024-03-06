---
title: Microsoft Monetize - Set Up Segment Targeting on a Line Item
description: Explore setting up segment targeting for precise ad campaigns, defining and targeting specific audience segments from various sources.
ms.date: 10/28/2023
---

# Microsoft Monetize - Set up segment targeting on a line item

You can set up a line item to target segments that you've created, as well as segments from third-party data providers.

For more information, see [Segment Targeting](segment-targeting.md).

1. Go to the **Audience & Location Targeting** \> **Audience & Location Segments** subsection within the **Create New Line Item** screen or **Edit Line Item** screen.

   The **Audience & Location Segments** subsection displays all segments belonging to the advertiser for the associated line item as well as segments defined at the Network level.

1. Click one of the following tabs:
    - **My Audience Segments**
    - **Third Party Segments**
1. To target users within one segment group, do the following:

   1. Drag the appropriate segments that display on the left into Segment Group 1 on the right.

      By default, the corresponding ✓ icon will be automatically  selected for every segment after dragging each one. You can leave the ✓ icon selected to target the users within the segment. Otherwise, click the **-** icon to exclude the users within the segment from being targeted.

   1. Select **And** or **Or** to add boolean operators between the segments.

      If you target multiple segments, the following will occur depending upon the boolean operator that you select:

      - Selecting **And** will automatically add an AND boolean operator between segments, which means that users must be in all the segments to be targeted.
      - Selecting **Or** will  automatically add an OR boolean operator between segments, which means that users can be in any one of the segments to be targeted.

1. To target users within multiple segment groups, do the following:

   1. Drag the appropriate segments that display on the left into Segment Group 1 on the right.

   1. Click **Create New Group** to add more segment groups and drag the appropriate segments into each corresponding segment group.

      By default, the corresponding ✓ icon will be automatically selected for every segment after dragging each one. You can leave the ✓ icon selected to target the users within the segment. Otherwise, click the - icon to exclude the users within the segment from being targeted.

   1. Select **And** or **Or** to add boolean operators between the segments and segment groups.

      If you are targeting multiple segment groups, the following will occur depending upon the boolean operator that you select:

    - Selecting **And** will automatically add an AND boolean operator between the segments within each segment group, but an OR boolean operator will be
    added between the segment groups. To be targeted, users only have to belong to at least one segment group, not all of the specified segment groups.
    - Selecting **Or** will automatically add an OR boolean operator between the segments within each segment group, but an AND boolean operator will be added between the segment groups. To be targeted, users must belong to all of the specified segment groups.

    There are many ways in which you can use multiple segment groups to target users. Let's say you have four segments: A, B, C, and D. A and B are "good" segments that you want to use for remarketing. Users only have to be in either segment A or segment B, not both, to be targeted. C and D are "bad" segments and include users that you
    aren't interested in being targeted.

    In this example, you would have segments A and B grouped within one segment group as well as a second segment group for segment C and a third segment group for segment D. Your goal is to exclude users that are in segment C and segment D.

    A boolean expression for this scenario would look something like this: (Require A OR Require B) AND (Exclude C) AND (Exclude D).

1. **Optional:** To further refine your segment targeting, hover over any of the segments and click the pencil icon:

   | Setting | Description |
   |---|---|
   | **Fired** | Retargets a subset of users within a segment pixel based on the time that they last visited a particular creative. For example, if you want to retarget a subset of users within a segment pixel who visited a product page in the last 24 hours, you can select **Between** from the **Fired** pull-down menu and enter a time period between 0 and 24 hours. |
   | **Value** | Refines the targeting criteria for a particular segment. For example, if you want to target a subset of users within a segment who have a household income that exceeds $200,000 USD and visited a product page containing different products, you would select **Above** from the **Value** pull-down menu and enter $200,000 USD in the text field.<br>Similarly, if you want to target a subset of users who have a household income between $100,000 USD and $200,000 USD, select **Between** in the **Value** pull-down menu and enter $99,999 USD in the **Greater than** field and $199,999 USD in the **Less than** field. |

   > [!NOTE]
   > The options that are available from the **Fired** and **Value** menus may vary based on the data provider's offering. Microsoft Advertising has only defined these options for segments that you've created.

1. Click **Save**.

## Related topics

- [Create a Segment Pixel](create-a-segment-pixel.md)
- [Associate Segment Pixels with Creatives](associate-segment-pixels-with-creatives.md)
- [Mobile User Segment Targeting](mobile-user-segment-targeting.md)
