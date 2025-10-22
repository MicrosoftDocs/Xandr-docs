---
title: User Agent Client Hints
description: In this article, find information about what User-Agent Client Hints API is and how it works.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: seller-tag
ms.author: shsrinivasan
---

# User Agent Client Hints

## Overview

The User-Agent Client Hints API is an expansion to the Client Hints API, that enables developers to access information about a user's browser in a more specific and targeted manner, while still preserving the user's privacy and providing users with greater control over the data that is shared about their browsing activity. This API extends the traditional User-Agent header in HTTP requests and allows developers to request only the specific pieces of information they need, rather than exposing the entire header. This helps to eventually reduce the User-Agent string granularity and the amount of potentially sensitive information that can be transmitted.

Client Hints are intended to be an alternative source of information contained in the User-Agent header. User-Agent (UA) reduction is an effort to minimize the identifying information shared in the User-Agent string. As a result, the return values from certain `Navigator` interfaces will be reduced, including: `navigator.userAgent`, `navigator.appVersion`, and `navigator.platform`. If we do not make the necessary adjustments and fail to adapt to this change, certain capabilities will be forfeited, including the ability to identify and prevent fraud and bot activity, recognizing browsers for rendering purposes, and targeting buyers based on their devices. Furthermore, buyers will no longer be able to take advantage of device targeting.

**Current UA string (detected as Tablet device):**

```
Mozilla/5.0 (Linux; Android 9; SM-T810) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.1234.56 Safari/537.36
```

**Same user with reduced UA string - not using Client Hints (detected as Desktop device):**

```
Mozilla/5.0 (Linux; Android 10; K) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.0.0 Safari/537.36
```

## **High Entropy Client Hints**

To offer maximum performance and execute optimal device targeting, Xandr needs to access two high entropy Client Hints:

- Model
- Platform Version

To pass these values, publishers need to set two headers, **Accept-CH** and **Permissions-Policy**.

**Accept-CH** is a http header, set by a server to specify which Client Hints headers the browser should include in subsequent requests. By default, the Client Hint headers will only be sent over same-origin requests. It indicates Xandr’s ad call does not have access being a cross-origin request . To allow hints on cross-origin requests, each hint must be specified by a **Permissions-Policy** header.

The publisher server is required to set these two headers as shown below:

- Accept-CH: `sec-ch-ua-model,sec-ch-ua-platform-version`
- Permissions-Policy: `ch-ua-model=*,ch-ua-platform-version=*`

## Scenarios

If you are using `ast.js` or Xandr’s bid adapter in `prebid.js`, there are two scenarios depending upon whether the client-side script (ast/prebid) is loaded outside or inside an iframe.

### Script is loaded outside an iframe

In this scenario, the publisher server needs to set the http headers whereas no change is required on the client side. For example, if the publisher domain is `https://example.com`, then the server for `example.com` needs to set the http headers.

### Script is loaded inside a cross-domain iframe

In this scenario, the cross-domain server needs to set the http headers. For example, if publisher domain is `https://example.com` and the iframe loads content from another domain, `https://adscripthost.com/ad_placement_setup.html`, then the server for `https://adscripthost.com` needs to set the headers.

Here, the `allow` attribute should also be present on the iframe with value set to `ch-ua-platform-version;ch-ua-model`. For example,

```
<iframe allow="ch-ua-platform-version;ch-ua-model" src="https://adscripthost.com/ad_placement_setup.html" style="width: 100%; height: 400px"></iframe>  
```
