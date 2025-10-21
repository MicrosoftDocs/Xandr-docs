---
title: Microsoft Monetize - Update Creatives in bulk
description: In this page, learn to update settings for individual or multiple creatives from the Creative Manager.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Update Creatives in bulk

You can update a variety of settings for individual or multiple creatives from the **Creative Manager**.

1. Go to **Advertisers** \> **Creative Manager**.
1. Select an advertiser.
1. Select the checkboxes for the appropriate creatives that need to be updated.
1. Click the **Bulk Edit** menu from the blue toolbar that displays and select any one of these settings:

| Setting | Description |
|--|--|
| **Activate** | When you activate deactivated creatives, they typically start serving within 10 - 15 seconds with a maximum wait time of approximately 60 seconds. |
| **Associated Substantiation** | When adding or editing sensitive content, you can provide a URL to supporting documentation (substantiation) as evidence that the creative doesn't contain any false claims.<br>**Note**: This feature is currently in **Alpha/Beta**. It is still under development and may be subjected to changes without notice. Contact your Microsoft Advertising Account Representative to get it enabled. |
| **Audit** | For more information about selecting a different audit option for a creative, see [Select an Audit Option for a Creative](select-an-audit-option-for-a-creative.md). |
| **Campaign** | You can only associate creatives with campaigns that have been added previously in the system. For more information about associating campaigns with a creative, see [Associate Creatives to Campaigns](associate-creatives-to-campaigns.md) |
| **Click Tracking Test** | We typically automatically run a click tracking test when the creative is initially uploaded using the **Create New** screen. You can retest click tracking for specific creatives from the **Creative Manager** if necessary. For more information, see [Click Tracking](click-tracking.md). |
| **Competitive Exclusions** | This is the ability to apply Competitive Exclusions settings in bulk to one or multiple selected creatives in Creative Manager. For more information, see [Competitive Exclusions](competitive-exclusions.md). |
| **Creative Properties** | This is the ability to apply a Media Type for Banner creatives in bulk to one or multiple selected creatives in Creative Manager. For more information, see [Applying Media Types and Templates to Banner Creatives](applying-media-types-and-templates-to-banner-creatives.md). |
| **Deactivate** | When you deactivate creatives, they typically stop serving within 10 - 15 seconds with a maximum wait time of approximately 60 seconds. |
| **Delete** | You should delete creatives when you are approaching your object limit, or when you want to get rid of unnecessary or accidentally created creatives for a particular advertiser. For more information about object limits, see [Viewing Your Object Limits](viewing-your-object-limits.md).<br>**Tip**: Creatives that have not served or been modified within the last 90 days are good candidates for deletion. To find such creatives, click the **Advanced Filter** button, select the **Last 90 days** radio button from the **Last modified** section in the **Filters** dialog, and click **Apply**. Deletions are permanent and cannot be reverted. In the case where a deleted creative was the only creative that was associated to an active line item or campaign, the line item or campaign will not serve. Although deleted creatives continue to be available in reporting, you will no longer have visibility into their specific settings such as third-party URL or tag, impression tracking pixels, and creative attributes. |
| **Duplicate** | Since the system will only allow you to associate the same creative with up to three third-party tracking pixels, you may want to duplicate a creative so that you can get around this limitation. You should also duplicate creatives when you want to reuse a creative's settings, which will only require minor changes to those settings, instead of manually adding a new creative to the platform altogether. |
| **Landing Page URL** | Using this option you can set the Landing Page for multiple creatives at once, and the user's browser will be redirected to the landing page that is configured for the creatives. You can also set the Landing page URL at the Line item level. |
| **Line Item** | You can only associate creatives with line items that have been added previously in the system. For more information about associating line items with a creative, see [Associate Line Items with a Creative](associate-line-items-with-a-creative.md). |
| **Move to Folder** | You can move creatives to any existing folder. |
| **Name** | Instead of being forced to delete creatives due to a name change, you can easily rename them. |
| **Resubmit for Adx Audit** | When a user chooses to submit their creative for Microsoft Advertising's Platform Audit, we simultaneously submit their creative for Google's "AdX Audit". This menu option provides a user an easy way to re-submit their creatives to Google's AdX audit if they received a 'failed audit' update from third-party Google. For more examples of failures from AdX, see [ADX Feedback and FAQ](../bidders/adx-feedback-and-faq.md). |
| **Resubmit for SSL Audit** | When a creative is uploaded, an SSL audit is initiated. If Microsoft Advertising determines that the creative contains non-secure attributes, then the creative's SSL audit status will be processed as failed since it won't be able to serve on secure inventory. You can re-run this SSL audit to validate that the creative is secure and can serve on secure inventory. |
| **Run a report** | After you select **Run Report**, you'll be taken to the Member **Analytics Report** settings screen where you can set additional parameters. For more information about running a report, see [Member Reporting](network-reporting.md). |
| **Tracking** | Pixels / Tracking in our docs. For more information, see [Configuring Tracking for Creatives](configuring-tracking-for-creatives.md). |

## Related topics

- [Creative Types](creative-types.md)
- [Add Creatives in Bulk](add-creatives-in-bulk.md)
- [Add a Creative](add-a-creative.md)