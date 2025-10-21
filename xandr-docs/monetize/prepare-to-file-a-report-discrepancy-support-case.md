---
title: Microsoft Monetize - Prepare to Request a Report Discrepancy Investigation
description: In this article, find instructions on how to prepare for and request a report discrepancy investigation.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Prepare to request a report discrepancy investigation

To request a report discrepancy investigation, you should first rule out the most obvious sources of discrepancy, and then gather the information Microsoft Advertising Support needs to take further action.

If you're considering working with Support to investigate a suspected discrepancy, please use the following steps to prepare. Specific details about case qualification and required documentation are covered in [Requirements for Filing a Support Case for Report Discrepancies](requirements-for-filing-a-support-case-for-report-discrepancies.md). For some common causes that can be addressed without Support intervention, see [What to Check if You Suspect a Discrepancy](what-to-check-if-you-suspect-a-report-discrepancy.md).

1. Double-check that the time timezone in the Microsoft Advertising report matches the timezone in the third-party report.
1. Make sure the reports you're comparing contain data from the same time frame. If the time frame isn't the same, Microsoft Advertising does not consider this a discrepancy.

    > [!TIP]
    > A shorter time frame is more useful than a long one.

1. Make sure you know how each ad server counts the activity you're comparing (impressions or clicks). You can contact your third-party ad server for this information. You'll need this information to file a case.

    Microsoft Advertising counts an impression when the creative is rendered. For video ads, an impression takes place when the first frame of the video is loaded. If the third-party counts their impressions differently (for example, when a third party imp tracker loads on the page) the numbers aren't directly comparable, and Microsoft Advertising does not consider this a discrepancy.

1. Make sure the objects for which you're pulling data (for example a campaign, placement, or advertiser) are specified in both reports.

    > [!NOTE]
    > The objects in the third party report must clearly correspond with objects in the Microsoft Advertising system. Please include Microsoft Advertising object IDs in both reports, so that Support can quickly and easily match objects and compare the data. Object names are not unique, and can’t be reliably used for matching.

1. Apply different reporting dimensions to see if you can isolate the discrepancy to a specific object such as a placement, creative, or domain. Wherever possible, take note of the object IDs so you can demonstrate that the object is the same for both reports and you can demonstrate the mapping between objects.

1. Make sure all tracking pixels and tags are in the correct format.

    For example, if you paste a tracking pixel into your browser and it shows up as an image, but it's configured as an HTML URL in Microsoft Advertising, this will cause a discrepancy.

1. Create a spreadsheet that includes both Microsoft Advertising and third-party reporting numbers.

    In the spreadsheet, you need to match the object IDs from each server to ensure one server is not counting more objects than the other. If it is, this isn't a true discrepancy.

1. Calculate the discrepancy percentage using the following formula:

    `(1 - (Microsoft Advertising Report/3rd Party Report)) x 100`

    If the discrepancy is greater than 10% (15% for mobile), you can file a case for Microsoft Advertising to investigate the discrepancy. If the discrepancy is less, it's considered expected variation, and doesn't qualify for a case investigation.
