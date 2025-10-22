---
title: Microsoft Windows App Inventory for Bidders
description: In this article, learn about Microsoft Windows app inventory for bidders, their availability, inventory volume, specifications, and how to buy a mobile inventory.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Microsoft Windows app inventory for bidders

## Inventory overview

- Advertising in apps across multiple devices on Windows PCs & tablets (Windows 8 and Windows 10) and Windows Phone 8.
- Dynamic, MRAID-enabled ads on touch-enabled devices. Windows 8 includes additional support for standard display size creatives.
- Inventory includes Microsoft Owned & Operated (e.g. Bing, MSN, Xbox) and third-party App Network featuring applications from across the Windows App Store.

Windows App Inventory includes:

## Availability and volume

Microsoft Windows App inventory is fully integrated with the Microsoft Advertising Exchange (Member 280) and classified as “Mobile App” supply type.

- 16 billion monthly impressions globally.
- Available in every MAX market.
- 50/50 mix of impressions Windows and Windows Phone device impressions.

For detailed inventory availability by size and country or region, contact your Xandr account representative and ask to receive periodic Mobile Inventory Availability Reports via e-mail.

## Creative formats and specifications

The majority of Microsoft Windows App inventory supports mobile creative standards including MRAID and JavaScript but impressions from legacy SDK versions will continue to be available. The Creative Specs focus on new SDK inventory.

| Specifications | Windows 8/10 | Windows Phone |
|:---|:---|:---|
| Sizes | - 160x600<br> - 300x250<br> - 300x600<br> - 728x90 | - 300x50<br> - 320x50<br> - 480x80<br> - 640x100 |
| Technical Attributes | - MRAID 1.0 and 2.0<br> - Hosted Images<br> - HTML<br> - HTML- iframe<br> - Javascript (excluding certain calls not supported in SDK web view)<br> - Image (Third-Party Ad Served)<br> - No flash allowed | - MRAID 1.0 and 2.0<br> - Hosted Images<br> - HTML<br> - HTML- iframe<br> - Javascript (excluding certain calls not supported in SDK web view)<br> - Image (Third-Party Ad Served)<br> - No flash allowed |
| Ad Quality | - [Microsoft CAP](https://advertising.microsoft.com/en/policies)<br> - Animation Length up to 30 seconds. | - [Microsoft CAP](https://advertising.microsoft.com/en/policies)<br> - Animation Length up to 30 seconds. |

**Legacy Ads SDK Creative Specs:**

Microsoft is phasing out a legacy SDK which lacks support for mobile standard third-party ad serving, impression tracking, Javascript and MRAID. As such, the majority of bidders will not be able to consume the inventory with a standard integration. However, since this accounts for 50% of the inventory today it is a significant opportunity to explore. If you are interested in more detail on this inventory opportunity, contact your Xandr account representative.

## Buying Microsoft Windows app mobile inventory

- [Step 1: Ensure that you accept Microsoft Windows app bid requests](#step-1-ensure-that-you-accept-microsoft-windows-app-bid-requests)
- [Step 2: Target and bid on Windows app inventory](#step-2-target-and-bid-on-windows-app-inventory)
- [Step 3: Receive auction results](#step-3-receive-auction-results)

### Step 1: Ensure that you accept Microsoft Windows app bid requests

Bidder profiles allow you to filter for the bid requests that you want to receive. To accept Windows App bid requests you must allow the values below within an existing bidder profile or create a new bidder profile specifically for Windows App bid requests (this profile must not have segment filtering enabled since all mobile_app bid requests are cookieless). For details about updating or creating bidder profiles, see [Legacy Bidder Profile Service](legacy-bidder-profile-service.md). Windows App bid requests have the following characteristics that allow you to distinguish them from other Xandr bid requests:

| Field | Value |
|:---|:---|
| `seller_member` | `280` |
| `supply_type` | `mobile_app` |

### Step 2: Target and bid on Windows app inventory

When Xandr receives an impression from Windows App, we route these impressions through a publisher, site, and tag ID combination, in increasing order of granularity. Xandr's bid request includes these IDs (`adid`), allowing you to target specific slices of Windows App inventory. The `adid` is passed through the [device.ifa field](outgoing-bid-request-to-bidders.md) in the OpenRTB request.

Xandr's bid request for a Windows App impression includes [standard mobile fields](mobile-for-bidders.md) useful for your bidder to target.

### Step 3: Receive auction results

Xandr's Notify request is essential to tracking when an impression is served, the win price of the impression, and to provide you with any custom notify data you may have included with the bid. This information will be helpful for understanding bid rejections due to Microsoft-specific creative requirements on Windows 8 or the legacy SDKs.

### Example request/response chain

```
{
    received_on: "2018-03-01 20:43:59",
    request: {
        id: "123456111412345",
        imp: [{
            id: "17",
            banner: {
                w: 300,
                h: 50,
                id: "1",
                battr: [
                    1,
                    2,
                    10
                ],
                pos: 0,
                format: [{
                    w: 300,
                    h: 50
                }]
            },
            instl: 0,
            tagid: "11",
            bidfloor: 0.09,
            bidfloorcur: "USD",
            secure: 0,
            pmp: {},
            ext: {
                appnexus: {
                    estimated_clear_price: 1.75,
                    predicted_video_completion_rate: 0.410102,
                    predicted_view_rate_over_total: 0.278455
                }
            }
        }],
        site: {
            id: "12",
            domain: "microsoft.com",
            cat: [
                "IAB19-18"
            ],
            page: "https://www.microsoft.com/store/apps/windows",
            publisher: {
                id: "345"
            }
        },
        device: {
            ua: "Mozilla/5.0 (Windows NT 10.0; Win64; x64; WebView/3.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36 Edge/16.16299",
            dnt: 0,
            make: "Unknown",
            model: "Unknown",
            os: "Microsoft Windows",
            language: "en",
            connectiontype: 0
        },
        user: {
            id: "20",
            gender: "O",
            data: [{
                    id: "0",
                    segment: [{
                        id: "1",
                        value: "0"
                    }]
                }
            ]
        },
        test: 0,
        at: 1,
        tmax: 350,
        wseat: [
            "1",
            "4",
            "7",
            "8"
        ],
        cur: [
            "USD"
        ],
        bcat: [
            "IAB23-3"
        ],
        ext: {
            appnexus: {
                seller_member_id: 280,
                spend_protection: false,
                publisher_integration: {
                    is_header: 0,
                    bid_shading_high: 0.2,
                    bid_shading_medium: 0.4,
                    bid_shading_low: 0.35
                }
            }
        },
        source: {
            fd: 1,
            tid: "123abc12-45c0-123b-456c-123123123"
        }
    },
    response: {
        id: "987",
        seatbid: [{
            bid: [{
                id: "0",
                impid: "17",
                price: 0.08,
                adid: "555",
                nurl: "https://11.11.111:111/notify?TAFFYOpenRTBAuctionID=${AUCTION_ID}&price=${AUCTION_PRICE}",
                crid: "0",
                ext: {
                    appnexus: {
                        custom_macros: [{
                                name: "MY_CO_MACRO",
                                value: "50"
                            }
                        ]
                    }
                }
            }],
            seat: "5555"
        }],
        cur: "USD"
    }
}
```

## Best practices

### Application targeting (App ID)

Microsoft Windows Apps are available to users through the Windows App stores. There are two separate App stores, one for Windows Phone and the other for Windows 8 and higher.

Bidders should download [Windows App ID Lookup Table](/windows/configuration/find-the-application-user-model-id-of-an-installed-app) to map App IDs to metadata like Platform, Name, Category and URL in the public store. A public API to retrieve this information is not available, but Microsoft will update the lookup table monthly.

### App-install attribution (App ID)

For buyers running campaigns with a CPA goal of an App installation, the third-party app installation vendors Kochava and HasOffers supports Windows Apps attribution tracking through Xandr. Microsoft will continue onboarding additional attribution vendors. If you rely upon a specific attribution vendor that is not supported today, then contact your Xandr account representative.

### Reach

To maximize reach across Windows App inventory, we recommend targeting “Mobile App” inventory within Microsoft Advertising Exchange without additional parameters such as “Device Type.” This is because there are certain instances where Xandr does not receive this information from the device SDK.
