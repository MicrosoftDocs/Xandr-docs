---
title: Microsoft Invest - Buy Microsoft Windows 3rd Party AppNetwork Inventory
description: Learn about Microsoft Windows 3rd party AppNetwork inventory's creative specifications, targeting methods, and ways to maximize reach across Windows app inventory.
ms.date: 10/28/2023
---

# Microsoft Invest - Buy Microsoft Windows 3rd party AppNetwork inventory

> [!TIP]
> For general mobile documentation, see [Welcome to Mobile](welcome-to-mobile.md).

## Inventory overview

Reach millions of user on desktop, tablet, and phone through Windows AppNetwork and Windows Phone AppNetwork 3rd Party. Advertising on Windows 3rd Party has never been a better investment, as improved user-sync and new media offerings best position your brand to connect with a highly engaged audience. Windows AppNetwork and Windows Phone AppNetwork allow brands to access millions of engaged users through hundreds of thousands of 3rd party apps.

## Availability and volume

Microsoft Windows 3rd Party AppNetwork inventory is fully integrated with the Microsoft Advertising Exchange (Member 280) and is classified as “Desktop” and “Web” supply type for both Desktop/Tablet, Web, and Phone.

> [!NOTE]
> Supply type is a targeting attribute designated by the seller that may not reflect actual device type.

- Available globally - top markets are United States, Brazil, United Kingdom, France, Vietnam.
- 13 billion monthly impressions worldwide.

> [!TIP]
> Inventory Research with specific break-downs of Windows App inventory by size & country can be accessed via the Network tab then filtering for Supply Type = "App" within seller Microsoft Advertising Exchange (280).

## Formats and specifications

### Creative specs

| Creative Size | Windows AppNetwork | Windows Phone AppNetwork |
|:--------------|:-------------------|:-------------------------|
| 160x600       | X                  |                          |
| 250x250       | X                  |                          |
| 300x250       | X                  | X                        |
| 300x600       | X                  |                          |
| 728x90        | X                  |                          |
| 320x50        | X                  | X                        |
| 300x50        | X                  | X                        |
| 480x80        |                    | X                        |
| 640x100       |                    |                          |

Technical Attributes:

- MRAID 1.0 and 2.0
- Hosted Images
- HTML
- HTML - iframe
- Javascript (in web view)
- Image (Third-Party Ad Served)
- No Flash Allowed on Windows Phone
- Video

> [!TIP]
> We have mapped the top 1000 app names for targeting on both the Windows AppNetwork and Windows Phone AppNetwork. If you want to target an app name outside of the top 1000, reach out to your account manager. There is reporting capability for App targeting.

Ad Quality:

- [Microsoft CAP](https://about.ads.microsoft.com/en-us/resources/policies)
- Animation Length up to 30 sec

### Legacy Ads SDK creative specs

Legacy SDK (versions prior to Windows 10) currently represents 55% of total impressions on the Windows 3rd Party AppNetwork (Windows 7 has 35% of total traffic, Windows 8.1 10% etc.). This percentage is steadily decreasing as Windows 10 adoption continues.

Any legacy SDK before Windows 8.1 lacks support for mobile standard third-party ad serving, impression tracking pixels, javascript and MRAID.

As an Microsoft Advertising Buyer, you may still access legacy SDK inventory by uploading an image creative to Microsoft Advertising and specifying a landing page. For more information on uploading a hosted image as a creative, see [Add Banner Creatives](./banner-and-html5-creatives.md).

## Instructions for targeting

To target **Windows AppNetwork and/or Windows Phone AppNetwork** inventory by **PubID** via Standard Line Item - Campaign:

1. In the **Device and Supply Type** section, select **all device types** to target.
1. Select **Default** to target **Web, Mobile Web,** and **App Placements**.
1. In the **Inventory** section, click **Edit**.
1. On the **3rd Party Inventory** &gt; **Publishers & Categories** subtab, target **pubID** **348882** for **Windows AppNetwork** and/or **pubID** **336212** for **Windows Phone App Network**.
1. Click **Add**.

To target **Windows AppNetwork** and/or **Windows Phone AppNetwork** via Augmented Line Item - Programmatic Splits:

1. Leave the default device type selected and Inventory Type should be set to **Apps & Web**.
1. On the **Programmatic Split**, select **Publisher** and add **348882** & **336212** for desktop and phone apps respectively for inclusion.
1. Click **Add**.

To target **Windows AppNetwork** and/or **Windows Phone AppNetwork** by deal:

1. Navigate to **Package MarketPlace** from the **Partners** ribbon.
1. Select seller as **Microsoft Advertising Exchange (280)**.
1. Search for Microsoft **Run of Windows PC Apps** and **Run of Windows Phone Apps**.
1. Click **Get Deals** and this will generate a Deal ID to target.

### Information about targeting criteria

| Targeting Criteria | Windows AppNetwork (Desktop/Tablet) | Windows Phone AppNetwork (Phone) |
|:-------------------|:------------------------------------|:---------------------------------|
| Pub ID             | 348882                              | 336212                           |
| Seller Member      | 280                                 | 280                              |
| Language           | Available                           | Available                        |
| Supply Type        | Web                                 | Web                              |
| OS Family          | Microsoft Windows                   | Microsoft Windows                |
| Device Type*       | All                                 | All                              |
| Device Make Model  | N/A                                 | Available                        |
| Carrier            | Available                           | Available                        |
| Lat/Long           | Limited Availability                | Limited Availability             |
| App Targeting**    | Limited Availability                | Limited Availability             |

It is recommended to **NOT** use Device Type for targeting. Retain the "All" default setting to maximize device targeting.

> [!TIP]
> To report on delivery for each publisher, you can select "publisher" as a dimension in an analytics report.
>
> The best way to distinguish between Windows 10 Desktop Inventory and Windows Phone inventory is to use creative size targeting or OS (extended) targeting.

## Best practice for reach

To maximize reach across Windows App inventory, we recommend targeting both Supply Type "Mobile App" and “Web” inventory within Microsoft Advertising Exchange without additional parameters such as "Device Type." This is because there are certain instances where Microsoft Advertising does not receive this information from the device SDK and applications are presented as Sites referencing the Windows Store URL.

## Packages and deals

Packages are a great way to leverage Microsoft user data with your campaigns. Currently, Windows AppNetwork and Windows Phone AppNetwork offer a few packages broken out by content category such as entertainment, games, and news. For more information, see [Buying Microsoft Deals](buying-microsoft-deals.md).

## Extra information

### User identification (Microsoft Ad ID)

All Microsoft Windows App inventory includes a mobile-specific device identifier called the Windows Ad ID. This identifier is similar to other mobile app identifiers like IDFA or Google Play in that it is persistent across apps on the same device, compliant to the user's OS-level privacy settings.

For Windows 10 inventory, Microsoft also provides the Microsoft Advertising ID (UUID64) corresponding to the user's default browser where available. This process is called user-syncing, and enables advertisers to track users across devices. **User-sync is available on 82% of Windows 10 impressions, and better enables category targeting, frequency cap, conversion tracking and more.**

### App-install attribution (Window Store ID)

For buyers running campaigns with a CPA goal of an App installation, the third-party app installation vendors Tune, Adjust, and Kochava support Windows Apps attribution tracking through Microsoft Advertising. For more information on hosted Microsoft Advertising creatives and how to use third-party app installation vendors for conversion tracking within Microsoft Advertising, see [Set Up Third-Party Mobile App Install Tracking](set-up-third-party-mobile-app-install-tracking.md). If you are using a third-party ad server, you will be tracking conversions in that third-party ad server, which will require its own integration with Tune, Adjust, or Kochava for conversion attribution. We will continue onboarding additional attribution vendors. If you rely upon a specific attribution vendor that is not supported today, contact your Microsoft Advertising Account Representative.

## More questions?

If you have any further questions about buying Windows App Inventory, contact your Microsoft Advertising account representative.
