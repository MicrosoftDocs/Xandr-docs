---
title: Microsoft Monetize (March 20, 2026) Historical Reporting adds new supply chain and GPID fields
description: Learn about the new Historical Reporting supply chain and GPID fields
ms.topic: release-notes
ms.date: 03/18/2026
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: rupambaruah
---

# Historical Reporting adds new supply chain and GPID fields

**Release date:** March 20, 2026
**Product:** Microsoft Monetize
**Area:** Historical Reporting
**Status:** General Availability (GA)

## Overview

Microsoft Monetize has added new reporting fields to **Historical Reporting** to provide additional visibility into supply chain transparency and Global Placement ID (GPID) usage. These fields are available in both the **Monetize reporting UI** and the **Digital Platform API**.

The new fields allow publishers and platform users to analyze supply chain object (SCHAIN) attributes and determine whether a **Global Placement ID (GPID)** was present on impressions.

---

## What's new

The following columns are now available in **Historical Reporting**.

### Supply Chain Node Count

**Type:** Int
**Filterable:** Yes

Indicates the number of nodes in the **ad request supply chain (SCHAIN)**.

---

### Is Supply Chain Complete

**Type:** String
**Filterable:** Yes

Indicates whether the **SCHAIN object** in the ad request is marked as complete.

---

### Is GPID Present

**Type:** String
**Filterable:** Yes

Indicates whether a **Global Placement ID (GPID)** was present on the impression.

> **Note**
> This field is a reporting-only characteristic and does not affect the GPID value used at auction time.
>
> The field is supported for **Impressions metrics only**. Because some ad requests do not result in a transacted impression, those requests are not GPID-reportable. As a result, using this field together with **Ad Request** or **Response** metrics may not accurately reflect GPID coverage and is not recommended.

---

## Availability

These fields are available in:

* **Microsoft Monetize Historical Reporting UI**
* **Digital Platform API – Historical Reporting**

---

## Impact

No action is required. These fields are available for use in reporting queries and UI reports immediately.
