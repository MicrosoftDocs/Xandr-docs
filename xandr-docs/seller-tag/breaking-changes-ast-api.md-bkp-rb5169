---
title: Breaking Changes - AST API
description: In this article, understand what breaking changes are and what types of changes do and do not qualify as breaking changes.
ms.custom: seller-tag
ms.date: 10/28/2023
---

# Breaking changes - AST API

Our AST API is continually changing. The vast majority of changes simply add new functionality, but occasionally we introduce breaking changes that may require you to adjust your integration.

This page explains what changes qualify as breaking changes to our AST API. It also gives examples of changes that do not qualify as breaking changes.

> [!NOTE]
> Xandr reserves the right to fix bugs, adjust functionality to comply with [part of our Service Policies](../policies-regulations/index.yml) and legal obligations, and change features and products in alpha and beta without providing early notice.

## Breaking changes

The following types of changes qualify as breaking changes:

- Removal of or changing the name of a field in an event handler response (adObj api)
- Removal of the object from an event handler callback function definition
- Removal of or changing the name of an AST method (for example, `defineTag()` or `showTag()`)
- Modification of the data type of a field (for example, an array of IDs converted to an array of objects)

> [!NOTE]
> When we introduce a breaking change into our AST API, we will support the version of AST without the breaking change as the production (`/ast.js`) version for 45 days. During this 45 day period, the new version (which includes breaking changes) will be available at a static URL (`/v1.0.1/ast.js`). After the 45 days, the breaking change version will be promoted to the production URL. All recent versions of AST will be available via the static URL, so you may continue to use the version without the breaking change by calling its specific version instead.

Additionally, we will notify AST users of these changes and how to correctly reach each version during the breaking changes period.

Breaking changes to the AST protocol will be announced on our [AST Release History](ast-release-history.md) page. We encourage you to subscribe to updates to be proactively notified of breaking changes. (For Xandr clients, breaking changes will also be announced in release notes.)

## Examples of non-breaking changes

The following types of changes do not qualify as breaking changes. Please note that this list is not exhaustive; these are just some examples of non-breaking changes.

- Addition of a new non-mandatory field
- Addition of a new AST method
- Deprecation of a field without removing it
- Change in order of fields in an object, objects in an array, and so on.
