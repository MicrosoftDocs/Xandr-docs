---
title: Microsoft Monetize - Domain Audit Status
description: Explore the Domain Audit Status tool to check the audit status of your domains and access various associated information.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Domain Audit Status

Microsoft Advertising provides domain audits as part of the platform. The **Domain Audit Status** tool provides the functionality to check the current audit status of your domains.

## Use the Domain Audit Status tool

The **Domain Audit Status** tool is available under **Network** > **Tools** > **Domain Audit Status**.

To check the audit status of your domains, follow these steps:

1. Go to the **Network** > and select **Domain Audit Status** from the vertical navigation on the left. This redirects you to the **Domain Audit Status** screen.
1. Under **Search Domains**, enter the domains you would like to check. Separate multiple values with commas or line breaks. Alternatively, select the **Upload** button to upload a CSV file containing up to 4,000 domains.
1. Select **Submit** to run the tool.

## Understand the results

After the domains are submitted for verification, the page shows the following information:

| Field | Description |
|:--|:--|
| **Domain** | The submitted domain. |
| **Audit Status** | The current audit status of the domain. Possible statuses:<ul><li>Audited</li><li>Pending</li><li>Unable to Audit</li><li>Rejected</li><li>Ad Serving</li><li>Unaudited</li><li>Masked</li></ul> |
| **Reason** | If the audit status is **Unable to Audit** or **Rejected**, this field provides a reason for the assigned audit status. This status can be used for more context on the decision and to troubleshoot any issues. |
| **Audience** | The intended audience of the domain, as determined by Microsoft Monetize. Possible values:<ul><li>mature</li><li>young adult</li><li>children</li><li>general</li></ul>If the audit status is **Rejected**, this field will be `null`. |

### Audit Status definitions

| Status | Description |
|:--|:--|
| **Audited** | The domain has been reviewed and passed an audit. |
| **Pending** | The domain has been submitted for audit but hasn't yet been reviewed. |
| **Unable to Audit** | The domain has been reviewed but cannot be audited. |
| **Rejected** | The domain has been rejected after an audit. |
| **Ad Serving** | The domain is an ad-serving domain. |
| **Unaudited** | The domain isn't yet in the Xandr audit queue. You should submit a ticket to have it reviewed. |
| **Masked** | The seller isn't exposing the domain or app's actual URL for targeting or reporting. However, the real domain or app URL is still audited by Xandr inventory quality controls within the bid request. |

## FAQ

### What should I do if my domains aren't audited?

If you require assistance with re-auditing your domains, contact your Microsoft Advertising representative.
