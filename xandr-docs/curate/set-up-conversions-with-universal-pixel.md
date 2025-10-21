---
title: Microsoft Curate - Set Up Conversions with Universal Pixel
description: In this article, learn step-by-step instructions on how to set up conversions with universal pixel.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-curate
ms.author: shsrinivasan
---

# Microsoft Curate - Set up conversions with Universal Pixel

You can set up conversions for your Universal Pixel using rules and conditions, then track conversion activity using Curate reporting.

1. From the top menu bar, select **Audiences** \> **Universal Pixel**.
1. Select a pixel from the **Universal Pixels** page.

    If no pixels are defined, use the setup instructions in [Universal Pixel Basic Implementation](universal-pixel-basic-implementation.md) to create one.

1. Select **+New**.
1. Provide a name for the conversion.

    This name will identify the conversion in conversion reporting.

1. Categorize your conversion as a lead, landing page, or another event category.

    > [!NOTE]
    > If you have already used a standard event as a condition for the conversion, then the conversion will be categorized with that standard event by default.

1. Under **Lookback**, specify the time between an ad view or select and the conversion event during which you will attribute conversions to the ad view or select.

    For example, if you want to attribute any shopping cart adds that occurred in the month after viewing an ad to the ad view event, set the post view lookback to 31 days.

1. Under **Count**, determine if you will limit the number of attributed conversions per user. You can also limit the number of conversions counted within a period of time.

    For example, you probably want to attribute multiple purchases per user within a time window to the ad, but if your conversion event is a page view for an informational site, counting multiple views might not be meaningful.

1. Select **Save**.
