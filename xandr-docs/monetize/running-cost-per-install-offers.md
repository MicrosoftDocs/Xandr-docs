---
title: Microsoft Monetize - Running Cost per Install Offers
description: This page covers procedures for integrating with an external app install tracker, setting up the right creative click URLs and reporting on your installs.   
ms.date: 10/28/2023
---


# Microsoft Monetize - Running cost per install offers

This document describes the procedure for setting up cost per install offers with your mobile ad campaigns. This includes procedures for:

- Integrating with an external app install tracker
- Setting up the right creative click URLs
- Reporting on your installs (conversions)

## Step 1. Set up third-party mobile App install tracking

Follow the steps described in [Set Up Third-Party Mobile App Install Tracking](set-up-third-party-mobile-app-install-tracking.md) to integrate with a third-party mobile app install tracker and set your creative click URLs so that Microsoft Advertising will be able to register your conversions. You may also want to associate your creative with an impression tracker. For instructions, see [Create an Impression Tracker](create-an-impression-tracker.md).

> [!NOTE]
>
> - The instructions in [Set Up Third-Party Mobile App Install Tracking](set-up-third-party-mobile-app-install-tracking.md) will only work with Microsoft Advertising-hosted creatives at this time. Technicallwill only work with Microsoft Advertising-hosted creatives at this time. Technically, our server-side conversion attribution requires the `${SSP_DATA}` macro to be populated by the creative's ad server, so any ad server that populates this macro will work. In practice, there are not any other ad servers that populate this macro at this time.
> - You should thoroughly test the integration with your install tracking vendor before campaigns go live to avoid discrepancy issues. For more information on how to test that your conversion pixels are loading as planned, see [Managing Mobile Discrepancies](managing-mobile-discrepancies.md).
> - For more information on how server-side conversion tracking works, see the descriptions in [Set Up Third-Party Mobile App Install Tracking](set-up-third-party-mobile-app-install-tracking.md) and [Server-Side Conversion Pixels](server-side-conversion-pixels.md).

## Step 2. Set up your mobile campaigns

Depending on your needs, you'll want to follow the steps outlined in one of the following:

- [Buy Mobile Inventory via RTB](buy-mobile-inventory-via-rtb.md)
- [Buy Mobile Inventory Directly from a Publisher](buy-mobile-inventory-directly-from-a-publisher.md)

## Step 3. Report on your conversions

Use the [Advertiser Attributed Conversions Report](advertiser-attributed-conversions-report.md) to report on the conversions coming through these creatives. This will also let you check for discrepancies with your external install tracking vendor.

## Related topics

- [Mobile Buying FAQ](mobile-buying-faq.md)
- [Welcome to Mobile](welcome-to-mobile.md)