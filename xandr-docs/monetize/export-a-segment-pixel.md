---
title: Microsoft Monetize - Export a Segment Pixel
description: The article displays how to export a segment pixel.Export segment pixel. Choose the pixel format, recommend JavaScript tag. 
ms.date: 10/28/2023
---

# Microsoft Monetize - Export a segment pixel

## Step 1: Get started

Go to the Segment Pixel list in the **Segments** screen (**Network** > **Segment Manager**), select the check box next to the segment pixel that you want to export, click **Actions**, and select **Export** pixels. This displays the **Export Pixels** dialog.

## Step 2: Select the pixel format

We recommend that you select **Use a JavaScript tag**. Selecting **Generate non-secure pixel** can result in browser warnings and/or the pixel not firing.

## Step 3: Select the delivery options

In the **Delivery Options** section, select whether you want to generate the tags on screen, or whether you would rather send the tags via email. If you select to email the tags, you can enter up to 10 email addresses, separated by commas.

## Step 4: Explore advanced options

In the Advanced Options section, you can select additional values to include in the pixel tag.

- **Use codes**: To generate a pixel with your external code (the value you entered when creating the pixel) and your member ID instead of the Microsoft Advertising pixel ID
- **Add user to segments on call**: Enables you to add additional segments
- **Remove user from segments on call**: Enables you to remove the user from segments
- **Parameter**:
  - Include dynamic value: Values are non-negative integers that can be associated and stored with the user at the time of firing the pixel. The same value can be the same across segments in the pixel ("across all segments" option) or they can be specific to each segment in the pixel ("for each segment" option).
  - Include a redirect URL: to redirect URL used to piggyback another pixel

## Step 5: Generate the tags

Click the **Generate Tags** button. Depending on the delivery option selected, the tags either are displayed on the screen or emailed to the addresses specified.

An image pixel looks something like this:

```
<!-- Segment Pixel - test - DO NOT MODIFY -->
<img src="media/seg?add=528336&t=2" width="1" height="1" />
<!-- End of Segment Pixel -->
```

A JavaScript pixel looks something like this:

```
<!-- Segment Pixel - test - DO NOT MODIFY -->
<script src="https://secure.adnxs.com/seg?add=528336&t=1" type="text/javascript"></script>
<!-- End of Segment Pixel -->
```

### Related topics

- [Segment Pixels](segment-pixels-advanced.md)
- [Segment Targeting](segment-targeting.md)
