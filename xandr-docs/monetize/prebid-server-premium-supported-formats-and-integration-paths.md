---
title: Prebid Server Premium Supported Formats and Integration Paths
description: In this article, learn about the advertising formats and integration methods supported by Prebid Server Premium across devices.
ms.date: 03/11/2024
---

# Prebid Server Premium supported formats and integration paths

Prebid Server Premium (PSP) supports a variety of advertising formats and integration methods as detailed below. For more information, see Integrate with PSP and Set up Prebid Server Premium.

> [!IMPORTANT]
>
> - Microsoft Monetize Ad Server customers do not need to change their integration method to call PSP, except for AMP.
> - Microsoft Monetize customers generally need to update Prebid.js or Prebid Mobile SDK to call PSP, although other methods are supported.
> - Native support is only available for native assets. Rendered native assets may come through as banner media type.

## Web and mobile web

| Integration Method | Banner | Native Display | Native Video | Video Outstream | Video Instream | Long-Form Video |
|--|--|--|--|--|--|--|
| **Microsoft Monetize Ad Server** |  |  |  |  |  |  |
| AST (ut/v3) | Y | Y | Y | Y |  |  |
| OpenRTB (/openrtb2) | Y | Y | Y | Y | Y | Y |
| TinyTag (ttj) | Y |  |  |  |  |  |
| Video Tag (/ptv or /ssptv) |  |  |  |  | Y | Y |
| VMAP (/vmap or /ssvmap) |  |  |  |  |  | Y |
|  |  |  |  |  |  |  |
| **Microsoft Monetize** |  |  |  |  |  |  |
| Client-Side Prebid   (ut/v3/prebid) | Y | Y | Y | Y | Y |  |
| Server-Side Prebid   (openrtb2/prebid) | Y | Y | Y | Y | Y |  |
| OpenRTB (/openrtb2) | Y | Y | Y | Y | Y | Y |
| TinyTag (ttj) | Y |  |  |  |  |  |
| Video Tag (/ptv or /ssptv) |  |  |  |  | Y |  |
| Long-Form Video (/prebid/lfv   or /prebid/lfvp) |  |  |  |  |  | Y |

## App

| Integration   Method | Banner | Native Display | Native Video | Video Outstream | Video Instream | Long-Form Video |
|--|--|--|--|--|--|--|
| **Microsoft Monetize Ad Server** |  |  |  |  |  |  |
| OpenRTB (/openrtb2) | Y | Y | Y | Y | Y | Y |
| Video Tag (/ptv or /ssptv) |  |  |  | Y | Y | Y |
| VMAP (/vmap or /ssvmap) |  |  |  |  |  | Y |
| Xandr Mobile SDK (ut/v3) | Y | Y | Y | Y | Y |  |
|  |  |  |  |  |  |  |
| **Microsoft Monetize** |  |  |  |  |  |  |
| OpenRTB (/openrtb2) | Y | Y | Y | Y | Y |  |
| Video Tag (/ptv or /ssptv) |  |  |  | Y | Y |  |
| Long-Form Video (/prebid/lfv   or /prebid/lfvp) |  |  |  |  |  | Y |
| Prebid Mobile SDK   (openrtb2/prebid) | Y | Y | Y | Y | Y |  |

## AMP

| Integration   Method | Banner |
|--|--|
| **Microsoft Monetize Ad Server** |  |
| AMP (prebid/amp) | Y |
|  |  |
| **Microsoft Monetize** |  |
| AMP (prebid/amp) | Y |
