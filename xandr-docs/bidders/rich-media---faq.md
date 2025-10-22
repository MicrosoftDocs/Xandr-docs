---
title: Rich Media - FAQ
description: In this article, find answers to frequently asked questions regarding Rich Media.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Rich media - FAQ

> [!NOTE]
> For more information about rich media, see [Expandables and Rich Media](expandables-and-rich-media.md).

## Expandables

### How do I know if an impression supports an expandable creative?

There will be two fields in the bid request to indicate the availability of expandables on an impression.

| Field | Description | Notes |
|---|---|---|
| `allowed_types` | Array of media type ids | This field is optional. If it appears, creatives of the specified media types may serve on this impression. |
| `allowed_subtypes` | Array of media subtype ids | This field is optional. If it appears, creatives of the specified media subtypes may serve on this impression. |
