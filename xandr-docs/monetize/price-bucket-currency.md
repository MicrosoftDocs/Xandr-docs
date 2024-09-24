---
title: Price Bucket Currency
description: In this article, find information about using currencies other than USD with Prebid Server Premium (PSP).
ms.date: 10/28/2023
---

# Price bucket currency

This page includes guidance on using currencies other than USD with Prebid Server Premium (PSP).

Price bucket currency specifies the currency used for price buckets and **does not apply to Microsoft Monetize Ad Server customers**. Specifically, targeting keys, not bids, are converted into the selected currency. Select the currency that aligns with the line items in the publisher's ad server. Any currency [supported by Microsoft Advertising](currency-support.md)can be chosen.

> [!IMPORTANT]
> This is independent of the Monetize currency selection and only applies to Prebid Server Premium (PSP) auctions.

## Bid response currency

### Targeting keys

- When using the `/openrtb2/prebid` (and have specifically set it to override targeting keys in response) or `/ut/v3/prebid` endpoints, targeting keys within bid responses use the transaction currency that you have set via the [Publisher Service API](../digital-platform-api/publisher-service.md). If you need to override that currency selection, use the [Prebid.js Currency Module](https://docs.prebid.org/dev-docs/modules/currency.html#currency-module).
- When using another integration method, targeting keys within bids use the currency selected for PSP price buckets independently of the [Publisher Service API](../digital-platform-api/publisher-service.md).

## Related topic

[Add or Edit PSP Global Settings](add-or-edit-psp-global-settings.md)
