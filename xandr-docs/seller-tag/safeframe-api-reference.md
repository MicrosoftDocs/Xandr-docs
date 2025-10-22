---
title: SafeFrame API Reference
description: SafeFrame—API-enabled iframe ensures secure communication, data safety, and efficient interaction with Microsoft's sf-ext.js on a secondary domain.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: seller-tag
ms.author: shsrinivasan
---

# SafeFrame API reference

SafeFrame is a managed, API-enabled iframe. It opens a line of communication between the publisher page content and the iframe-contained external content, such as ads. It operates in a secondary domain provided by the Host, and ideally established on a content delivery network (CDN). This secondary domain serves as an agnostic processing space between the host and external party. Any information that the External Party needs to know about the Host domain is accessed by request, using the SafeFrame API. This API is used to communicate between the host site and external content, using Xandr's solution for SafeFrame: sf-ext.js. This was built with AST, but is delivered as a separate component.

SafeFrame feature has many benefits. This includes consumer protection, publisher control and efficiency.

## SafeFrame and video

For video customers, SafeFrame is currently only supported for Outstream video placements. If you decide to use this functionality, make sure that you follow the guidelines for setting up on-page tags for outstream video in the [Microsoft Advertising Help center](../index.yml).

## Implementation and functions

- This pertains to the API that is accessible by creatives.
- The following functions are available for communication. These functions are implemented as per [IAB Spec](https://www.iab.com/wp-content/uploads/2014/08/SafeFrames_v1.1_final.pdf).

| Function | Description |
|--|--|
| `$sf.ext.collapse` | The collapse function collapses the SafeFrame container to the original geometric position. |
| `$sf.ext.expand` | The expand function expands the SafeFrame container to the specified geometric position, allowing intermediary expansions. It supports expansion in both push modes. |
| `$sf.ext.geom` | The geom function enables an exchange of geometric dimensions and location of the SafeFrame container. This includes its content in relation to the browser or application window, and the screen boundaries of the device in which the host content is being viewed. |
| `$sf.ext.inViewPercentage` | Returns the percentage of area that a container is in view on the screen as a whole number between 0 and 100. This is as per the [IAB Spec](https://www.iab.com/wp-content/uploads/2014/08/SafeFrames_v1.1_final.pdf). Please reference this for additional detail. |
| `$sf.ext.register` | The external party register function registers the SafeFrame platform to accept SafeFrame external party API calls. The external party creative declares the initial (collapsed) width and height. In addition to width and height, this function can also define a callback function, which informs the external content about various status details. |
| `$sf.ext.status` | The status function returns information about the current state of the container. States are: expanded, expanding, collapsed, collapsing |
| `$sf.ext.supports` | The supports function returns an object with keys representing what features have been turned on or off for a specific: Expansion, Push mode, Read cookie, Write cookie container. |
| `$sf.ext.winHasFocus` | Returns whether or not the browser window or tab that contains the SafeFrame has focus, or is currently active. |
  
## apntag.defineTag({param})

Param '`enableSafeFrame`' is added to `defineTag` which delivers the creative in SafeFrame container.

### Parameters

| Name | Type | Description |
|--|--|--|
| `enableSafeFrame` | boolean | Delivers the creative in SafeFrame container. |
| `setSafeFrameConfig` | boolean | Allows configuration of SafeFrame, a managed iframe that provides additional consumer protection and publisher control beyond that provided by a standard iframe. |

### Example

``` 
 
var tag = apntag.defineTag({
            enableSafeFrame : true,
            tagId : 10107529, //10066308,
            sizes : [[300,250]],
            targetId: 'apn_ad_40954389053',
           //new field
            safeframeConfig: {
              allowExpansionByPush:true,
              allowExpansionByOverlay:true
            }
          //end new field
        });
```

## apntag.setSafeFrameConfig({param})

This function can be used to configure SafeFrame. We have given two options, `allowExpansionByPush` and  `allowExpansionByOverlay` for SafeFrame expand API. Configuration by this function will change the return values of `$sf.ext.supports` function. Publisher can revoke expand permissions from here.

### Parameters

| Name | Type | Description |
|--|--|--|
| `allowExpansionByPush` | boolean | Host can toggle expansion by push using this param. |
| `allowExpansionByOverlay` | boolean | Host can toggle expansion by overlay using this param. |

### Example

``` 
apntag.setSafeFrameConfig({
        "allowExpansionByPush" : true,
        "allowExpansionByOverlay" : true
});
```

## apntag.setPageOpts({param})

Parameter `enableSafeFrame` is added to `setPageOpts` function. This parameter enables SafeFrame and serves all the all ads in SafeFrame container.

### Parameter

| Name | Type | Description |
|--|--|--|
| `enableSafeFrame` | boolean | Deliver all creative in safeframe container. |

### Example

``` 
apntag.setPageOpts({
        //other setPageOpts params
        "enableSafeFrame" : true
});
```

> [!NOTE]
> Page level functions: All AST functions will be page-level. Creative functions: all $sf.ext functions will be called by creative.

## Safeframe API function examples

The following examples show how to use the API functions for SafeFrame.

## $sf.ext.register(width, height, callbackFn)

The SafeFrame External API register function registers the function to accept SafeFrame external party API calls. External party creative declares the initial (collapsed) width and height and callback function, which informs the external content about various status details.

### Parameters

| Name | Type | Description |
|--|--|--|
| `callbackFn` | function | Function to be called on any operation. |
| `height` | number | Initial height of the creative |
| `width` | number | Initial width of the creative |

### Example

``` 
var statusUpdate = function(status) {
        if(status === 'expanded') {
                //do something
        } else if(status == 'collapsed') {
                //do something
        }
}
$sf.ext.register('300','250',statusUpdate);
```

## $sf.ext.supports()

This function returns an object with keys representing which features have been turned on or off for this particular container.

### Example

``` 
var supports = $sf.ext.supports();
if(supports['exp-ovr']) {
        //expansion by overlay is supported so expand can be called safely with overlay param
}
if(supports['exp-push']) {
        //expansion by push is supported so expand can be called safely with push param
}
```

## $sf.ext.geom()

This function gets the space available around the `targetDiv` to expand the SafeFrame container. It returns the following object:

### Example

``` 
 var g = $sf.ext.geom();
 if (/*check available space to expand before calling expand function*/) {
      $sf.ext.expand(obj);
 }
```

### Scroll Position Example

``` 
 var geom = $sf.ext.geom();
 geom.anx.scrollTop; // scrollTop
 geom.anx.scrollLeft; // scrollLeft
```

This takes into account the eventual scroll position of intermediary same-domain iframe, when AST is itself in an iframe.

> [!NOTE]
> `geom.anx` is a proprietary extension to the safeframe specification.

## $sf.ext.expand({params})

This function expands the SafeFrame container to the specified geometric position. All the params are compulsory, so if you are not going to expand left than keep 'left' : 0

### Parameters

| Name | Type | Description |
|--|--|--|
| `b` | number | The new bottom coordinate (y+height) relative to the current top coordinate(y+height). |
| `l` | number | The new left coordinate (x) relative to the current left coordinate. |
| `push` | boolean | Whether or not expansion should push the host content, rather than overlay. |
| `r` | number | The new right coordinate (x+width) relative to the current right coordinate(x+width). |
| `t` | number | The new top coordinate (y) relative to the current top coordinate. |

### Example

``` 
$sf.ext.expand({
        'l' : 0,
        'r' : 0,
        't' : 0,
        'b' : 500,
        'push' : true
});
```

## $sf.ext.collapse()

This function collapses the SafeFrame container to the original geometric position.

### Example

```
$sf.ext.collapse();
```

## $sf.ext.status()

This function returns the current state of the SafeFrame container. Possible States are `expanded`, `collapsed`, `ready`.

### Example

``` 
$sf.ext.status();
```
