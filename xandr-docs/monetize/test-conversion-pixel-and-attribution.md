---
title: Test Conversion Pixel and Attribution
description: In this article, find instructions on how to test conversion pixels using a test publisher and placement.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Test conversion pixel and attribution

You must have a test publisher and placement to test conversion pixels. If necessary, users set up a test publisher and placement as described in [Create a Publisher](create-a-publisher.md) and [Create a Placement](create-a-placement.md). Edit the placement, and filter the campaign to the campaign that you are testing. This will ensure that the placement will only show ads from your test campaign. Ensure that your network or publisher ad quality profiles has **Direct Advertiser Trust** > **Maximum**, or that you have allowed your campaign's creative ID on the network and publisher ad quality rules.

1. Edit your advertising campaign to include the test placement:
    1. Select **Buy Direct Inventory** with priority **10**
    1. Under **Targeting**, select **Inventory** and include your test placement from **Direct Inventory**:

    > [!NOTE]
    > Unless your campaign is already buying direct inventory, make absolutely sure to only include your test placement. Otherwise, you run the risk of delivering across your entire network instead of a single placement.

1. [Run a debug auction](understanding-the-debug-auction.md) using a URL in this format: `https://secure.adnxs.com/tt?id=[TEST_PLACEMENT_ID]&size=[WIDTH]x[HEIGHT]&debug_member=[MEMBER_ID]&dongle=[DONGLE]`

    For example:

    ```
    https://secure.adnxs.com/tt?id=123456&size=300x250&debug_member=1234&dongle=clienta123
    ```

1. [Review the debug output](understanding-the-debug-auction.md) that your test campaign serves.

    It will probably take 10-15 minutes for your campaign to appear. Once the test campaign is winning your debugs, you're ready to serve yourself an ad.

    > [!TIP]
    > Use `Control`+`F` or `Command`+`F` to search for the campaign ID.

1. Once the test campaign is winning the debug auctions, serve yourself an ad using a URL in the following format:

    `https://secure.adnxs.com/tt?id=[TEST_PLACEMENT_ID]&size=[WIDTH]x[HEIGHT]`

    | Option | Description |
    |---|---|
    | **To count post-click conversions** | Click the creative. |
    | **To count post-view conversions** | Do not click, and proceed to the next step. |

1. Use your browser's developer tools to confirm that the pixel is firing.
    1. Open a new browser tab in Chrome or Firefox.
    1. Right-click in the tab window and select **Inspect Element**.
    1. Select the **Network** tab.
    1. From the current tab, navigate to the page where the conversion pixel is placed.

    You will see all the calls going out from the browser to various servers. Within the list of calls, you should see your pixel tag: `https://secure.adnxs.com/px?id=[PIXEL_ID]&t=X` where `X` is `1` (JavaScript) or `2` Image.

    | Scenario | Action Item |
    |---|---|
    | If you see the pixel call fire with the correct ID | Success! You should see a conversion appear in reporting several hours after the pixel fires. |
    | If you have served yourself an ad and have confirmed that the pixel fired properly, but do not see conversions several hours later: | Contact the [Customer Support team](https://help.xandr.com) and include all of the following information: <br> - your Microsoft Advertising user ID (you can find this on `https://secure.adnxs.com/cookie?dongle=[YourMember'sDongle]`) <br> - the hour (including time zone) you served yourself the impression <br> - the pixel ID you fired <br> - the campaign ID you used <br> - the page where the conversion pixel was trafficked <br> - an HTTP archive (available in the browser's **Network** tab) |

## Related topics

- [Server-Side Conversion Pixels](server-side-conversion-pixels.md)
- [Create a Conversion Pixel](create-a-conversion-pixel.md)
- [Export Conversion Pixels](export-conversion-pixels.md)
- [Update Campaigns](update-campaigns.md)
- [Conversion Pixels Advanced](conversion-pixels-advanced.md)
- [Reporting on Conversions](reporting-on-conversions.md)
- [Understanding the Debug Auction](understanding-the-debug-auction.md)
