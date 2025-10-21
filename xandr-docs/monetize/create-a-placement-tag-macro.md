---
title: Create a Placement Tag Macro
description: In this article, find information on how to create and set up a placement tag macro.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Create a placement tag macro

If you would like even more flexibility than what our existing macros provide, you can create a placement tag macro, which will send custom data on the placement ad call so that you can use it in your creative tag. You can create a placement tag macro if you have access to both managed supply and demand.

Placement tag macros can be used for sending page-level data to non-Microsoft Advertising systems. For more information about our creative macros, see [Creative Macros](creative-macros.md).

> [!NOTE]
> Before creating placement tag macros, you should consider the following:
>
> - Data passed in using this method is not stored in our data pipeline. There is no reporting available from Microsoft Advertising related to your use of this feature.
> - Like most of our non-clicktracking creative macros, these macros are populated by our bidder engine. Therefore, they won't populate in creative previews, but only during true auctions.

1. Create a placement using your platform or content management system.

    For more information, see [Create a Placement](create-a-placement.md).

1. Export the placement from your platform or content management system.

    For more information, see [Export Placement Tags](export-placement-tags.md).

    You should now have a snippet of HTML that represents your placement. It should look something like this:

    ```
    <!-- BEGIN JS TAG - [A Publisher You've Probably Heard of] - Default < - DO NOT MODIFY -->
    <SCRIPT SRC="https://ib.adnxs.com/ttj?id=608398&size=[WIDTHxHEIGHT]&cb=[CACHEBUSTER]" TYPE="text/javascript"></SCRIPT>
    <!-- END TAG -->
    ```

1. Edit the placement tag by adding one or more of the query string parameters, such as `pt0`, `pt1`, `pt2`, `pt3`, `pt4`, `pt5`, `pt6`, `pt7`, `pt8`, `pt9`, to the ad call's URL within the HTML.

    This will allow the placement tag to send the custom data that you specified.

    > [!NOTE]
    > Please ignore the "DO NOT MODIFY" warning.

    The modified URL would look similar to this: `https://ib.``adnxs``.com/ttj?id=608398&size=[WIDTHxHEIGHT]&cb=[CACHEBUSTER]&pt1=product-keywords:iphone;ipad&pt2=pagescore:99.2`

    > [!NOTE]
    > Notice the differences between the URLs before and after adding the `pt1` and `pt2` query string parameters. Those parameters contain whatever data you assign to them, and that data will be used to populate the corresponding macros in your creative.

1. Create a third-party creative.

    > [!NOTE]
    > You won't be able to create a third-party creative if you select an HTML tag that is being served inside an iFrame. This is because our system does not pass the various query string parameters when generating iFrames. Therefore, the macros will not populate with your custom data.

    For more information, see [Add a Creative](add-a-creative.md) and [Add Creatives in Bulk](add-creatives-in-bulk.md).

1. Inside the **Tag** text area, enter the JavaScript that you would like to use to generate your creative.

    The macro text "variables" available for your use include:
    - `${PT0}`
    - `${PT1}`
    - `${PT2}`
    - `${PT3}`
    - `${PT4}`
    - `${PT5}`
    - `${PT6}`
    - `${PT7}`
    - `${PT8}`
    - `${PT9}`

    The macro text variables correspond to the following query string parameters on the placement ad call:

    | Macro Text | Query String Parameters |
    |---|---|
    | `${PT0}` | pt0 |
    | `${PT1}` | pt1 |
    | `${PT2}` | pt2 |
    | `${PT3}` | pt3 |
    | `${PT4}` | pt4 |
    | `${PT5}` | pt5 |
    | `${PT6}` | pt6 |
    | `${PT7}` | pt7 |
    | `${PT8}` | pt8 |
    | `${PT9}` | pt9 |

    Here's a simple example of how you might use the macro text inside your JavaScript creative's code:

    ```
    var pt1 = "${PT1}";
    var pt2 = "${PT2}";
    document.write("<img src=\"https://great-ad-server.com/300x250/f0f&product_keywords=" + pt1 + "&page_score=" + pt2 + " \">");
    ```

## Related topics

- [Create a Placement](create-a-placement.md)
- [Export Placement Tags](export-placement-tags.md)
- [Click Tracking](click-tracking.md)
