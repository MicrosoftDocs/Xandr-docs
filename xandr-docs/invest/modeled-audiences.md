---
title: Modeled Audiences
description: In this article, learn about modeled audiences and how advertisers can take their first-party segments and expand them to similar users for targeting.
ms.date: 07/08/2024
---

# Modeled audiences

Modeled Audience is a new feature available for Microsoft Invest that allows advertisers to take their first-party segments and expand them to similar users for targeting. Modeled Audiences uses Microsoft first-party data and advanced machine learning techniques to create new audience segments with similar characteristics and behaviors as users in your first-party segments.

## Set up a modeled audience

1. In the Microsoft Invest UI, select the line item for your advertiser.
1. Select the **Edit** option, and then select the **Audience & Location Targeting** option on the left pane.
1. An **Audience and Location Segments** panel is displayed on the right side of the screen. Next, select **Create Modeled Audience** from the targeting model.
1. Select a **Seed Segment** from the drop-down menu.

    > [!NOTE]
    >
    > - Only eligible seed segments (first-party segment with over 7,000 daily active users) are displayed in the drop-down menu.
    > - If your seed segment meets these criteria but does not appear in the drop-down menu, the system might lack sufficient data for modeling. To ensure eligibility, it is recommended to run your seed segment in a campaign for at least seven days.

1. Select one of the **Segment Reach** options for the modeled segment:
    - **More Precise**: Includes approximately the top one-third (1/3) of the users in the modeled segment.
    - **Balanced**: Includes approximately the top two-thirds (2/3) of the users in the modeled segment.
    - **More Reach**: Includes all the users in the modeled segment.
1. Select **Save Modeled Segment** to save your modeled segment. The newly generated segment model will be available within the next 48-72 hours, along with its estimated size.

> [!NOTE]
> **Restrictions:**
>
> - A modeled audience can only be created and edited in the line item view.
> - Modeled audiences are not supported for data marketplace or third-party segments.
> - Only one segment can be used as the seed for a modeled audience.
> - The seed segment must be an advertiser-owned first-party segment.
> - The start date of the line items are used to determine when to start modeling.
