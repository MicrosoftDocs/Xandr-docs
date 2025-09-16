---
title: Modeled Audiences
description: Modeled Audiences is a new feature available for Microsoft Curate that allows curators to take their first-party segments and expand them to similar users for targeting.
ms.date: 09/16/2025
ms.author: shsrinivasan
---

# Modeled audiences

Modeled Audiences is a new feature available for Microsoft Curate that allows curators to take their first-party segments and expand them to similar users for targeting. Modeled Audiences uses Microsoft first-party data and advanced machine learning techniques to create new audience segments with similar characteristics and behaviors as users in your first-party segments. 

## Set up a modeled audience 
- In the Microsoft Curate user interface, select the **curated deal line item**. 
- Ensure at least one country is selected under the Geography targeting option. 
- Select the **Edit** option, and then select the **Segments** targeting option. 
- A **Segment Targeting** dialog is displayed. 
- Select **Create Modeled Audience**. 
- Select a **Seed Segment** from the drop-down menu. 
> [!NOTE]
> - Only eligible seed segments (first-party segments with over 7,000 daily active users) are displayed in the drop-down menu. 
> - If your seed segment meets these criteria but does not appear in the drop-down menu, the system might lack sufficient data for modeling. To ensure eligibility, it is recommended to run your seed segment on a curated deal for at least seven days. 
- Select one of the Segment Reach options for the modeled segment: 
    - **More Precise:** Includes approximately the top one-third (1/3) of the users in the modeled segment. 
    - **Balanced:** Includes approximately the top two-thirds (2/3) of the users in the modeled segment. 
    - **More Reach:** Includes all the users in the modeled segment.
- Select **Save Modeled Segment** to save your modeled segment. The newly generated segment model will be available within the next 48-72 hours, along with its estimated size.
> [!NOTE]
> - A modeled audience can only be created and edited in the curated deal line item view. 
> - The curated deal line item must be inclusively targeting at least one country for modeled segments to be processed. 
> - Modeled Audiences are not supported for Data Marketplace or third-party segments. The seed segment must be a first-party segment. 
> - Only one segment can be used as the seed for a modeled audience. 
> - The start date of the curated deal line items is used to determine when to start modeling. 
> - Seed segments must be composed of Xandr user IDs or MAIDs. Segments targeting URLs or IPs are not currently supported. 