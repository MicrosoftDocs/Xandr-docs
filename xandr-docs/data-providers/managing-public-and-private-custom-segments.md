---
title: Managing Public and Private (Custom) Segments
description: The Data Marketplace supports both public and private segments. This page covers creating a new segment object, a new private segment, changing a public segment to private and a private segment to public segment.   
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-providers
ms.author: shsrinivasan
---

# Managing public and private (custom) segments

The Data Marketplace supports both public and private segments. This means that any segment – whether public or private – used through the Data Marketplace is cleared and reported on by Xandr. Both the data provider and data buyer benefit from the operational savings of our clearing house and the detailed reporting of data usage. The purpose of this page is to provide best practices depending on the types of data you provide through the marketplace.

## Public segments

Public segments are segments that are immediately available to all data buyers in the Data Marketplace. These segments typically represent a data provider's standard offering. Xandr automatically shares this segment with all Data Marketplace buyers.

> [!IMPORTANT]
> For data providers to be visible to buyers, they must have at least one segment publicly mapped to their taxonomy.

## Create a new public segment

1. Create a new segment object using the [Segment Service](../digital-platform-api/segment-service.md) API. An example is shown below:

    ``` 
    "$ cat segment"{
       "segment":{
          "member_id":25,
          "short_name":"remarketing - netflix user",
          "code":"netflix08"
       }
    }"$ curl -b cookies -c cookies -d @segment""https://api.adnxs.com/segment/958"                        
                            
    ```

1. Upload data into the new segment using [Batch Server-side Segmentation](../bidders/uploading-segment-data-using-bss.md).

1. Set the segment as **"is_public = true"** and activate the segment on the Data Marketplace using the [Segment Billing Category Service](segment-billing-category-service.md) API. An example is shown below:

    ``` 
    "$ cat create_segment_mapping"{
       "segment-billing-category":{
          "active":true,
          "data_provider_id":1,
          "data_category_id":1001,
          "segment_id":111111,
          "is_public":true
       }
    }"$ curl -b cookies -c cookies -X POST -d @create_segment_mapping""https://api.appnexus.com/segment-billing-category?member_id=958"                            
                            
    ```

## Private (custom) segments

Private segments are segments that require explicit sharing by the data provider to the data buyer. Private segments are typically custom segments built for a specific data buyer and are not meant to be seen by any other buyer. Any segment that should not be available to all Data Marketplace buyers should be set as a private segment.

> [!IMPORTANT]
> **Before sharing a private segment with a buyer, verify that buyers have added your company in the Data Marketplace as described in the Add Data Provider section of [Data Buyer Workflow Changes](data-buyer-workflow-changes.md). Sharing segments with non-activated buyers results in un-tracked and un-billed data usage. See [Data Buyer Provider Service](data-buyer-provider-service.md).**
> [!TIP]
> Remember that private segments need to be shared manually to your data buyers. As shown in step 3 of "Create a new private segment", you'll need to use our Member Data Sharing API service to share segment IDs to specific Xandrmembers.

## Create a new private segment

1. Create a new segment object using the [Segment Service](../digital-platform-api/segment-service.md) API. An example is shown below:

    ``` 
     "$ cat segment"{
       "segment":{
          "member_id":25,
          "short_name":"remarketing - netflix user",
          "code":"netflix08"
       }
    }"$ curl -b cookies -c cookies -d @segment""https://api.adnxs.com/segment/958"                 
    ```

1. Set the segment as **"is_public = false"** and activate the segment on the Data Marketplace using the [Segment Billing Category Service](segment-billing-category-service.md) API. An example is shown below:

    ``` 
    "$ cat create_segment_mapping"{
       "segment-billing-category":{
          "active":true,
          "data_provider_id":1,
          "data_category_id":1001,
          "segment_id":111111,
          "is_public":false
       }
    }"$ curl -b cookies -c cookies -X POST -d @create_segment_mapping""https://api.&lt;ph keyref=\"legacy-product-lc\"/>.com/segment-billing-category?member_id=958"
    ```

1. Share private segments with the buyers that should see the segment. An example is shown below:

    ``` 
    "$ cat data_share_single"{
       "member_data_sharing":{
          "buyer_member_id":105,
          "segment_exposure":"list",
          "segments":[
             {
                "id":121175
             },
             {
                "id":121176
             },
             {
                "id":121177
             },
             {
                "id":121178
             }
          ]
       }
    }"$ curl -b cookies -c cookies -X POST -d @data_share_single""https://api.&lt;ph keyref=\"legacy-product-bidders-lc\"/>.com/member-data-sharing?data_member_id=958"               
    ```

## Change a public segment to private

1. Modify the segment to "private" using the [Segment Billing Category Service](segment-billing-category-service.md) API. An example is shown below:

    ``` 
    "$ cat create_segment_mapping"{
       "segment-billing-category":{
          "active":true,
          "data_provider_id":1,
          "data_category_id":1001,
          "segment_id":111111,
          "is_public":false
       }
    }"$ curl -b cookies -c cookies -X PUT -d @create_segment_mapping""https://api.appnexus.com/segment-billing-category?member_id=958&amp;id=77777"
    ```

    > [!NOTE]
    > Xandr will stop sharing this segment to all new Data Marketplace buyers. Data Marketplace buyers that already have access to this segment will continue to have access to the segment.

1. Unshare existing sharing records via the [Member Data Sharing Service](member-data-sharing-service.md) API.

## Change a private segment to public

1. Modify the segment to "private" using the [Segment Billing Category Service](segment-billing-category-service.md) API. An example is shown below:

    ``` 
    "$ cat create_segment_mapping"{
       "segment-billing-category":{
          "active":true,
          "data_provider_id":1,
          "data_category_id":1001,
          "segment_id":111111,
          "is_public":true
       }
    }"$ curl -b cookies -c cookies -X PUT -d @create_segment_mapping""https://api.appnexus.com/segment-billing-category?member_id=958&amp;id=77777"
    ```

> [!NOTE]
> Xandr automatically shares this segment with all Data Marketplace buyers.
