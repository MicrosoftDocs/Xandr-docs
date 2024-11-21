---
title: Microsoft Curate - Geo Radius Segments
description: Learn how you can use geo radius segments for geographical targeting of multiple user locations in this page.
ms.date: 11/14/2023
---

# Microsoft Curate - Geo Radius Segments

A geo radius segment is a list of latitude, longitude, and radius data. You can use geo radius segments for geographical targeting of multiple user locations. When you create a geo radius segment, you add latitude, longitude, and radius data either manually (copy and paste) or by importing a file. Once the geo radius segment is created, these locations are easily targetable on your line item using the segment ID (see [Segment Targeting](segment-targeting.md)) for more information.

> [!IMPORTANT]
> Approximately 30% of impressions received contain location data that you can target with geo radius segments.
> [!NOTE]
> There is a maximum limit of 10k geo radius segments per member.

## Creating a Geo Radius Segment

There are five steps to creating a geo radius segment:

### Step 1. Get started

Open the [Location Manager](location-manager.md) page and select **New** to open the **Create Geo Radius Segment** dialog.

### Step 2. Create a new Geo Radius Segment

Fill in the following fields:

| Name | Description | Required/Optional |
|--|--|--|
| **Code** | User-defined code for calling the geo radius segment, e.g. GEO123 | Optional |
| **Description** | Description of geo radius segment | Optional |
| **Name** | Name for geo radius segment | Required |

Select **Next**.

### Step 3. Choose the method to add Geo Radius Segment features

**Copy and paste**

1. Enter the following information, separated by commas:
    - Latitude

    - Longitude

    - Radius (in meters: 3m to 100000m)

      > [!NOTE]
      > The radius needs to be a whole number.

    - Name (optional name for this feature)

      Separate each group by entering a hard return. For example:

      ``` 
      40.741624,-73.990991,10,Feature One  
      48.376928,-54.986546,8  
      ```

1. Select **Validate Input Formatting** to ensure that the information is in the correct format. If the information is in the correct format, the **Next** button is enabled.
1. Select **Next**.

**Import from file**

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

1. Select **Next**.

### Step 4. Review Geo Radius Segment features and create Geo Radius Segment

Review the **Related Geo Features** of the geo radius segment. Select **Create Geo Radius Segment** to finish creating the geo radius segment.

### Step 5. Note the segment ID for use in line item targeting

When a new geo radius segment is created, it is automatically assigned a segment ID. Use this segment ID (or the geo radius segment name) to locate the segments when configuring targeting for line items. See [Segment Targeting](segment-targeting.md) for more information on using the segment IDs assigned to geo radius segments for targeting.

> [!NOTE]
> Within 365 days of being created, geo radius segments must be refreshed or updated since their maximum Time-To-Live (TTL) is 365 days. If a segment is not refreshed, it will become inactive and unusable for targeting. You can refresh segments by adding new or existing latitudes and longitudes.
