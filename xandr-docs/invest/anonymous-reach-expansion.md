---
title: Microsoft Invest - Anonymous Reach Expansion
description: In this article, learn about daypart targeting and how you can target users based on the day and time when they see impressions.
ms.date: 11/04/2024
---

# Microsoft Invest - Anonymous Reach Expansion

You can target users based on the day and time when they see impressions. In the **Budgeting and Scheduling** section of an ALI, select the pencil icon next to **Daypart**.

By default, all days and times are targeted. On the **Daypart Targeting** dialog, you can narrow your targeting by drawing the blocks of time during which you want to reach users. Also, you can define whether targeting should be based on each user's timezone (as determined by the user's browser) or by a specific timezone, regardless of user.

> [!TIP]
> Once you've drawn a box, you can drag the lower right corner to adjust the width and height of the box to cover the days and times desired. Overlapping and adjacent daypart boxes will be merged automatically.

In the **Audience & Location Targeting** section of an ALI, there is a setting called **Anonymous Reach Expansion**.

By default this toggle is turned off, meaning the line item will not serve if the impression does not contain identifiers. Frequency capping will function normally in this case.

Turning this toggle on allows Microsoft to maximize your reach to users for whom we do not have any know identifiers. If frequency caps are set, modeling will be used to ensure the desire caps are respected.

> [!Note] If the line item has a CPA goal or a user-based audience segment, this setting will be ignored and only identified traffic will be allowed. 