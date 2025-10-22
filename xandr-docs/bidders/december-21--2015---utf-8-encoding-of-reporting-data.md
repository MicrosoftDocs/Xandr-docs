---
title: December 21, 2015 - UTF-8 Encoding of Reporting Data
description: Explore enhanced UTF-8 encoding for reporting since Dec 21, 2015; from Jan 15, 2016, include all UTF-8 characters in returned data, incorporating Log-Level Data.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# December 21, 2015 - UTF-8 encoding of reporting data

Starting on January 15th, 2016, we will now be including all UTF-8 characters for all data returned via reporting (including Log-Level Data, if applicable). Historically, we were either stripping or replacing some select special characters from string fields, and now we will be returning all UTF-8 characters.

What this change means for you is that:

- You will begin to receive UTF-8 characters in reporting, including any Log-Level feeds you may subscribe to. This data will be actual UTF-8, it will not be encoded using the `"\u00DF"` syntax used by, e.g., the JSON specification.

- You will be able to target domains made up of UTF-8 characters.

- If you `PUT` or `POST` UTF-8 data to an API service, you will hit per-field character limits sooner than before, since UTF-8 characters  are "wider" and take up more space than our current encoding.

The first point in the above list (reporting) is the one most likely to affect your integration. If you do not already work with languages that require UTF-8 characters on a regular basis, these changes are unlikely to affect you.

We recommend that you ensure your integration is capable of receiving UTF-8 characters in reporting.
