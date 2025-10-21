---
title: Microsoft Monetize - Google Ad Manager Creative Audit Process
description: In this article, find information about the creative audit process on Google Ad Manager.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Google Ad Manager creative audit process

For your creative to serve on Google Ad Manager inventory, it must pass both the Microsoft Advertising and Google Ad Manager creative audit.

If you are eligible to buy Google Ad Manager inventory, your creatives are automatically enrolled in the Google Ad Manager audit process. Once you add a new creative, Microsoft Advertising automatically submits it to Google Ad Manager. The Microsoft Advertising and Google Ad Manager audit processes begin simultaneously. Your creatives do not need to pass the Microsoft Advertising audit in order to be submitted to Google Ad Manager. The Google Ad Manager audit process runs hourly, which is independent of the Microsoft Advertising audit. Microsoft Advertising cannot make any guarantees about how quickly the audit will be performed by Google Ad Manager. We are only able to control how often we check Google Ad Manager for an audit status. There are four possible Google Ad Manager creative audit statuses:

- **No Audit** - The creative has not been submitted to Google Ad Manager for audit. This status is displayed immediately after your creative has been saved, but will eventualy change to "Pending" once we have submitted the creative to Google Ad Manager. This can also happen if you are not eligible to buy Google Ad Manager inventory.
- **Pending** - The creative has been submitted to Google Ad Manager for audit, but the audit has not been completed yet. Therefore, it is not yet eligible to serve on Google Ad Manager inventory.
- **Approved** - The creative has been approved by Google Ad Manager. If the creative has also passed the Microsoft Advertising audit, it will be eligible to serve on Google Ad Manager inventory.
- **Rejected** - The creative has been rejected by Google Ad Manager and is not eligible to serve on Google Ad Manager inventory. This status will be accompanied by an explanation from Google Ad Manager.

You should also note the following:

- Microsoft Advertising does not audit creatives for compliance with Google's policies. Microsoft Advertising only audits creatives to ensure that they adhere to our [Creative Standards](creative-standards.md). For more information about Google Ad Manager's standards, see [Google's Ad Exchange Policies](https://support.google.com/authorizedbuyers/answer/1325008?hl=en).
- Audit email notifications do not include the Google Audit column.

> [!WARNING]
> **Appeals for Google Ad Manager audit failures must go through Google Ad Manager**.
>
> Our audit team is not able to assist clients with appeals if a creative is rejected by Google Ad Manager because we are simply reflecting the audit status that Google's API has returned.
>
> In the event that you want to appeal, you should update the creative content and then resubmit your creative for audit. This will trigger a full re-audit cycle with our auditors and Google Ad Manager. Alternatively, you can reach out to your contacts at Google Ad Manager so that your appeal can be considered and manually resubmitted.

## Related topics

- [Google Ad Manager Disapproval Reasons](adx-disapproval-reasons.md)
- [Resubmit Creatives for Google Ad Manager Auditing](resubmit-creatives-for-adx-auditing.md)
- [Creative Service](../digital-platform-api/creative-service.md)
- [Completed Creative Audits Report](completed-creative-audits-report.md)
