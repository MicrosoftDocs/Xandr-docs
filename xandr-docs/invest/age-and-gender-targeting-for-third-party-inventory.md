---
title: Microsoft Invest – Age & Gender Targeting for Third-Party Inventory
description: Improve workflow when using member’s age and gender user data to target both managed and third-party inventory.
ms.date: 10/28/2023
---

# Microsoft Invest - Age and gender targeting for third-party inventory

> [!NOTE]
> If you are advertising in connection with any financial, insurance, education, career and employment, and/or housing services, you may not use individuals’ demographics for the purpose of personalizing advertising, segmenting, or profiling customers.

Microsoft Advertising has an option for improving workflow when targeting a member's own age and gender data on both managed and third-party inventory.

## Process overview

Buyers can easily target inventory where the publisher provides age and gender data in the query strings of their ad calls. This feature is typically used for managed buying of a member's own data. Buyers can set this in the **Demographics** section in the **Audience & Location Targeting** section of the augmented line item.

A buyer can use their age and gender user data to target both managed and third-party inventory from the **Demographics** section of the Targeting setup. To do so:

1. Buyer members create a specific age segment and a gender segment in the Segments section. These segments can be populated through segment pixels, batch segment upload, or query string values.
1. Once created, the member contacts Microsoft Advertising Support to request a one-time member setting change to make those segment IDs the default age and gender segments for the member.
1. After the age and gender segments are defined, the member can use demographics targeting to target age and gender using the member's own segment data on managed or third-party inventory.

## Workflow

Once enabled, demographic targeting in Microsoft Invest will apply to inventory from managed publishers as well as third-party publishers. In the case of impressions where the publisher passes age and gender data in the ad call:

- For inventory from managed inventory: age/gender segment values will be used for demographic targeting, unless age/gender is explicitly passed on the query string, in which case query string values will be used.
- For inventory from third party inventory: age/gender segment values will always be used for demographic targeting, even if age/gender is explicitly passed on the query string.
