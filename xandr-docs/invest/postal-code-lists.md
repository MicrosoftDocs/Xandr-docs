---
title: Microsoft Invest - Postal Code Lists
description: In this article, understand how postal code lists help in hyperlocal targeting, how to manage postal code lists, and how to target postal code lists.
ms.date: 10/28/2023
---

# Microsoft Invest - Postal code lists

> [!NOTE]
> If you are advertising in connection with any financial, insurance, education, career and employment, and/or housing services, you may not use postal codes for the purpose of personalizing advertising, segmenting, or profiling customers.

Leveraging postal codes is a powerful way for advertisers to achieve highly granular and precise, or *hyperlocal*, targeting. Hyperlocal targeting is a key factor in driving advertising performance. Because buyers often want to increase efficiency by targeting the same set of postal codes across different objects (line items and splits), the Postal Code List feature allows them to reuse a list of postal codes across different line items and splits.

The Postal Code List feature enables traders to:

- create postal code lists (include or exclude) so that a list can be used across different objects (line items, splits).
- enable postal code lists (include or exclude) for targeting at the line item level. The maximum number of postal code lists a line item or split can target is 100.

> [!NOTE]
> Certain legitimate ZIP or postal codes are unrecognizable or invalid within the Microsoft Advertising geography targeting system. This can happen because [Digital Envoy](https://www.digitalelement.com/), a Microsoft Advertising partner that handles geolocation data, can't recognize a ZIP or postal code's existence until an IP address (user) has been associated with it. Postal codes that don't exist in the system often represent obscure or otherwise small geographical zones with minimal internet activity.

## Manage postal code lists

You can create a Postal Code List at the Member level. A Postal Code List may contain one or more postal codes. Postal codes can be added to multiple Postal Code Lists. However, a postal code can be added only once to a single Postal Code List.

Postal codes can be added to a list by either:

- Copying and pasting in a dialog box.
- Bulk uploading a CSV, Excel, or Text file.

> [!IMPORTANT]
>
> - The maximum number of postal codes allowed in a list is 100,000.
> - The maximum number of postal codes lists allowed per member is 8,000.
> - Postal code lists that have not been modified in six months and are not associated with line items that have served in the last six months are eligible to be deleted by Microsoft Advertising.

### Create a new postal code list

1. Select **Audiences** > **Location Manager**.
1. On the **Location Manager** page, select **New** > **Postal Code List**.
1. Provide the following details in the **Create A Location Target** page:
    1. **Name**: Enter the name of the Postal Code List. For example, enter "NetherlandsLoc1". The maximum number of characters allowed is 255.
    1. **Code**: (optional) Enter a code for the Postal Code List.
    1. **Description**: (optional) Enter a description for the Postal Code List that gives a brief definition of the postal code location target. For example, enter "Postal Code List for Noor-Holland region in the city of Amsterdam, Netherlands".
1. Select **Next**.
1. On the **Location Target Features** page, select one of the following options:
    - **Copy and Paste**: If you select this option, on the next page you can enter the postal codes to include in the Postal Code List. The codes need to be separated by a comma or hard return. When you're done, select **Next**.
    - **Import from file**: If you select this option, on the next page you can browse for and upload a CSV, Excel, or Text file that contains the postal codes. Once uploaded, select **Next**.

    > [!NOTE]
    >
    > - You need to select the country to which the postal codes belong before using the **Copy and Paste** or **Import from file** option. You can only upload postal codes from one country at a time.
    > - For USA, you can target the full 9-digit postal code (also known as zip +4). For example, you can target "10010-7456".

1. On the **Review Location Target** page, the following tabs are available:
    - **Successfully Imported** displays the list of postal codes that were successfully imported to the Postal Code List with the **Code**, **Country Name**, **Country ID** of each postal code.
    - **Did Not Import** displays postal codes that failed to import properly.
1. Select **Save** to complete the setup.

## Target postal code lists and postal codes on line items

To learn more about targeting Postal Code Lists and Postal Codes on line items, see [Additional Geo Restrictions](additional-geo-restrictions-ali.md).

## Target postal code lists and postal codes on splits

A trader can include and exclude Postal Code Lists and individual postal codes from targeting on splits.

To target specific Postal Code Lists and Postal Codes:

1. Go to the **Targeting** section in **Edit Split**.
1. Select Postal Code. Additional lists that allow you to select **Postal Code Lists** and **Postal Codes** are displayed. For each,    perform the steps in the following table.

    | Value | Steps |
    |---|---|
    | Postal Code Lists | - Search by ID or Name for available Postal Code Lists to target <br> - Either include or exclude the postal code list for the line item for targeting. Select the **green check** to include a list and select the **red dash** to exclude a list. <br> - After you select a postal code list, it displays the particulars of the list such as Name and ID under the section **Selected Postal Codes**. You can use the **Remove all** button if necessary. <br> - You can add multiple postal code lists to include or exclude for the line item using this search option. |
    | Postal Codes | - Copy and paste the postal codes or import a file of postal codes you want to target following the instructions in step 5 in the **To create a new Postal Code List** section above. You can add upto 100,000 postal codes in this dialog box. <br> - You can include or exclude a postal code from targeting for a split. |

1. Select **Save** to complete the setup.

## Related topic

[Additional Geo Restrictions](additional-geo-restrictions-ali.md)
