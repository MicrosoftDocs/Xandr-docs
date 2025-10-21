---
title: Microsoft Monetize - Geo Radius Segments
description: The article introduces a geo radius segment, which is a collection of data including latitude, longitude, and radius information.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Geo radius segments

> [!NOTE]
> Access to the geo radius segment targeting feature requires additional roles and permissions. Contact your Microsoft Advertising account representative for more information.

A geo radius segment is a list of latitude, longitude, and radius data. You can use geo radius segments for geographical targeting of multiple user locations. When you create a geo radius segment, you add latitude, longitude, and radius data either manually (copy and paste) or by importing a file. Once the geo radius segment is created, these locations are easily targetable on your line item using the segment ID (see [Segment Targeting](segment-targeting.md) for more information).

> [!IMPORTANT]
> Approximately 30% of impressions received contain location data that you can target with geo radius segments.
> [!NOTE]
> There is a maximum limit of 10k geo radius segments per member.

## Creating a geo radius segment

There are five steps to creating a geo radius segment:

### Step 1. Get started

Open the [Location Manager](location-manager.md) page and click **New** to open the **Create Geo Radius Segment** dialog.

### Step 2. Create a new geo radius segment

Fill in the following fields:

| Name | Description | Required/Optional |
|--|--|--|
| **Name** | Name for geo radius segment | Required |
| **Code** | User-defined code for calling the geo radius segment, e.g. GEO123 | Optional |
| **Description** | Description of geo radius segment | Optional |

Click **Next**.

### Step 3. Choose the method to add geo radius segment features

### Copy and paste

 1. Enter the following information, separated by commas:

    - Latitude
    - Longitude
    - Radius (in meters: 3m to 100000m)

     > [!NOTE]
     >
     > The radius needs to be whole number.

     - Name (optional name for this feature)

      Separate each group by entering a hard return. For example:

       ```
       40.741624,-73.990991,10,Feature One  
       48.376928,-54.986546,8 
       ```

 1. Click **Validate Input Formatting** to ensure that the information is in the correct format. If the information is in the correct format, the **Next** button is enabled.

 1. Click **Next**.

### Import from file

1. Browse your computer and select the .csv file to upload. Ensure that the first row of the .csv file includes the following headers with corresponding values listed in rows underneath:

    ```
    lat | long | radius_meters | name 
    ```

    For example:

    ```
    lat,long,radius_meters,name  
    40.741624,-73.990991,10,Feature One  
    48.376928,-54.986546,8 
    ```

1. Click **Next**.

### Step 4. Review geo radius segment features and create geo radius segment

Review the **Related Geo Features** of the geo radius segment. Click **Create Geo Radius Segment** to finish creating the geo radius segment.

### Step 5. Note the segment ID for use in line item targeting

When a new geo radius segment is created, it is automatically assigned a segment ID. Use this segment ID (or the geo radius segment name) to locate the segments when configuring targeting for line items. See [Segment Targeting](segment-targeting.md) for more information on using the segment IDs assigned to geo radius segments for targeting.

> [!NOTE]
> Within 365 days of being created, geo radius segments must be refreshed or updated since their maximum Time-To-Live (TTL) is 365 days. If a segment is not refreshed, it will become inactive and unusable for targeting. You can refresh segments by adding new or existing latitudes and longitudes.
