---
title: Bidder - Initial BSS Account Setup
description: Learn about the Batch Segment Service account setup.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidder - Initial BSS account setup

To start using the Batch Segment Service (BSS), open a ticket with [product support](https://support.ads.microsoft.com) and:

1. Decide which file format you plan to use: [BSS Avro File Format](../digital-platform-api/bss-avro-file-format.md) is preferred, but you can use the [Legacy BSS File Format](./legacy-bss-file-format.md) if you don't need to support external IDs.
1. If you're using Avro format and you decide to use a custom schema rather than the Xandr schema, provide the custom schema. You can use the Xandr-provided schema: see [BSS Avro File Format](../digital-platform-api/bss-avro-file-format.md) for more information.
1. If you're using the legacy file format (see [Legacy BSS File Format](./legacy-bss-file-format.md)):
    1. Define each separator you will use (SEPARATOR 1 through SEPARATOR 5).
    1. Define the order of `SEG_FIELDS`. Send us the format that is simplest for you. This includes formats that include multiple segments on one line.
1. Provide a short sample file in your chosen format.
1. Provide external IDs, if applicable. For example, you use mapUID to store the mapping in Xandr. If you use another member's external user IDs, include their `member_id.`
1. Provide associated `member_id`s, if you need to populate segments belonging to other members.
1. Identify the number of error lines you would like to see (max. 999).
1. Provide a default expiration window for your segments. For example, set segments to expire after 60 days. The maximum expiration that can be set is 180 days. Users are automatically removed from segments after 180 days.

> [!NOTE]
> If you include `EXPIRATION` in your `SEG` block, you cannot use a default expiration setting.

For our internal capacity planning, provide the following information:

1. The number of unique user IDs per upload.
1. The number of expected uploads per day.
1. The number of unique segments per upload.

> [!NOTE]
> If you need to populate segments belonging to other members, that member must send a ticket via [product support](https://support.ads.microsoft.com) explicitly authorizing your usage: "I authorize `CLIENT_NAME` to add users to/remove users from segments in my account using the Batch Segment API service." They must also add their Account Manager to the CC field in the support form.

## Related topics

- [Batch Server-Side Segmentation](./batch-server-side-segmentation.md)
- [Batch Segment Service Best Practices](./batch-segment-service-best-practices.md)
- [Troubleshooting BSS Uploads](./troubleshooting-bss-uploads.md)
