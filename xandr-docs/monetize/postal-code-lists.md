---
title: Microsoft Monetize - Postal Code Lists
description: In this article, find information about postal code lists and how to manage, create, and target them.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Postal code lists

## Introduction

> [!NOTE]
> If you are advertising in connection with any financial, insurance, education, career and employment, and/or housing services, you may not use postal codes for the purpose of personalizing advertising, segmenting, or profiling customers.

Leveraging postal codes is a powerful way for advertisers to achieve highly granular and precise, or *hyperlocal*, targeting. Hyperlocal targeting is a key factor in driving advertising performance. Because sellers and curators often want to increase efficiency by targeting the same set of postal codes across multiple deals, the Postal Code List feature allows users to easily reuse a predefined list of postal codes.

The Postal Code List feature enables users to:

- create postal code lists (include or exclude) so that a list can be used across their deals.
- enable postal code lists (include or exclude) for targeting at the deal line item level. The maximum number of postal code lists a deal line item can target is 100.

> [!NOTE]
> Certain legitimate ZIP or postal codes are unrecognizable or invalid within the Microsoft Advertising geography targeting system. This can happen because [Digital Envoy](https://www.digitalelement.com/), a Microsoft Advertising partner that handles geolocation data, can't recognize a ZIP or postal code's existence until an IP address (user) has been associated with it. Postal codes that don't exist in the system often represent obscure or otherwise small geographical zones with minimal internet activity.

## Manage postal code lists

You can create a Postal Code List at the Network level. A Postal Code List may contain one or more postal codes. Postal codes can be added to multiple Postal Code Lists. However, a postal code can be added only once to a single Postal Code List.

Postal codes can be added to a list by either:

- copying and pasting in a dialog box.
- bulk uploading a CSV, Excel, or Text file.

> [!IMPORTANT]
>
> - The maximum number of postal codes allowed in a list is 100,000.
> - The maximum number of postal codes lists allowed per member is 8,000.
> - Postal code lists that have not been modified in six months and are not associated with line items that have served in the last six months are eligible to be deleted by Microsoft Advertising.

### Create a new postal code list

1. Select **Network** > **Location Manager**.
1. On the **Location Manager** page, select **New** > **Postal Code List**.
1. Provide the following details in the **Create a Postal Code List** page:
    1. **Name**: Enter the name of the Postal Code List. For example, enter "NetherlandsLoc1". The maximum number of characters allowed is 255.
    1. **Code**: (optional) Enter a code for the Postal Code List.
    1. **Description**: (optional) Enter a description for the Postal Code List that gives a brief definition of the postal code location target. For example, enter "Postal Code List for Noor-Holland region in the city of Amsterdam, Netherlands".
1. Choose **Any Advertiser** or target a specific subset of advertisers by selecting **Specific Advertisers**
1. Select one of the following options:
    - **Copy and paste**: If you select this option, on the next page you can enter the postal codes to include in the Postal Code List. The codes need to be separated by a comma or hard return. When you're done, click **Next**.
    - **Import from file**: If you select this option, on the next page you can browse for and upload a CSV, Excel, or Text file that contains the postal codes.
1. Click **Save** to complete the setup.

## Related topic

[Additional Geo Restrictions](additional-geo-restrictions-ali.md)    

<!--
    > [!NOTE]
    > - You need to select the country or region to which the postal codes belong before using the **Copy and Paste** or **Import from file** option. You can only upload postal codes from one country or region at a time.
    > - For USA, you can target the full 9-digit postal code (also known as zip +4). For example, you can target "10010-7456".

1. On the **Review Location Target** page, the following tabs are available:
    - **Successfully Imported** displays the list of postal codes that were successfully imported to the Postal Code List with the **Code**, **Country Name**, **Country ID** of each postal code.
    - **Did Not Import** displays postal codes that failed to import properly. --> 

<!--
## Target postal code lists and postal codes on line items

To learn more about targeting Postal Code Lists and Postal Codes on line items, see [Additional Geo Restrictions](additional-geo-restrictions-ali.md).
-->


