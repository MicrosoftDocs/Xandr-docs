---
title: Working with Third-Party Buying Filters
description: Explore third-party filters, manage budgets, strategically select sites—essential for buyers with limited resources.
ms.date: 10/28/2023
---

# Working with third-party buying filters

There are literally billions of chances for buyers to purchase impressions every single day. However, this is never done; buyers have finite budgets and must choose the web sites on which they want their ads to run with great care. In addition to campaign-specific specifications, buyers can also create filters that govern all of their campaigns. These filters cover two areas:

- Including or excluding specific domain lists
- Including specific countries

You can create these filters in Microsoft Monetize by going to the menu location **Network** \> **Tools** \> **General**. Select the **3rd-Party Buying Filters** tab.

> [!NOTE]
> These settings affect third-party inventory only. They have no impact on managed inventory.

## Manage your third-party buying filters

This **3rd-Party Buying Filters** screen shows the two areas in which you can apply member-wide filters. To reach this screen, select **Network** > **Tools** > **General** on the top menu and then select the **3rd-Party Buying Filters** tab.

### Targeting: Geography

This section allows you to establish a list of countries that you can choose from when targeting a specific campaign.

- **Search:** You can enter a text string in this field (to the right of the magnifying glass symbol) to locate a country in the **Available List**. As you type, countries matching the entered text appear in the field.
- **Available List:** This section contains the countries that you have not yet selected.
- **Chosen List:** This section contains the countries that you have selected. Only these countries will be available for campaign targeting by geography (refer to [Geography Targeting](geography-targeting.md) for more information).

### Inventory: Domain lists

This section allows you to determine targeting using domain lists.

- **Search:** You can enter a text string in this field (to the right of  the magnifying glass symbol) to locate a country in the Available Domains List.
- **Available Domain Lists:** This section contains the lists that you have not yet selected.
- **Chosen Domain Lists:** This section contains the lists that you have selected. Depending on your selection for the **Include/Exclude  specific list of domains** (above), the domains in these lists will either be restricted from bidding, or will be the only domains in which you can bid.

## Limit the countries that you can target

The first section of the **3rd-Party Buying Filters** section allow the creation of a list of countries. These countries will be the only locations in which your campaigns will be able to purchase third-party impressions. This allows you to be more efficient when creating campaigns because you will have a smaller list of countries from which to define geographic targeting.

### Step 1. Open the targeting: Geography section

Click the arrow to the left of the **Targeting: Geography** header. The section opens to allow for editing.

Prior to opening this section, the countries which have already been included for this member are visible. This information is visible below the title of the collapsed section.

### Step 2. Choose the countries to add or remove from targeting

You can move countries between the **Available List** and the **Chosen List** to include or exclude them from targeting. Countries that appear in the **Chosen List** are eligible for third-party targeting when creating a campaign. Countries that appear in the **Available List** cannot be selected when creating a campaign.

#### To move countries to the Chosen List

A country must be highlighted in the **Available List** before you can move it to the **Chosen List**. There are several ways to highlight and move countries:

- Click on the desired country or countries select the **Add** button at the bottom of the list. All highlighted countries move to the **Chosen List**.
- Type the country name in the search field (to the right of the magnifying glass symbol). The list shows only those countries that match your search criteria. Highlight the desired countries and click the **Add** button at the bottom of the list. All highlighted countries move to the **Chosen List**.
- Click the **Select all** option at the top right of the list. Click the **Add** button at the bottom of the list to move them all to the **Chosen List**.

#### To move countries to the Available List

A country must be highlighted in the **Chosen List** before you can move it to the **Available List**. The options for highlighting and moving countries to this list are the same as moving them to the **Chosen List** (with the exception that all movement is in the reverse direction).

### Step 3. Save your settings

Click the **Save** button at the bottom left of the screen when you have finished making changes to the **Targeting: Geography** settings.

> [!IMPORTANT]
> Saving the **Targeting: Geography** settings does not preclude you from making changes to the **Inventory: Domain List** settings.

## Limit the Domain Lists that you can target

The second section of the **3rd Party Buying Filters** screen allows you to choose which domain lists you will use, either inclusively or exclusively.

### Step 1. Open the Inventory: Domain Lists section

Click the arrow to the left of the **Targeting: Geography** header. The section opens to allow for editing.

> [!IMPORTANT]
> This section shows the domain lists which have already been included for this member prior to opening it. These are located to the right of the **Include** text in the second row of the collapsed section.

### Step 2. Indicate whether to specify domain lists or not

This option allows you to choose one or more domain lists at the network level, thereby filtering the websites they contain prior to use for targeting at the campaign level. This is beneficial if you know that you regularly include or exclude one or more domains. You must choose one of the following options:

- **Option 1 - Include all domains:** Select this option to keep all domain lists available for targeting at the campaign level. You would select this if you do not have any "across-the-board" inclusions or exclusions and want all domain lists available when you specify campaign-level targeting.

- **Option 2 - Include/Exclude specific list of domains:** Select this option to specify network-wide inclusions and exclusions by domain list. When you select this option, you are presented with all domain lists in the **Available Domain Lists** field. You must move the desired domain lists into the **Targeted Domain Lists** field and determine whether to **Include** or **Exclude** them.

- **Option 3 - Exclude:** Choose this option to ensure that this domain list will **not** be available for targeting at the campaign level once you move it to the **Targeted Domain List**. This means that you will not be able to use it at the campaign level. However, this makes all other domains included by default.

- **Option 4 - Include:** Inclusion at the network level restricts the **domains** that are available to be targeted at the campaign level. At the campaign level, you can include additional domain lists, even though they were not included at the network level. However, if those domain lists contain domains which are not part of the domain lists included at the network level, those domains will not be targeted.

#### Common use cases

1. If you have domains that you wish to exclude from seeing impressions (a network wide blocklist), you should exclude the blocked domain list at the network level. This way, no campaigns will serve on the domains in this list since all blocked domains will be filtered out prior to applying the campaign level domain lists.
1. If you have domains on which you always want to serve impressions (a network wide allowlist), you should include the allowed domain lists at the network level. This way, your campaigns will never serve on domains that have not been included in the allowlist since these domains will be filtered out prior to applying the campaign level domain lists.
1. If you do not have a network wide blocklist or allowlist, then you should not use network level settings.

#### Example

- You include two domain lists at the network level: **DLA** and **DLB**.
  - **DLA** contains domains **AAA.com**, **BBB.com**, **CCC.com**, and **DDD.com**.
  - **DLB** contains domains **111.com**, **222.com**, **333.com**, and **444.com**.
- These two domain lists and the eight domains pass through to the campaign level. At that time you can include or exclude either domain list on a campaign-by-campaign basis. In this example, we will include both at the campaign level.
- At the campaign level, you include domain list **DLA1**.
  - This domain lists contains the following domains: **AAA.com**, **CCC.com**, **222.com**, **777.com**, and **999.com**
- **DLA1** will be included with the campaign. Domains **AAA.com**, **CCC.com**, and **222.com** will be targeted, because they are contained within at least one of the domain lists included at the domain level (**DLA** and **DLB**). However, domains **777.com** and **999.com** will **not** be targeted, as they are not contained with either of the two domain lists included at the network level.

> [!NOTE]
> Be sure to note the difference between a **domain** and a **domain list** in the descriptions above.

### Step 3. Choose the domain lists to add or remove from targeting

You can move domain lists between the **Available Domain Lists** and the **Targeted Domain Lists** fields to make them available for targeting or exclusion in a campaign. Domain lists that appear in the **Targeted Domain Lists** are eligible for targeting when creating a campaign. Domain lists that appear in the **Available Domains List** cannot be selected when creating a campaign.

#### To move countries to the Targeted Domain List

- Click the **Add** button at the bottom of the list. All highlighted countries move to the **Targeted Domains List**.
- Type the country name in the search field (to the right of the magnifying glass symbol). The list shows only those countries that match your search criteria. Highlight the desired countries and click the **Add** button at the bottom of the list. All highlighted countries move to the **Targeted Domains List**.
- Click the **Select all** option at the top right of the list. Click the **Add** button at the bottom of the list to move them all to the **Chosen Domains List**. Everything in the **Targeted Domain List** is available for use on the [Working with Targeting Lists](working-with-targeting-lists.md) screen.

#### To move countries to the Available Domains List

- Click on the desired country or countries to highlight them and click the **Remove** button at the bottom of the list. All highlighted countries move to the **Available Domains List**.
- Type the country name in the search field (to the right of the magnifying glass symbol). The list shows only those countries that match your search criteria. Highlight the desired countries and click the **Remove** button at the bottom of the list. All highlighted countries move to the **Available Domains List**.
- Click the **Select all** option at the top right of the list. Click the **Remove** button at the bottom of the list to move them all to the **Available Domains List**.

### Step 4. Save your settings

Click the **Save** button at the bottom left of the screen when you have finished making changes to the **Inventory: Domain List** settings.

> [!IMPORTANT]
> Saving these settings does not close the section. You can save and then make changes to the **Targeting: Geography** settings.

## Related topics

- [Geography Targeting](geography-targeting.md)
- [Working with Targeting Lists](working-with-targeting-lists.md)
