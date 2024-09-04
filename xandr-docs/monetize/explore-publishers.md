---
title: Explore Publishers
description: Explore insights on network and publisher performance by summarizing the Publishers screen, revealing details for each associated publisher. 
ms.date: 10/28/2023
---

# Explore publishers

The **Publishers** screen lists the publishers with which your member is associated. In this list you can see information regarding network and publisher performance for each publisher. You can select individual publishers to display more information.

## Getting to the publisher screen

> [!NOTE]
> Depending on which version of Microsoft Monetize you use, you will access the **Publishers** screen using one of the following options.

From the **Publishers** tab: either select the **Publishers** option in the menu at the top of the screen, or select **All Publishers** from the **Publishers** dropdown.

From the **Inventory** tab: either select the **Inventory** option in the menu at the top of the screen, or select **Publishers** from the **Inventory** dropdown.

## Reviewing publisher performance

You can select the time period you want to review by clicking the date- selector above the table. You can choose to view data from **Today**, **Yesterday**, **Last 7 Days**, or **Lifetime**.

The following information about the activity of each publisher associated to your member is available in the **Publishers** table:

- **Name** - The name of the publisher.
- **ID** - The unique identification number of the publisher.
- **Placements** - The number of placements defined for the publisher. This information is displayed on a button; clicking this button will take you to the Inventory Manager for that publisher. (See [Explore Placements](explore-placements.md) for more on using the Inventory Manager.)
- **Currency** - The currency units being displayed for the publisher. The default is USD (United States  Dollar). You can change your settings to display all currency values, such as Revenue and Profit, in the local currency of each publisher. Note that as with all columns on this screen you can hide the Currency column from view. See Configuring Publisher Display below for information on configuring the currencies and columns that are displayed.
- **Network (member name)** -
  - **Revenue** - The total revenue for the network. This value includes the sum of booked and resold revenue.
  - **RPM** - The revenue per 1,000 impressions for the network. This value includes impressions from defaults, [Public Service Announcements](default-psas.md) and errors.
  - **Profit** - The dollar amount that this network has earned from this publisher.
  - **PPM** - The network profit per 1,000 impressions (Network RPM - Publisher RPM).
  - **Deal Revenue** - The total revenue from deals.
- **Publisher's Share**
  
  > [!IMPORTANT]
  > For publishers with an inventory relationship of **Owned & Operated**, **Publisher Revenue** and **RPM** will always be zero. The amount made on inventory is rolled up into the Network Revenue column, which represents the revenue earned by your Microsoft Advertising member seat.

- **Revenue** - The total revenue earned by this publisher. This value represents the network's cost.
- **RPM** - The revenue per 1,000 impressions for this publisher. This value includes impressions from defaults, PSAs, and errors. It represents your network's CPM.
- **Impressions**
  - **Imps** - The total number of impressions.
  - **Kept** - This value applies to managed accounts. It reflects the number of managed advertiser's creatives served on a managed publisher's site.
  - **Resold** - The number of impressions resold to a third-party buyer.
  - **Default** - The number of impressions where a [default creative](assign-a-default-creative-to-a-placement.md) served because there were no valid bids.
  - **PSA** - The number of impressions that showed PSAs. PSAs serve only when there is no other creative available.
- **Viewability**
  
   > [!IMPORTANT]
   > A viewable impression, as defined by the IAB (Interactive Advertising Bureau), is a display ad with 50% or more of the pixels visible for at least one continuous second. A video ad is defined as viewable if 50% or more of the pixels are visible for at least two consecutive seconds.

- **Viewable** - The percentage of impressions that were viewable, based on the total number of impressions that were measured for viewability.
  - **Measured** - The percentage of impressions measured for viewability, based on the total number of impressions.
  - **Clicks** - The total number of clicks on all impressions for this publisher.

## Configuring publisher display

Click the configuration button (in the upper right corner of the screen) to customize the display of your publisher list. Several display options are available.

### Column configuration

Configure which columns you'll see in the **Publishers** table. All columns are visible by default. Uncheck the category (**Network**, **Publisher**, **Impressions**, **Viewability**) to hide all columns within that category. Checking the category will restore all columns along with the category. Check and uncheck individual columns within categories depending on your view preferences.

### Currency display

Select whether to view currency units for each publisher in **USD: United States Dollar** or the **Local Currency** of the publisher. **Local currency** is determined by the currency settings for each publisher. Current exchange rates will be applied. Exchange rates are updated hourly. See [Currency Support](currency-support.md) for more information on currencies.

### Time zone display

Click the  dropdown to select a time zone. This will be the time zone that is used to determine the data collected for the specified time period (**Today**, **Yesterday**, or **Last 7 Days**).

## Filtering by publisher name/ID

You can limit the number of publishers visible on the screen by searching for a Publisher by name or ID. In the text box labeled ID/Name, enter either an ID or a name. The system will automatically begin searching for matches to whatever you type. For example, if you type 123, all publishers with IDs containing the numbers 123 (in that order) will be displayed. If you type Pub1, all publishers whose names begin with "Pub1" will be displayed.

To see all publishers (or, if you have used the search text box to filter your list, all publishers that match that search), select **All** from the state dropdown. To see only active publishers, select **Active**. To see only inactive publishers, select **Inactive**.

## Sorting the publisher list

You can sort the list of publishers on almost any column by clicking the column heading. Keep in mind that if your publisher list is long, sorting might take a little bit of time. The columns you can sort on are:

- **Name**
- **ID**
- **Network** category: All columns
- **Publisher's Share** category: **Revenue** column
- **Impressions** category: All columns
- **Viewability** category: All columns
- **Clicks**

> [!NOTE]
> When sorting on any column that displays values of currency, the sorting will always be done based on USD. This means that if you've chosen to display each publisher's local currency, the values might look out of order because of the exchange rates.

### Related topics

- [Working with Publishers](working-with-publishers.md)
- [Create a Publisher](create-a-publisher.md)
- [Update Publishers](update-publishers.md)
