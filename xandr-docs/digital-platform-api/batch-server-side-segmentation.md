---
title: Digital Platform API - Batch Server-Side Segmentation
description: In this article, find information about the use cases, features, and workflow of the Batch Segment Service.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Batch server-side segmentation

The Batch Segment Service is also known as BSS. It is a server-side method that allows you to batch your users together and add them to segments in bulk by uploading a file to Xandr via the API. You can easily integrate your first, second, and third-party audience data to create dynamic, configurable segments for sophisticated user targeting and increased ROI. This data can be used in conjunction with data from buyers or sellers for the purpose of campaign targeting or yield management.

## Use cases

### CRM / outside audience uploads

As a buyer, DMP, or data provider, you may have offline customer data or online customer data that resides in a system that's separate from Xandr. The Batch Segment Service can be used to upload these user segment files to Xandr. For example, a retailer could upload CRM data from their in-store system for targeting on Xandr.

The Batch Segment Service allows you to upload audiences to Xandr's platform through a batch/bulk upload framework. This data can be used in conjunction with data from buyers or sellers for the purposes of campaign targeting or yield management. All data sent through the Batch Segment Service is appended to the existing segment data already in our system.

Features include:

- Ability to upload compressed files
- Error checking of segment data
- Configurable input file format
- Confirmation of successful upload
- Feedback on overall processing status
- Association of segments to users regardless of location of users
- A high maximum data volume

> [!TIP]
> Before you can use the Batch Segment Service, you'll need to get it set up. See [Initial BSS Account Setup](initial-bss-account-setup.md) for instructions.
> [!IMPORTANT]
> Gzip is the only file compression method supported by this service.

## Workflow

- Step 1: [Map your user IDs with Xandr user IDs](../invest/user-id-mapping-with-getuid-and-mapuid.md).

- Step 2: Make sure you've set up your BSS account using the instructions in [Initial BSS Account Setup](initial-bss-account-setup.md).

- Step 3: Upload your file using the instructions in [Uploading Segment Data Using BSS](uploading-segment-data-using-bss.md).

  Alternately, you could implement [Passive Segment Upload Using AWS S3](passive-segment-upload-using-aws-s3.md). The preferred format is Avro.

- Step 4: Check the status of your file and correct any errors shown in the error logs. You can also see exactly how many valid user IDs you added to each segment in the segment logs.

> [!NOTE]
> Targeting may, in some cases, encompass related IDs linked to the same user. In such instances, the identifier(s) in exposure logs represent the same user as the uploaded ID.
