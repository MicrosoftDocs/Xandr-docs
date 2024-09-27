---
title: Microsoft Invest - Server-Side Conversion Pixels
description: This page makes references to an attribution server which is set up to capture the server-side pixel token data, attribute a conversion, and inform about a successful conversion.
ms.date: 10/28/2023
---

# Microsoft Invest - Server-side conversion pixels

## Use case

Server-side conversion pixels, also known as postback URLs, are used in situations where normal Microsoft Advertising cookie-based
conversion tracking is unavailable or not used. A major use case for server-side pixels is to track conversions on mobile devices where app sandboxing (the inability of one mobile app to communicate with another) and a lack of cookies prevent a conversion from being recorded in a conventional manner.

For instance, if the conversion is a user downloading and installing an app from the Apple App Store, a normal conversion pixel could not track a user completely through this process; however, a server-side pixel would allow for this conversion to be tied to a specific auction.

This page makes references to an attribution server. This is a server that is set up to capture the server-side pixel token data, attribute a conversion, and notify Microsoft Advertising of a successful conversion.

## Server-side pixel functionality

<!--:::image type="content" source="./media/ssp-kb-article-graphic-revised.png" alt-text="Diagram explaining the server-side pixel conversion.":::-->
- From a browser or app there is an ad call to Microsoft Advertising.
- Microsoft Advertising runs an auction.
- Microsoft Advertising passes back the winning creative along with a server-side pixel token that is unique to the auction. Here is an example server-side pixel data token:
  ```ams1AAAAAAAAkQC8rFPull3JKKU9tUKckv1Oj1WFMAAAAAULAAA3AAAAUQIAAD4AAA.```
  Often there is a period at the end that must be included.
- The user clicks on the creative. The landing page for the creative has special macros that include information like the server-side pixel token and mobile device IDs (if present) in the landing page URL which it receives from Microsoft Advertising An example landing page URL with the macros would look like this:

    ```
    https://attributionserver.com/attr?id=12&idfa=${DEVICE_APPLE_IDA}&token=${SSP_DATA}
    ```

    The user’s device ID and the server-side pixel token replace the macros in the URL.

    ```
    https://attributionserver.com/attr?id=12&idfa=adw-231234-550&token=ams1AAAAAAAAkQC8rFPull3JKKU9tUKckvOj1WFMAAAAAGULAAA3AAAUQIAAd$AAA
    ```

- The attribution server captures the token along with any other available information.
- The user is redirected to the App Store or an advertiser’s landing page. The user converts. In the case of a mobile app installation the user downloads the app and opens it.
- Built into the app or conversion page is a call to the attribution server. For apps this is fired when the app is opened for the first time.
- The attribution server determines that the Microsoft Advertising’s advertiser is attributed with the conversion. This is typically a last touch scenario.
- The attribution server fires to Microsoft Advertising which includes the Conversion Pixel ID and the token. An example of this call would look like:

    ```
    https://sspx-router.adnxs.com/sspx?id=1235&sspdata=ams1AAAAAAAAkQC8rFPull3JKKU9tUKckv1Oj1WFMAAAAAGULAAA3AAAAUQIAAD4AAA
    ```

    The ID parameter is the Microsoft Advertising’s ID of the pixel and sspdata is the token.
- Microsoft Advertising connects the sspdata value to the token value and attributes the conversion to the correct auction.

## Locate the URL for a server-side pixel call

For server-side conversion pixels, you'll need to generate a URL that you can call, instead of an HTML-based pixel that is placed on a publisher's web page. To do this, consult the **Explore Advanced Options** section of the [Export Conversion Pixels](./export-conversion-pixels.md) page. The URL that is generated when you export the pixel will look something like this:

### Export Pixels

Conversion Pixel - test conversion  - Call the following URL to register a server side conversion:

```
https://sspx-router.adnxs.com/sspx?id=59633&sspdata=[SSPDATA] 
(SSPDATA is the token received by the advertiser when the user reaches the landing page)
```

<!--:::image type="content" source="./media/serverside-conversion-revised.png" alt-text="Screenshot of the URL that is generated when you export the pixel.":::-->

## Add parameters to a server-side pixel call

You can add the following parameters to any SSPX call:

- `order_id`
- `value`
- `other`

To use these parameters, you must insert them into the query string before the `sspdata` parameter. For more details about these parameters, see [Conversion Pixels Advanced](./conversion-pixels-advanced.md).

The following is an example of a server-side conversion pixel call with additional parameters:

```
https://sspx-router.adnxs.com/sspx?id=25619&order_id=1234&value=5678&sspdata=ams1AAAAAAAAkQC8rFPulI3JKKU9tUKckv1Oj1WFMAAAAAGULAAA3AAAAUQIAAD4AAA 
```

> [!NOTE]
> The sspx handler is supported over only in secure (https://secure.adnxs.com/sspx) mode.

## Test a server-side pixel

1. Serve yourself a line item on a test page using a test placement. The line item must include a landing page with the SSP token.

1. Select the ad and see the token populate in the URL.

1. Copy the token from the http header and fire it back to Microsoft Advertising using the command line. The call for this looks like

    ```
    curl --verbose -L 'https://sspx-router.adnxs.com/sspx?id=78874&sspdata=nym1CJjYiJ3oq6LkMxACGIHey7vM0vGDRyIJMTAuMS4xMi42KAE.' 
    ```

    > [!NOTE]
    > - `id` is the pixel ID from Microsoft Advertising.
    > - `sspdata` is the populated `${SSP_DATA}` token; the length of this string is susceptible to change.

## Gotchas

- The sspx-router call when a user converts often includes a 302 redirect. The redirect must be followed for a conversion to be logged. When using the command line tool, cURL, be sure to include ""-L command in the call to allow the redirect.

- Server-side pixels cannot be used to add or remove users from segments. However, a normal, client-side pixel can add or remove users from segments; see [Conversion Pixels Advanced](./conversion-pixels-advanced.md).

- The `sspdata` parameter must be the last parameter listed in the conversion call sent from the attribution server to Microsoft Advertising.

- Server-side pixel data tokens typically have a period at the end, which must be included in calls.

## Investigations

To investigate issues or discrepancies with server-side pixels, Microsoft Advertising must be provided with verbose logs of the pixel fires because these calls provide the information needed to do an investigation.

## Alternate use case: Post-view conversions

The steps are the same as above, but in Step 4, you will add the macro to an impression tracking pixel instead of the creative's landing page URL:

:::image type="content" source="./media/pixels.png" alt-text="Screenshot showing a macro being addded to an impression tracking pixel instead of the creative's landing page URL.":::

Note that with this method, you will have an `SSP_DATA` token for every single impression rather than for only clicks.

## Related topics

- [Create a Conversion Pixel](./create-a-conversion-pixel.md)
- [Export Conversion Pixels](./export-conversion-pixels.md)
- [Conversion Attribution](./conversion-attribution.md)
