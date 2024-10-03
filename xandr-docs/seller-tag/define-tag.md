---
title: Define Tag
description: In this article, learn how the Define Tag is utilized to establish parameters for an ad placement.
ms.custom: seller-tag
ms.date: 10/28/2023
---

# Define Tag

This function defines parameters for an ad placement. Note that no more than 12 placements should be specified per page. Returns a `Tag` `object` that can be used later after defining.

```
defineTag({params})
```

## Parameters

The parameters listed below can be sent as arguments in the function.

| Parameter | Type | Description |
|:---|:---|:---|
| `member` | Number | The member ID for the placement (overrides global setting from `setPageOpts()`). |
| `invCode` | String | The placement code for this placement. |
| `tagId` | Number | The placement ID for the placement. |
| `sizes` | Array of numbers | One or more placement sizes in the format `[300,250]` ({{height, width}}) for a single size and `[[300,250],[728,90]]` for multiple sizes.<br>If more than one size is specified, the first is the placement size and the rest are promo sizes.<br><br> **Note:** Either `sizes` or `sizeMapping` is allowed per ad slot, not both. |
| `sizeMapping` | Array of objects | Specifies a set of sizes based on a minimum viewport size. This allows a seller to set which sizes should be used based on the size of the viewport. If the viewport size is smaller than the smallest `minWidth` provided, no ad will be requested for the ad slot. Sizes are passed in the format `[300,250]` for a single size and `[[300,250],[728,90]]` for multiple sizes.<br>Each object in the array contains two parameters :<br> - `minWidth`: Specifies the minimum width of the viewport. For example, `minWidth: 1024`.<br> - `sizes`: Specifies the size(s) of the ad. For example, `sizes:` `[[300,250],[300,600]]`.<br><br>**Note:** Either `sizes` or `sizeMapping` is allowed per ad slot, not both. |
| `targetId` | String | The unique identifier of a specific ad slot, created by the publisher/seller. Corresponds to a `div` tag in the body of the page where the ad should appear. The `div` tag's `id` should be set to the same value as the `targetId`. |
| `forceCreativeId` | Number | Specifies the ID of a creative that should be forced to appear in this placement. Forcing a creative allows you to preview an ad on a site, perform testing or certification, and create tear sheets.<br><br>**Tip:** Creatives can also be forced in the query string of the website URL in the format `ast_override_[parameter]=[value]:[creative_id]`, where you will replace `parameter`, `value`, and `creative_id` as needed. You may pass in multiple `[value]:[creative_id]` combinations separated by a comma (e.g. `https://test.example.com/demo.html?ast_override_ index = 2 : 40611315 , 3 : 40611316`).<br>You may choose one of the following options for the `parameter`.<br><br>**div**<br>Specifies a target div ID of the ad slot to override. In `value`, enter the div ID you would like to force `creative_id` into.<br>To override the div with ID `apn_ad_slot_1` with creative `40611315`:<br>`https://test.example.com/demo.html?ast_override_div=apn_ad_slot_1:40611315`<br><br>**index**<br>Specifies the index number of the ad slot to override, starting from `0`. In `value` enter the index number you would like to force `creative_id` into.<br>To override the 3rd defined placement with creative `40611315`:<br>`https://test.example.com/demo.html?ast_override_index=2:40611315`<br><br>**tag_id**<br>Specifies the tag ID that of the ad slot to override. In `value` enter the tag_id you would like to force `creative_id` into. If the size of the ad slot and creative do not match, the creative will still be rendered but a warning message will be displayed. The creative would not serve in this ad slot in a live auction.<br>To override `tag_id 8011968` with creative `40611315`:<br>`https://test.example.com/demo.html?ast_override_tag_id=8011968:40611315`<br><br>**inv_code**<br>Specifies the inventory code that of the ad slot to override. In `value` enter the inventory code you would like to force `creative_id` into. If the size of the ad slot and creative do not match, the creative will still be rendered but a warning message will be displayed. The creative would not serve in this ad slot in a live auction.<br>To override `40611315`: with creative `40611315`:<br>`https://test.example.com/demo.html?ast_override_inv_code=9123450:40611315`<br><br>**Tip:** The query string parameters listed above will override any value specified in the `forceCreativeId` parameter of the ad tag. |
| `allowSmallerSizes` | Boolean | Indicates whether smaller ad sizes than defined on `sizes` are allowed. |
| `allowedFormats` | Array of strings | Indicates the desired formats. Options include ['video', 'banner', 'native, 'audio']. If `allowedFormats` are invoked, it will override the media types assigned on the placements' settings in Microsoft Monetize. Do not invoke `allowedFormats` to use an ad format, such as `interstitials`, that is not included in the predefined options. |
| `rendererOptions` | Object | Specifies one or more options that can be passed into the renderer for custom rendering. |
| `position` | String | Identify the placement as above or below the fold. Possible values: `above` or `below`. |
| `disablePsa` | Boolean | Indicates whether this placement should disable PSAs from being shown. |
| `nobidIfUnsold` | Boolean | Indicates that a blank ad should be returned if the placement is not sold rather than a default ad or PSA. |
| `keywords` | Object | A set of key/value pairs applicable to this placement. Query string segments are defined by key/value pairs in this object. Keywords that contain hyphens must be surrounded by single quote marks. Best practice is to always enclose keywords in single quotes. A maximum of 100 key/value pairs can be defined per tag.<br>To pass custom data use any of the keywords:  `pt1, pt2, pt3, pt4, pt5, pt6, pt7, pt8, pt9`.<br><br>These keywords can be used to pass custom data through managed placements to managed 3rd-party creatives, for example, `pt1=products:ipad,ios,iphone`. |
| `trafficSourceCode` | String | Specifies the third-party source of this impression. |
| `alwaysUseXDomainIframe` | Boolean | Indicates whether the ad creative should be loaded into a cross-domain iframe. This will prevent data leakage and does not allow the creative to access the parent page directly.<br><br>**Note:** This parameter has been deprecated in favor of `enableSafeFrame`. |
| `privateSizes` | Array of numbers | The additional sizes that allowed to serve only for custom deals or packages (when private sizes are allowed by the deal or package). In the format `[300,250]` for a single size and `[[300,250],[728,90]]` for multiple sizes. |
| `supplyType` | String | Indicates the type of supply for this placement. Possible values are `mobile_web`, `mobile_app`, or `web`. |
| `pubClick` | String | Specifies a publisher-supplied URL for third-party click tracking. This is just a placeholder into which the publisher can insert their own click tracker. This parameter should be used for an unencoded tracker. This parameter is expected to be the last parameter in the URL. Note that the click tracker placed in this parameter will only fire if the creative winning the auction is using Xandr click tracking properly. For example, `pubClick=https://click.adserver.com/`. |
| `reserve` | Number | Specifies the reserve price for this inventory. This parameter will override a preset price and will set the hard floor if Yield Management is not being used. Price is assumed to be in the publisher's currency. For example, `reserve=5.00`.<br><br>**Note:** This option is not available from Microsoft Monetize, and must be appended to the placement tag manually. |
| `extInvCode` |  String | Specifies a predefined value passed via the `ext_inv_code` field of the request body that can be used in reporting. The value must be entered into the system before it is logged. For more information, see [External Inventory Code Service](../digital-platform-api/external-inventory-code-service.md). For example, `ext_inv_code='10039'`. |
| `native` | Object | A native ad is a collection of individual assets. These could be a title, a description, or an image. This is an optional parameter. You do not need to specify this in `defineTag`. Any field in the `native` object configured as `{required:true}` will be required on the bid response object. If not present, the bid is not added to the auction. The [native ad resources](#native-ad-resources) are listed below. |
| `externalImpId` | String | Specifies the unique identifier of an externally generated auction. For example, `externalImpId:'bacbab02626452b097f6030b3c89ac05'`. |
| `enableSafeFrame` | Boolean | Specifies whether this placement will be served in a SafeFrame container. For more information, see [SafeFrame API Reference](safeframe-api-reference.md). |
| `setSafeFrameConfig` | Boolean | Allows configuration of SafeFrame, a managed iframe that provides additional consumer protection and publisher control beyond that provided by a standard iframe. For more information, see [SafeFrame API Reference](safeframe-api-reference.md). |
| `initCollapsed` | Object | Initializes the ad iframe at zero size. The only option for the `expandBy` field is creative. This setting gives the creative the responsibility of expanding the ad slot by calling resizeAd function. |
| `prebid` | Boolean | Indicates that the tag being requested is for a header bidding or prebid auction. This will return the cpm on the adObj `adObj.cpm`. However, the ad will not be rendered. It is assumed that another ad server will render the ad if this bid wins. |
| `usePmtRule` | Boolean | Indicates whether payment rules should be applied to a bid before sending the bid to the ad server. Default value is false. |
| `resizeAdParentDiv` | Boolean | Setting this property to true will force the Parent Div container of the Ad creative to resize. This is particularly useful when resizing banner safeframe creatives when the parent div doesn't resize in some environments. By default, this option is turned off. <br><br>**Note:** The value set here can be overridden during a resizeAd call. For more information, see resizeAd page. |
| `globalPlacementId` | String | Provides a way for publishers to specify their own global publisher identifier to represent the placement. |
| `renderingManagement` | Object | An object that specifies values for rendering related features, which influence how ads are rendered onto a webpage. These options also be set at the setPageOpts level to apply to all ad slots on the page.<br> - **`insertWrapperDiv`**: When enabled, AST adds an additional div element between the main AST `utif` div and the AST iframe (or safeframe) container for all ad slots. This option is useful for publishers who wish to customize or control the contents of the ad container further without modifying the main div container.<br>**Default:** false<br><br> - **`sandboxAdIframe`**: When enabled, AST adds and populates the HTML sandbox attribute for the AST iframe (or safeframe) container for all ad slots using the values from the appropriate `sandboxAttributes` parameter.<br>**Default:** false<br><br> - **`sandboxAttributes`**: The values of these attributes are applied to the HTML sandbox attribute for the AST iframe (or safeframe) ad containers when the appropriate `andboxAdIframe` setting is set to true. For suitable values to include in this array, see the HTML sandbox documentation. If enabled, it is advised to include at least `allow-same-origin` and `allow-scripts` to ensure that the contents of the iframe may function properly (omitting these values may result in some warnings in the browser console). |
| `rewardedAds` | Boolean | Indicates whether the user receives a reward for viewing the ad. The default is false. Set to true if the user receives a reward, otherwise set to false.|
|`msft_tag`| Object | For more information, see [Set Page Options - Microsoft Object](https://microsoftapc.sharepoint.com/teams/TechComm/SitePages/Set-Page-Options---Microsoft-Object.aspx#msft-object).|

### Native Ad resources

#### custom

Can contain two sub-objects named **data** and **images**.  See below for further details on these properties.

#### data

An array of objects with the following available fields:

- `type: <integer>` note - Must be greater than 500.
- `required: <true | false>`
- `max_length: <integer>`

#### image

An array of object with the following available fields:

- `type: <integer>` - Must be greater than 500
- `required: <true | false>`
- `size: {width: <integer>, height: <integer>}`
- `min_size: {width: <integer>, height: <integer>}`
- `mimes: [<string>, <string2>, ...]`

#### title

`required: <true | false>`

`max_length: <number>`

Where field marked `required: true` will be required on the bid response object. If `max_length` is specified, responses for this fields must not exceed the `max_length` number.

#### body

`required: <true | false>`

`max_length: <number>`

Where field marked `required: true` will be required on the bid response object. If `max_length` is specified, responses for this field must not exceed the `max_length` number.

#### image

```
required: <true | false>
sizes: [
{ width: <number>, height: <number> }
]
aspect_ratios: [
{min_width: <number>, min_height: <number>, ratio_width: <number>, ratio_height: <number>}
]
```

Where field marked `required: true` will be required on the bid response object.

If `sizes` is specified, the image response must exactly match the given width and height dimensions.

If `aspect_ratios` are specified as an alternative to sizes, the image must at least match the minimum height/width dimensions and `aspect_ratios` value defined.

#### icon

```
required: <true | false>
sizes: [
{ width: <number>, height: <number> }
]
aspect_ratios: [
{min_width: <number>, min_height: <number>, ratio_width: <number>, ratio_height: <number>}
]
```

Where field marked `required: true` will be required on the bid response object.

If `sizes` is specified, the image response must exactly match the given width and height dimensions.

If `aspect_ratios` are specified as an alternative to `sizes`, the image must at least match the minimum height/width dimensions and `aspect_ratios` value defined.

#### sponsoredBy

`required: <true | false>`

`max_length: <number>`

Where this field marked `required: true` will be required on the bid response object. If `max_length` is specified, responses for this fields must not exceed the `max_length` number.

#### cta

`required: <true | false>`

Where this field is marked `required: true`, the parameter will be required on the bid response object.

#### clickUrl

`required: <true | false>`

Where this field is marked `required: true`, the parameter will be required on the bid response object.

#### privacySupported

`<true | false>`

If true, the publisher supports a privacy link. The privacy link will be sent to the publisher in the bid response.

#### video

`required: <true | false>`

`min_duration: <number>`

`max_duration: <number>`

Where field marked `required: true` will be required on the bid response object. `min_duration` and `max_duration` values are specified in milliseconds.

`min_duration` default = 0

#### desc2

`required: <true | false>`

#### rating

`required: <true | false>`

#### displayUrl

`required: <true | false>`

#### likes

`required: <true | false>`

#### downloads

`required: <true | false>`

#### price

`required: <true | false>`

#### salePrice

`required: <true | false>`

#### rating

`required: <true | false>`

#### phone

`required: <true | false>`

#### address

`required: <true | false>`

## Example 1

**Format:**

```
    
native: {
title: {required: true},
body: {required: false, max_length: 300},
image: {required: true},
icon: {
required: false,
sizes: [{ width: 50, height: 50 }]
},
sponsoredBy: {required: true},
cta: {required: true},
clickUrl: {required: true},
privacySupported: true,
desc2: {required: true},
rating: {required: false},
displayUrl: {required: false},
likes: {required: true},
downloads: {required: false},
price: {required: false},
salePrice: {required: false},
rating: {required: true},
phone: {required: false},
address: {required: false},
    custom: {
        data: [{
            type: 501,
            required: false
        }],
        images: [{
            type: 505,
            required: false
        }]
    }
}


```

## Example 2

```
apntag.defineTag({
        member: 958,
        invCode: 'ABC1234',
    alwaysUseXDomainIframe: true,
    tagId: 123456,
        sizes: [[300,250]],     // only 1 of sizes or sizeMapping is allowed
        sizeMapping: [          // only 1 of sizes or sizeMapping is allowed
        {
            "minWidth": 1024,
                "sizes": [[300,250],[300,600]]
        },
        {
                "minWidth": 400,
                "sizes": [[320,50]]
        }
        ],
        targetId: 'apn_ad_slot_1',
    forceCreativeId: 23456786,
    allowSmallerSizes : true,
        allowedFormats : ['banner', 'video'],
    initCollapsed: { expandBy: 'creative' },
        position : 'above',
        disablePsa : true,
    noBidIfUnsold: true,
    keywords: {
                'genre': ['rock', 'pop']
    },
        trafficSourceCode: 'ssp1', 
    privateSizes : [[300,600]],                          // coming soon
        supplyType : 'mobile_web',
        pubClick : 'http://pubc1.com',           // coming soon
        pubClickEnc : 'http%3A%2F%2Fpubcl.com',  // coming soon
        reserve : 5.01,
        extInvCode : 'extcode1',
    externalImpId: 'bacbab02626452b097f6030b3c89ac05',
    enableSafeFrame: true,
        safeframeConfig: {
                allowExpansionByPush:true,
        allowExpansionByOverlay:true
    },
    rendererOptions: {
                playerTechnology: [
                        "html5",
                        "flash"
                ],
                adText: "Ad",
                showMute: true,
                showVolume: true,
                showProgressBar: true,
                allowFullscreen: true,
                skippable: {
                        videoThreshold: 15,
                        videoOffset: 5,
                        skipLocation: "top-left",
                        skipText: "Video can be skipped in %%TIME%% seconds",
                        skipButtonText: "SKIP"
                }
        },
      
      usePmtRule : false,
      resizeAdParentDiv: true,
      globalPlacementId: 'testId123',
      renderingManagement: {
               insertWrapperDiv: true,
               sandboxAdIframe: true,
               sandboxAttributes: ['allow-same-origin', 'allow-scripts', 'allow-presentation']
              }
        });
```
