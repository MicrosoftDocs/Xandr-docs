---
title: Microsoft Monetize - Breaking Changes
description: In this article, find information on what breaking changes are along with examples for breaking and non-breaking changes for Microsoft Monetize.
ms.date: 03/11/2025
ms.author: shsrinivasan
ms.topic: release-notes
---

# Microsoft Monetize - Breaking changes

Our API is continually changing. The vast majority of changes simply add new functionality, but occasionally we introduce *breaking changes* that may require you to adjust your integration.

This page explains what changes qualify as breaking changes to our API. It also gives examples of changes that do not qualify as breaking changes.

> [!IMPORTANT]
> We reserve the right to fix bugs, adjust functionality to comply with our [Part of Service Policies](../policies-regulations/index.yml) and legal obligations, and change features and products in alpha and beta without providing early notice.

## Breaking changes

The following types of changes qualify as breaking changes:

- Removal of a field
- Change of a field from non-mandatory to mandatory
- Addition of new validation rules
- Modification of the data type of a field (for example, array of IDs converted to array of objects)
- Modification of throttling of requests
- Reduction in the number of objects returned by responses

When we introduce a breaking change into our API, we will support two versions of the API in production, one with and one without the breaking change, for 60 days. Also, we will notify API users of these changes and how to correctly reach each version during the breaking changes period. If your user account is enabled for the API, you will receive breaking change communications automatically.

## Examples of non-breaking changes

The following types of changes do not qualify as breaking changes. Please note that this list is not exhaustive; these are just some examples of non-breaking changes.

- Addition of a new non-mandatory field
- Addition of a new service
- Addition of metrics/dimensions to reports
- Addition of a new report type
- Deprecation of a field without removing it
- Reduction or increase in the number of concurrent reports allowed
- Appending a new field to one of our log-level data feeds
- Change in order of fields in an object, objects in an array, and so on
