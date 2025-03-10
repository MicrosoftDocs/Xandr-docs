---
title: Onboarding Audio Supply
description: Leran how to modify and adjust placement settings to accept audio creatives and how to export and test placement tags. 
ms.date: 10/28/2023
---

# Onboarding audio supply

This page explains how to modify placement settings to accept audio creatives and how to export and test placement tags. For a complete walkthrough of placement object setup, see [Create a Placement](create-a-placement.md).

## Onboarding audio placements

1. From the **Publishers** tab, navigate to **Publishers** > **Inventory Manager**.
1. If prompted, select a publisher, click the **Create New** button, and select **Placement**.
1. In the **Allowed Media** section, select **Audio**.

> [!NOTE]
> When Audio is selected, no other media types are allowed.

## Export placement tag

When you [export the placement tag](export-placement-tags.md) for a placement that allows VAST audio creatives, the placement tag generated is a URL. In the URL, we automatically change `/ttj` to `/ptv` to ensure that ad calls will return the XML required by your publisher's video player to serve the desired creative. The end result
looks something like this:

```
https://ib.adnxs.com/ptv?id=1234
```

Once you have the tag, make sure to append the placement tag with the parameters below before implementing. Make sure that you copy the URL into the audio player rather than place it directly on the page.

**Append placement tag parameters:**

The following placement tag parameters are highly recommended. You should append all available parameters in order to comply with platform policies and maximize revenue opportunity.

| Parameter | Type | Description |
|---|---|---|
| `appid` | string | This string is used to identify a mobile app running on Android or iOS devices.<br> - On Android, this is the app's package name. It's formatted as `com.example.helloworld`.<br> - On iOS, this is the app's iTunes ID. It's formatted as `123456789`.<br>Many buyers set campaign targeting and reporting based on `appid`. Failing to supply a correct `appid` will make your inventory unattractive to these buyers. Therefore, passing this field is **strongly recommended** when `supply_type` is set to `mobile_app`.<br>**Note**: This is what our Mobile SDKs do when they request an ad.<br>To find the `appid` for a particular Android or iOS app, find the app's detail page in Google Playstore or App Store. The easiest way is to do a web search. The URL of the app store's detail page will show the `appid`. |
| `idfa` | string | The Apple advertising identifier for iOS devices. |
| `aaid` | string | The Google advertising identifier for Android devices as retrieved from Google Playstore. |
| `adid` | string | The Windows advertising identifier for Windows devices. |
| `ip` | string | IP address of the device making the ad request, e.g., `207.237.150.246`.<br>If not specified for `/ptv` calls, the IP address passed via HTTP headers is used for geo detection. |
| `loc` | string | The user's location expressed in latitude and longitude, in the format: `snnn.ddddddddddddd,snnn.ddddddddddddd`. Up to 13 decimal places of precision are allowed. |

**Example of a placement tag**:

```
https://ib.adnxs.com/ptv?id=10928372&appid=919288199&idfa=939828182082837&ip=100.10.102.19.&loc=-79.1209911,-10.9900099
```

## Testing placement tags

If you do not have access to a test page, you can use an online VAST validator to determine if the placement tag is functioning properly. There are several available online, including at [VAST Inspector](https://googleads.github.io/googleads-ima-html5/vsi/).

## Recording impressions

VAST impressions are recorded after the first frame serves, per the [IAB guidelines](https://www.iab.com/guidelines/iab-new-ad-portfolio/). If you test VAST by loading the URL in a browser, no impressions will be recorded. It is only when the VAST response is parsed by an audio player and the VAST impression trackers are called that the impression is recorded.

## Related topics

- [Create a Placement](create-a-placement.md)
- [Assign a Default Creative to a Placement](assign-a-default-creative-to-a-placement.md)
- [Export Placement Tags](export-placement-tags.md)
- [Placement Tag Parameters](placement-tag-parameters.md)
