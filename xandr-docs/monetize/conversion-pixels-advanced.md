---
title: Microsoft Monetize - Conversion Pixels Advanced
description: Define advanced options for conversion pixels, including creation and export details. Explore available advanced features.
ms.date: 10/09/2024
---

# Microsoft Monetize - Conversion pixels advanced

When creating and exporting conversion pixels, there are some advanced options available.

> [!TIP]
> Most of the below options can be performed during pixel export in Monetize. For details on pixel export, see [Export Conversion Pixels](export-conversion-pixels.md). You cannot use the `other` parameter during pixel export.

## Use secure pixels

The UI allows you to create secure pixels, which should be used on HTTPS webpages. You can choose secure pixels as an option in Monetize when you export a pixel. Or you can convert a pixel manually by making two changes:

1. Replace "http" with "https".
1. The sub-domain should be "ib.adnxs.com".

> [!WARNING]
> On a secure page, only **secure** pixels can be used. In addition, non-secure pixels can only be placed on an **non-secure** page.

## Segment users once they have converted

You can add or remove a user from one or more segments at the same time the conversion pixel is fired. One case in which you might want to segment users after conversion is if you do not want to advertise to users who have already purchased a product. Once a user has converted and been added to a segment, you can exclude that segment from being targeted in your line item or campaign. Please note that whether or not a user is subject to segment actions is independent of whether or not the conversion was attributed.

This pixel adds the user to two segments, and removes them from one:

```
 <img src="media/px?id=8371&seg=12192,12304&remove=23145&t=2" width="1" height="1" /> 
```

> [!NOTE]
> There are two ways to add a user to a segment after a conversion:
>
> 1. Add a user at the same time the conversion pixel is fired.
> 1. Add a Segment pixel as a piggyback to the conversion pixel.
>
> It is preferable to use the first scenario, keeping the conversion and segment pixel as one call, over having the segment be a piggy back. There are several reasons for this. First only one call, rather then two, is made as the page loads reducing latency. Second if the user clicks away from the page before it fully loads it is possible for the conversion pixel to fire but not the piggybacked segment causing a mismatch. If you use the first scenario, you will not have a mismatch
> assuming you are not adding users to the segment some place else.

## Use conversion pixel parameters

### Order ID/SKU: order_id

You can pass in an order ID or SKU in your pixel and then see this data in conversion reporting. For example, the user sees a ProStarr Sportswear ad, clicks on it, and orders a t-shirt with SKU 124252334. The advertiser populates the pixel with order_id=124252334, which then flows into the reporting tables. You can put letters and numbers in an order ID and there is a 36 character limit.

You can report on this data using the [Advertiser Attributed Conversions Report](advertiser-attributed-conversions-report.md) or the [Log-Level Data Feeds](../log-level-data/log-level-data-feeds.md) if you subscribe to our Log-Level Data.

```
<img src="media/px?id=1&order_id=[ORDER_ID]&t=2" width="1" height="1" /> 
```

## Dynamic revenue values: value

You can pass in dynamic revenue values which will show up in reporting as post-click and post-view revenue. This is most often used to pass in the advertiser's revenue and keep it separate from the network's revenue. To see these dynamic values in reporting, select "PC/PV Revenue" as a **dimension** on your Attributed Conversions report, or select "Post View Revenue" and "Post Click Revenue" as **metrics** in your Analytics Report. Note that the "Revenue" metric in Analytics reports will not be affected by dynamic revenue values - it is static and pulled from the Post-view revenue and Post-click revenue values entered at the Line Item level. Note that for a CPA line item or campaign, we cannot optimize to a moving target, so we will optimize to the static value entered at the line item level.

```
<img src="media/px?id=1&value=[REVENUE]&t=2" width="1" height="1" /> 
```

> [!WARNING]
> The revenue value passed in must be a purely numerical value in order for it to be properly logged in reporting. For example, 10 would be valid, but $10 would not.

## Redirect URL/Piggybacking: redir

You can piggyback off the Microsoft Advertising conversion pixel and notify your internal or third-party server about conversion events. When you create a conversion pixel in Monetize, you can input the URL of your pixel and mark it as image or JavaScript. Please note that following restrictions:

- Image pixels can only piggyback off other other image pixels, and JavaScript pixels can only piggyback other JavaScript pixels.

- Image pixels can only have one piggyback pixel. If you need to piggyback multiple pixels, be sure to use a JavaScript pixel.

- There are no character limits to piggybacked pixels in Microsoft Monetize, but browser/server URL limits
  may apply.

  ```
  <img src="media/px?id=1&redir=[REDIRECT_URL]&t=2" width="1" height="1" /> 
  ```

## Other external data: other

You can include an extra field to pass into your pixel and then see this data in conversion reporting. This cannot be done using the "Export Pixels" pane, so you need to manually include this parameter in your pixel tag. You can include letters and numbers in this additional field and there is a 20 character limit.

You can report on this data using the [Advertiser Attributed Conversions Report](advertiser-attributed-conversions-report.md) as well as the [Log-Level Data Feeds](../log-level-data/log-level-data-feeds.md), if you subscribe to our Log-Level Data Feeds.

```
<img src="media/px?id=1&other=[EXTERNAL_DATA]&t=2" width="1" height="1" /> 
```

## Privacy considerations

To comply with privacy regulations, the inclusion of privacy signals in URL parameters is mandatory in certain geographical regions, such as the European Economic Area (EEA). Clients must provide either TCF parameters or the consent parameter to ensure personal information is processed correctly, allowing services to function as intended.

When working with CMPs that support TCF signals, clients must include the parameters `gdpr=1` (when GDPR applies) and `gdpr_consent=<CONSENT-STRING>` in the respective URLs. These values must be dynamically set based on the customer's privacy choices. If TCF signals are not available, the consent parameter must be used, where `1` indicates customer consent and `0` indicates consent denial.

It is the client's responsibility to ensure that these parameters reflect the customer's privacy preferences. Failure to provide the correct signals will prevent the processing of the request and might impact service functionality.

Example `img` tag with TCF Consent parameters:

```
<img src="https://ib.adnxs.com/px?id=1234&t=2&gdpr=1&gdpr_consent=XXX" width=1 height=1></img>
```

Example `img` tag with binary consent parameters for denied consent:

```
<img src="https://ib.adnxs.com/px?id=1234&t=2&consent=0" width=1 height=1></img>
```

Example `img` tag with binary consent parameters for granted consent:

```
<img src="https://ib.adnxs.com/px?id=1234&t=2&consent=1" width=1 height=1></img>
```

### Related topics

- [Create a Conversion Pixel](create-a-conversion-pixel.md)
- [Export Conversion Pixels](export-conversion-pixels.md)
- [Reporting on Conversions](reporting-on-conversions.md)
- [Server-Side Conversion Pixels](server-side-conversion-pixels.md)
