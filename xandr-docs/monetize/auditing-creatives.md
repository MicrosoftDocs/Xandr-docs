---
title:  Microsoft Monetize - Auditing Creatives
description: Learn how Microsoft Advertising does auditing of creatives before its run on real-time inventory. This page covers when the creatives are audited and how their auditing can get prioritized.
ms.date: 10/28/2023
---


#  Microsoft Monetize - Auditing creatives

Buyers must submit creatives to Microsoft Advertising so that they can be audited before running on Microsoft Advertising real-time inventory. Creatives that fail the Microsoft Advertising platform audit will not run.

All aggregators, including Microsoft, require creatives to be audited by the Microsoft Advertising team prior to running on their inventory. Microsoft Advertising conducts a combination of human and automated auditing for every creative that is added to the platform.

Creatives may be automatically opted in or out of the auditing process. Creatives that are added using the UI are notated with "no audit" by default. Creatives that are added using the API will be marked for audit by default. In the UI, the audit status can be changed using the **Creative Quality** section on the **Create** **New** and **Edit** screens, as well as the **Creative Manager**. For more information, see [Select an Audit Option for a Creative](select-an-audit-option-for-a-creative.md) and [Update Creatives in bulk](update-creatives-in-bulk.md).

If a creative has been altered on the Microsoft Advertising platform after successfully passing the platform audit, its audit status will be automatically reset so that it can be re-audited. The creative must be manually resubmitted for audit if it is altered outside of Microsoft Advertising. For example, in cases where it is redirected to another creative or its graphical assets are altered.

Since Microsoft Advertising charges a fee for each audited creative and buyers may incur additional fees for a failed audit, it's important to test the creative's functionality and review the compliance policies prior to submission. Creatives can be tested by putting a valid Microsoft Advertising ID at the end of the following URLs:

- `https://creative-preview-an.com/cached/creative/insert creative id here` **for Secure Previews**
- `http://creative-preview-an.com/cached/creative/insert creative id here` **for Non Secure Previews**

Questions or appeals regarding creatives audited in excess of 30 days cannot be considered. These creatives should simply be resubmitted to our queue for audit.

> [!NOTE]
> In order to receive the fastest and most efficient service, provide us with your Microsoft Advertising creative IDs, which are typically nine digits.

We recommend that buyers choose the platform audit option when adding creatives on the Microsoft Advertising platform. However, they can choose to self-audit their creative, but should be careful when opting out of platform audits since many sellers only accept Microsoft Advertising audited creatives. Self-auditing may reduce access to inventory outside of one's network. Self-audited creatives that are submitted for platform audit may see some classification changes. For more information, see [Self-Auditing Creatives](self-auditing-creatives.md). Buyers don't have to submit creatives for audit when:

- the creatives will only run directly with the publisher.
- the creatives will run on resold inventory, so the buyer doesn't have to submit those creatives for audit since publishers may allow unaudited creatives to run.
- the creatives are not ready to serve. For example, the buyer wants to edit the content later, or the third-party offer has not been activated.

## Auditing timeline and priority

Creatives are audited in the order that they are received with a target completion time of one business day from the submission time. Priority audits, which are available for an additional fee, are completed within two business hours.

> [!NOTE]
> Buyers should speak with their Microsoft Advertising business representative to enable priority audits for their account.

We always try to deliver on our SLA by keeping to the one business day timeframe. However, circumstances sometimes prevent us from meeting this exact time.

> [!NOTE]
> Requests for priority auditing should not be submitted using the Support Form. Buyers should contact their Microsoft Advertising business representative for the contract supplement. The Microsoft Advertising Support team cannot process requests for priority auditing.

Select one of the following audit options from the **Creative Quality** section:

- **Platform Audit**: Select this option to submit the creative for auditing by the Microsoft Advertising Audit team and perform the following:

  - Select a priority.

   > [!NOTE]
   > Business days are from 9:00pm Sunday to 11:59pm Friday ET.

    Microsoft Advertising charges a fee for each audited creative. The **priority table** below lists the fee charged for audits conducted for different time durations.

   | Priority | Fee | Description |
   |--|--|--|
   | Regular one day audit | $1 USD | Fee charged for 1 Day Audit |
   | Priority audit | $25 USD | Fee charged for 2 Hour Audit |

  - Enter a desktop compatible URL in the **Brand URL** text field.

    > [!NOTE]
    > The **Brand URL** should contain the same branding that is represented on your CTV, OTT, or mobile creative. The Audit team will use the URL to validate the branding represented on the creative.

  - Select the **language** that is used in the creative such as French, German, or Chinese.

    > [!NOTE]
    > Modifying the selected **language** will cause the creative to be resubmitted for audit.

- **Self Audit**: Select this option to classify the creative on your own. For further guidance on self-auditing, see [Self-Auditing Creatives](../invest/self-auditing-creatives.md).

  > [!NOTE]
  > Self-auditing may reduce access to inventory outside of your network since many sellers only allow Microsoft Advertising audited creatives.

  Set any one of the following creative attributes:

  - **Brand**: This lets other sellers on the platform know what brands this creative is associated with in the system.
  - **Offer Categories**: This lets sellers know the offer category such as Education or Employment.
  - **Language**: The language used in the creative such as French, German, or Chinese.
  - **Technical Attributes**: It describes features associated with the creative, such as whether it is a video.
  - **Sensitive Attributes**: These are often banned by publishers.

  > [!NOTE]
  > The Compliance must be confirmed for self audited creatives.

- **No Audit**: Select this option if you do not want the creative to be audited.
  
  > [!NOTE]
  > When selecting **No Audit**, this may result in the creative serving less frequently, as publishers might choose to block it.

For a full description of the Microsoft Advertising auditing process and the content standards for creatives running on the Microsoft Advertising platform, see [Auditing Creatives](../invest/auditing-creatives.md) and [Creative Standards](../invest/creative-standards.md). Regardless of your audit selection, the Microsoft Advertising Sherlock technology checks all creatives for overt malvertising threats and suspicious behavior.

**Bulk submissions**

Bulk submissions are audited as efficiently as possible without interfering with the auditing of regular submissions. Microsoft Advertising can audit:

- a submission of 3K+ creatives in an hour
- a submission of 5K+ in the span of 2 hours
- a submission of 8K+ in the span of 4 hours

For more information, see [Creative Audit Best Practices](best-practices-for-submitting-creatives-for-audit.md).

## Auditing feedback

Buyers can choose to receive automatic notification emails about their creatives. For additional information, see [Managing Notification Recipients](managing-notification-recipients.md). If your creative has not passed our platform audit, your notification will include additional details regarding why the creative failed the platform audit. For more information, see [Creative Standards](../invest/creative-standards.md).

## Expired creatives

If your creative has not run and has not been modified in 45 days, then it will be automatically deactivated and will not serve on any inventory. Email notifications will go out automatically to the corresponding members regarding those deactivated creatives. Buyers do not have to re-submit deactivated creatives for auditing. They can simply reactivate them.

## Third-Party tracking pixels

Adding a pixel directly to an existing creative will normally cause the creative to be re-audited. However, since third-party tracking pixels go through an independent audit process, you can add third-party tracking pixels to creatives without causing the creatives themselves to be re-audited. For more information about third-party tracking pixels, see [Third-Party Tracking Pixels for Creatives](third-party-tracking-pixels-for-creatives.md).

## PSA-Enabled creative verification

Creatives that use a supported verification vendor to block delivery of a creative on certain content will be labeled "PSA Enabled". Instead of the actual creative, PSA-enabled creatives serve as backup creatives in the event of a block by the verification vendor. Supported verification vendors include DoubleVerify, AdXpose, AdSafe Media, and Brand.net. Microsoft Advertising has worked with each of these verification vendors to ensure that their tags can be configured for use on our platform. The buyer's verification vendor should be able to help with setting up an appropriate backup creative for Microsoft Advertising.

Here are some requirements to note:

- The verification vendor tags must be trafficked directly in our system. They cannot be in a third-party ad server.
- Backup creatives must meet all our standard creative guidelines, with the only exception being that it may rotate brands, as long as they are all PSAs.
- Backup creatives must display an actual creative for an organization that is a non-profit, non-denominational, and non-partisan. Microsoft Advertising recommends Ad Council creatives.

## Malvertising

Creatives submitted to Microsoft Advertising for auditing will be audited using both manual and automated processes. All active creatives regardless of whether they have been submitted for auditing will be continuously monitored for malvertising prevention.

Use the [Support Form](https://support.ads.microsoft.com) to submit questions about Sherlock automated auditing. Under the **Request Type**, select **Anti-Malvertising**.

## Related topics

- [Creative Standards](creative-standards.md)
- [Select an Audit Option for a Creative](select-an-audit-option-for-a-creative.md)
