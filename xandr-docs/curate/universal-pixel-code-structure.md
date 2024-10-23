---
title: Microsoft Curate - Universal Pixel Code Structure
description: Learn the code structure of the universal Pixel for general and custom event deployments on advertiser websites.
ms.date: 11/16/2023
---

# Microsoft Curate - Universal Pixel code structure

The general Universal Pixel code to be deployed in the `<head>` tag on each page of the advertiser website is different from the pixel code required for standard and custom events, which is deployed only on pages of interest.

## Universal Pixel initialization code

The following code sample shows the structure of the Universal Pixel code that you can deploy in the `<head>` tag of an advertiser's web page. You should include the Universal Pixel initialization script only once per page. Note that the `PageView` event is the default event for page view tracking, and is included on all pages.

The pixel code always includes a `<noscript>` version for browsers that don’t accept JavaScript.

```
<script> 
!function(e,i){if(!e.pixie){var a=e.pixie=function(e,i,n){a.actionQueue.push({action:e,actionValue:i,params:n})};a.actionQueue=[];var n=i.createElement("script");n.async=!1,n.src="//acdn.adnxs.com/dmp/up/pixie.js";var t=i.getElementsByTagName("head")[0];t.insertBefore(n,t.firstChild)}}(window,document); 
         pixie('init', 'a58fde5b-f991-474f-9456-b2509ba30042'); 
         pixie('event', 'PageView'); 
</script> 

<noscript>
<img width="1" height="1" style="display:none;" src="//ib.adnxs.com/pixie?pi=a58fde5b-f991-474f-9456-b2509ba30042&e=PageView&script=0" />
</noscript> 
```

## Event code

The following code sample shows the script code for an `AddToCart` event with additional parameters appended. You should place code for standard and custom events like this only on relevant pages, such as on a conversion landing page.

```
<script> 
        pixie('event', 'AddToCart'); 
</script> 

<noscript>
<img width="1" height="1" style="display:none;" src="//ib.adnxs.com/pixie?pi=a58fde5b-f991-474f-9456-b2509ba30042&e=AddToCart&ii=product_5&itp=apparel&in=shirt&script=0"/>
</noscript>
```

## Related topics

- [Standard Events and Parameters](./standard-events-and-parameters.md)
- [Create Custom Events and Parameters](./create-custom-events-and-parameters.md)
