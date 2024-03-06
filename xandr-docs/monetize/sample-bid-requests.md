---
title: Microsoft Monetize - Sample Bid Requests
description: This page provides step-by-step instructions to sample bid request data.
ms.date: 10/28/2023
---


# Microsoft Monetize - Sample bid requests

The **Bid Request Sampler** provides sample bid request data under certain time frames and conditions. You can download results as a text file.

> [!NOTE]
> The Microsoft Monetize Monitoring feature is in **Open Beta** and currently only supports deal line items, augmented line items (ALI), and guaranteed delivery augmented line items (GDALI). It is subject to change without notice and is only available to select clients.

To sample bid request data:

1. In **Date**, select the date and time in which you want to pull bid requests.

    > [!NOTE]
    > Bid requests are pulled within the previous 24 hours of the date and time you select. You can only select a date and time within the last 7 days.

1. In **Media Type**, select either **Any Media Type** or a specific media type (**Banner**, **Video**, **Native**, or **Audio**).
1. In **Country**, select either **Any Country** or **Custom Country** (use the **Select Country** drop-down to select a country from the list).
1. In **Number of Bid Request**, select the number of bid requests you would like to pull.

    > [!NOTE]
    >  Bid requests are limited to a maximum of 100.

1. Click **Search** to generate bid requests.

    > [!NOTE]
    > Bid requests are generated using a 0.001% sampling rate. If you try to generate a bid request and don't see results, Microsoft Advertising will automatically increase the sampling rate to 5%. Wait 30 minutes for this sampling rate change to take effect before you generate another bid request. You don't have to keep the **Bid Request Sampler** section open while you wait 30 minutes before generating a new request. You can leave the section and come back to generate a new request after 30 minutes have passed.

    Bid requests (if any) are listed in the **Bid Request** section. You can do the following with **Bid Request** results:
    - Download generated bid requests as a text file by clicking **Export All as Text File**. The text file is downloaded to your browser’s downloads folder.
    - Copy the generated bid requests by clicking **Copy Request to Clipboard**.
    - Open the generated bid requests in a new browser tab by clicking **Open in New Window**.

## Related topics

- [Monitor Line Items](monitor-line-items.md)
- [Troubleshoot Line Items](troubleshoot-line-items.md)
- [View Line Item Details](view-line-item-details-smw.md)
