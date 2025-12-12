---
title: PSP Supported Formats and Integration Paths
description: In this article, learn about the advertising formats and integration methods supported by Prebid Server Premium across devices.
ms.date: 12/12/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: rupambaruah
---

# PSP supported formats and integration paths

Prebid Server Premium (PSP) supports a variety of advertising formats and integration methods as detailed below. For more information, see [Integrate with PSP](integrate-with-psp.md) and [Set up Prebid Server Premium](set-up-prebid-server-premium.md).

> [!IMPORTANT]
>
> - Microsoft Monetize Ad Server customers do not need to change their integration method to call PSP, except for [AMP](integrate-accelerated-mobile-pages-with-psp.md)
> - Microsoft Monetize customers generally need to update Prebid.js or Prebid Mobile SDK to call PSP, although other methods are supported
> - Native support is only available for native assets. Rendered native assets may come through as banner media type

## Web and mobile web

| Integration Method | Banner | Native Display | Native Video | Video Outstream | Video Instream | Long-Form Video |
|--|--|--|--|--|--|--|
| **Microsoft Monetize Ad Server** |  |  |  |  |  |  |
| [AST (ut/v3)](working-with-seller-tag.md) | Y | Y | Y | Y |  |  |
| [OpenRTB (/openrtb2)](non-prebid-integrations-with-psp.md) | Y | Y | Y | Y | Y |  |
| [TinyTag (ttj)](../bidders/tinytags.md) | Y |  |  |  |  |  |
| [Video Tag (/ptv or /ssptv)](non-prebid-integrations-with-psp.md) |  |  |  | Y | Y | Y |
| [VMAP (/vmap or /ssvmap)](non-prebid-integrations-with-psp.md) |  |  |  |  |  | Y |
| **Microsoft Monetize** |  |  |  |  |  |  |
| [Client-Side Prebid (openrtb2/prebidjs)](integrate-web-mobile-web-with-psp.md) | Y | Y | Y | Y | Y |  |
| [Server-Side Prebid (openrtb2/prebid)](integrate-web-mobile-web-with-psp.md) | Y | Y | Y | Y | Y |  |
| [OpenRTB (/openrtb2)](non-prebid-integrations-with-psp.md) | Y | Y | Y | Y | Y |  |
| [TinyTag (ttj)](../bidders/tinytags.md) | Y |  |  |  |  |  |
| [Video Tag (/ptv or /ssptv)](non-prebid-integrations-with-psp.md) |  |  |  |  | Y |  |
| [Long-Form Video (/prebid/lfv or /prebid/lfvp)](../digital-platform-api/long-form-video-service.md) |  |  |  |  |  | Y |

## App

| Integration   Method | Banner | Native Display | Native Video | Video Outstream | Video Instream | Long-Form Video |
|--|--|--|--|--|--|--|
| **Microsoft Monetize Ad Server** |  |  |  |  |  |  |
| [Xandr Mobile SDK (ut/v3)](../mobile-sdk/xandr-mobile-sdks.md) | Y | Y | Y | Y | Y |  |
| [OpenRTB (/openrtb2)](non-prebid-integrations-with-psp.md) | Y | Y | Y | Y | Y |  |
| [Video Tag (/ptv or /ssptv)](non-prebid-integrations-with-psp.md) |  |  |  | Y | Y | Y |
| [VMAP (/vmap or /ssvmap)](non-prebid-integrations-with-psp.md) |  |  |  |  |  | Y |
| **Microsoft Monetize** |  |  |  |  |  |  |
| [Prebid Mobile SDK (openrtb2/prebid)](integrate-apps-with-psp.md) | Y | Y | Y | Y | Y |  |
| [OpenRTB (/openrtb2)](non-prebid-integrations-with-psp.md) | Y | Y | Y | Y | Y |  |
| [Video Tag (/ptv or /ssptv)](non-prebid-integrations-with-psp.md) |  |  |  | Y | Y |  |
| [Long-Form Video (/prebid/lfv or /prebid/lfvp)](../digital-platform-api/long-form-video-service.md) |  |  |  |  |  | Y |

## AMP

| Integration   Method | Banner |
|--|--|
| **Microsoft Monetize Ad Server** |  |
| [AMP (prebid/amp)](integrate-accelerated-mobile-pages-with-psp.md) | Y |
| **Microsoft Monetize** |  |
| [AMP (prebid/amp)](integrate-accelerated-mobile-pages-with-psp.md) | Y |
