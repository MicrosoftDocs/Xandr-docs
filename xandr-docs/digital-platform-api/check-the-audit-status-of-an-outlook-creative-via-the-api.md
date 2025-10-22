---
title: Check the Audit Status of an Outlook Creative via the API
description: In this article, learn about the three possible audit statuses of an Outlook creative via the API.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Check the audit status of an Outlook creative via the API

Once you've added an Outlook creative, you can make a `GET` call to the [Creative Service](creative-service.md) to check where the creative is in Xandr's secure platform and Microsoft audits. For each audit, there are three possible statuses your creative can have:

| Field | Statuses |
|:---|:---|
| `ssl_audit` | The eligibility of the creative to serve on secure inventory. <br>Possible values:<br> - `"pending"`: The creative is being SSL audited by Xandr.<br> - `"approved"`: The creative has passed the SSL audit and is eligible to serve on secure inventory.<br> - `"failed"`: The creative has been rejected for SSL audit and is not eligible to serve on secure inventory. |
| `msft_audit_status` | The eligibility of the creative to search on Microsoft inventory. <br>Possible values:<br> - `"pending"`: The creative is being audited for Microsoft Creative Acceptance Policy by Xandr.<br> - `"approved"`: The creative has passed Microsoft CAP audit and is eligible to serve on Microsoft Advertising Exchange.<br> - `"rejected"`: The creative has been rejected for Microsoft CAP audit and is not eligible to serve on Microsoft Advertising Exchange .  |

> [!TIP]
> If an Outlook creative fails the Xandr SSL or Microsoft audit, you can re-submit it for audit (once you've fixed the downstream non-secure content) by changing `ssl_status` to `"pending"`.

## Related topics

- [Buying Microsoft Outlook.com Inventory](buying-microsoft-outlook-com-inventory.md)
- [Create an Outlook Campaign via the API](create-an-outlook-campaign-via-the-api.md)
