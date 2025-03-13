---
title: Microsoft Monetize - Offline Conversion Attribution
description: Explore Offline conversion attribution, shifting data processing for tracking to a centralized warehouse, streamlining insights.
ms.date: 10/28/2023
---

# Microsoft Monetize - Offline conversion attribution

"Offline" attribution is [conversion attribution](conversion-attribution.md) that involves pushing all of the data processing required for conversion attribution "offline" to the Microsoft Advertising data warehouse.

Offline attribution provides:

- **Scalability**: First and foremost, performing conversion attribution at scale is a hard problem. Attributing conversions requires sorting through immense amounts of data, very quickly, in order to find a salient conversion event. Doing so efficiently is challenging. Offline attribution removes a number of steps from the attribution process, as well as removing components of our data processing infrastructure that did not scale well.
- **Accuracy**: Offline attribution more accurately implements the "last-view/last-click" attribution model. In particular, it more accurately attributes conversions when the elapsed time between the conversion pixel firing and a view or click is very short. It also tracks conversions for impression trackers, whereas the previous design did not. For more information about the "last-view/last-click" attribution model that we use, see [Conversion Attribution](conversion-attribution.md).
- **Flexibility**: This architecture provides us with more flexibility in how we implement conversion attribution models. As such, this change prepares our system to handle additional attribution models beyond "last-view/last-click."

  > [!IMPORTANT]
  > The below text and diagrams describe lower-level infrastructural details; for a higher-level overview of how we do conversion attribution, see [Conversion Attribution](conversion-attribution.md).

## Conversion attribution, "online" vs. "offline"

The following diagram shows the major components involved in the conversion attribution process, as well as the steps that occur between a user converting and that conversion being attributed and made available in reporting. The left side of the diagram shows the previous "online" conversion attribution process. The right side of the diagram shows the current "offline" process.

:::image type="content" source="media/oca.png" alt-text= "Diagram that defines the previous online conversion attribution process on your left side and the current offline process is on your right.":::

## Previous method ("online")

### Step 1. Conversion pixel loads

The user's browser loads the conversion landing page, which fires the conversion pixel hosted by the **Impression Bus**.

### Step 2. User data is requested by the impression bus

The **Impression Bus** asks the **User Data** store for information on the user.

### Step 3. User data is returned to the impression bus

The **User Data** store responds to the **Impression Bus** with information about the user.

Because of the nature of the design of the data store, and the speed with which it must respond to requests, the information about the user it can pass to the **Impression Bus** in this step is limited. It is also unable to receive information about views or clicks as quickly as it must respond to requests for the latest view and click information. As a result, the information can be slightly out of date - where "slightly" is measured in seconds - leading to less accuracy in attributing conversions.

### Step 4. User data is passed to Microsoft Advertising's bidder

The **Impression Bus** passes along the information about the user it received from the **User Data** store to **Microsoft Advertising's Bidder** for attribution.

### Step 5. Attribution is performed by **Microsoft Advertising's bidder**

**Microsoft Advertising's Bidder** performs the actual [conversion attribution](conversion-attribution.md), searching the user's data for the most recent view or click associated with the advertiser's creative.

### Step 6. User data is passed to the Data Warehouse for additional processing

**Microsoft Advertising's Bidder** has attributed the conversion, and passes that information along to the **Data Warehouse**, along with the information it was given by the **Impression Bus** and **User Data** store.

As noted in Step 3, the user information the **User Data** store can provide is limited. That limited set of data on the user must now go through a lengthy post-processing step, whereby it is combined with the more comprehensive user data stored in the **Data Warehouse**.

### Step 7. Conversion-related data is made available for reporting, optimization, and budget

The **Data Warehouse** has finished post-processing the limited amount of information on the converted user passed along from the **User Data** storage and integrating it with its own, more comprehensive data. At this point, the conversion-related data is made available to the Microsoft Advertising Platform for reporting, optimization, and budget purposes.

## Current method ("Offline")

### Step 1. Conversion pixel loads in current method

The user's browser loads the conversion landing page, which fires the conversion pixel hosted by the **Impression Bus**.

### Step 2. Impression-level data is sent to the Data Warehouse

The **Impression Bus** passes along the data it has about the impression and the user to the **Data Warehouse**.

### Step 3. Conversion is attributed, other data is processed

The **Data Warehouse** receives information about the impression and the user from the **Impression Bus**. As you can see from the diagram, the **User Data** store is now located within the **Data Warehouse**. This allows for faster integration and processing of the data provided by the **Impression Bus**.

### Step 4. Conversion-related data is made available for reporting, optimization, and budget

The **Data Warehouse** has finished processing and integrating the information on the impression and the converted user passed along from the **Impression Bus**. At this point, the impression and conversion-related data is made available to the Microsoft Advertising Platform for reporting, optimization, and budget purposes.

### Related topics

- [Conversion Attribution](conversion-attribution.md)
- [Working with Conversion Pixels](working-with-conversion-pixels.md)
- [Availability of Reporting Data](availability-of-reporting-data.md)
