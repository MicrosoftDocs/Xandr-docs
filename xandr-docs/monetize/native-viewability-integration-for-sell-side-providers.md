---
title: Native Viewability Integration for Sell-Side Providers
description: Explore Microsoft Advertising's viewability boost for Sell-Side Providers by configuring websites to modify viewability script payloads.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Native viewability integration for sell-Side providers

Native SSPs using OpenRTB can integrate with Microsoft Advertising native viewability measurement by configuring the website to modify the payload of the viewability script. You can integrate the script using direct access to the DOM ID or the classname, or use a CSS selector.

TheMicrosoft Advertising viewability script payload can be found in the `jstracker` field of the OpenRTB response, as defined in the [IAB specs](https://www.iab.com/wp-content/uploads/2016/03/OpenRTB-Native-Ads-Specification-1-1_2016.pdf). This payload contains the `;dom_id=%native_dom_id%` parameter, which can be replaced using any of the methods below.

## Use the DOM ID

To integrate using direct access to the DOM ID, populate `%native_dom_id%` with the ID of an HTML element that wraps the creative content. The native ad renderer will then overwrite the `%native_dom_id%` in the viewability script payload.

You can use any unique ID (newly created or already existing on the page) that's compliant with the HTML standard. For example, the following snippet shows the ID attribute applied to a `<div>` element.

```
  <div id="1234abcd">
  <!—native content-->
  </div>
```

The native ad renderer injects the script in the page, so that the Microsoft Advertising viewability script can retrieve the HTML element using `document.getElementById`.

## Pass a reference to DOM element (Compatible with shadow DOM)

In order to integrate using access to the creative HTML Element (the element that wraps the creative content), pass a reference of the DOM Element to the given variable `dom_elt_var`. This approach is particularly helpful when the creative HTML is housed within a Shadow DOM or nested Shadow DOMs.

**Example**:

```
  #shadow-root (open)
      <!-- native content -->
    

const creativeDOM1234 = document.getElementById("creative-sidebar-1").shadowRoot.querySelector("#native-creative-wrapper");  // Location of the creative inside Shadow DOM
window['creativeDOM1234'] = creativeDOM1234; // Attach the creative element to the window object
```

The native renderer then replaces `%native_dom_id%` with `;dom_elt_var=creativeDOM1234`.

```
newViewJsPayload = viewJsPayload.replace("%native_dom_id%", ";dom_elt_var=creativeDOM1234");
```
This method instructs the viewability script which element to measure, using a DOM reference to the element contained in `window`.

## Use a classname

To integrate by using access to a classname, add `anx_cr_loc` as an attribute on an HTML element that wraps the creative content to be rendered. The native ad renderer will then overwrite the `%native_dom_id%` in the viewability script payload.

For example, the following snippet shows the attribute applied to a `<div>` element.

```
<div class="anx_cr_loc">  
<!—native content -->
```

The native ad renderer removes `%native_dom_id%` from the payload using

```
newViewJsPayload = viewJsPayload.replace("%native_dom_id%", "");
```

and injects the viewability script element in the ad wrapping element directly after the creative content, as shown in the example.

```
<div class="anx_cr_loc">
<!—native content -->
<script src="//cdn.adnxs.com/appnexusviewabilityscriptpayload_url...">
</script>
```

## Use a CSS selector

To integrate using a CSS selector, find a stable selector that selects only your ad, and URL-encode it. For example, suppose you're using the following code:

```
 <div class="right">
 <div class="ad1">
 <!—native content -->
 </div>
 </div>  
```

You could use the selector `.right > .ad1` and encode it as `.right%20%3E%20.ad1`.

The native renderer then replaces the `%native_dom_id%` with `;css_selector=url encoded css selector` as shown in the following example:

```
newViewJsPayload = viewJsPayload.replace("%native_dom_id%", ";css_selector=.right%20%3E%20.ad1");
```

The viewability script then retrieves the HTML element using `document.querySelector`.

## Related topics

- [Introduction to Viewability](introduction-to-viewability.md)
- [Native Creatives](native-creatives.md)