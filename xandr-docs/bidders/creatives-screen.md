---
title: Creatives Screen
description: Learn steps to access the Creatives screen in this page. Also this page covers a table with bidder and their associated attributes/metadata listed.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---


# Creatives screen

The **Creatives** screen is where a bidder can see their creatives, and search for the creative they would like to investigate further. For additional details on the creative, bidders can use the [Creative Service](creative-service.md).

## Creatives screen access

1. Sign in to the Bidders UI: [https://bidder.xandr.com](https://bidder.xandr.com/login)
1. Select the bidder.
1. Click **Switch to Default User**. The **Profiles** screen is accessed.
1. Click on the **Creatives** tab to access the **Creatives** screen. (It is located to the right of the **Profiles** tab).

A table is displayed that lists all of the creatives for a bidder, and their associated attributes/metadata:

| Attribute | Description |
|--|--|
| **Ad Type** | This is the type of creative. These are the possible ad types: <br> - **Banner** <br> - **Video** <br> - **Audio** <br> - **Native** |
| **Audit Feedback** | This is specific audit feedback. This remains blank unless the creative is rejected in audit. |
| **Audit Status** | This is the status of the audit being performed on the creative. These are the possible statuses: <br> - **Audited** = Approved by creative audit process. Ready to be used in auction. <br> - **Pending** = Under review by audit process. <br> - **Rejected** = Not approved by creative audit process. Check audit feedback column for further details. <br> - **No Audit** = Creative not submitted for audit because allow_audit flag of creative object was set to "false". |
| **Code** | This is the creative code, which is typically set to the external ID for the bidder. This is the ID of the creative in the bidder’s system. |
| **Description** | This is an optional description for the creative, which is configured by the bidder. |
| **ID** | This is the Creative ID assigned by Xandr systems. To preview the creative, click on the magnifying glass next to the ID value. |
| **Last Modified** | This is when the creative was last modified by the bidder. |
| **Member** | This is the name of the member that the creative registered under. <br> **Note**: Bidders frequently have multiple members. |
| **SSL Status** | This refers to the status of the **Secure Sockets Layer**. It is the standard security technology for establishing an encrypted link between a web server and a browser. This link ensures that all data passed between the web server and browsers remain private and integral. These are the possible statuses: <br> - **Approved** <br> - **Pending** <br> - **Failed/Disabled** |
| **State** | This identifies if the creative is **Active** or **Inactive**. |

> [!NOTE]
> You can navigate through the pages by clicking the arrow **(Page>)** which is located on the lower right-hand section of the screen. 
>
> For performance reasons, we do not attempt to calculate the total number of creatives/pages that individual bidders have.

## Related topics

- [Filters](filters.md)
- [Columns](columns.md)
- [Actions](actions.md)
- [Creative Service](creative-service.md)
