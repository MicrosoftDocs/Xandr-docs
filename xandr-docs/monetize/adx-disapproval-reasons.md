---
title: Microsoft Monetize - Google Ad Manager Disapproval Reasons
description: In this article, find a list of reasons why your creative might be rejected by the Google Ad Manager along with the recommended action to resolve the rejection reason.
ms.date: 10/28/2023
---

# Microsoft Monetize - Google Ad Manager disapproval reasons

You may receive a disapproval reason from Google Ad Manager for various reasons.

Use the table below to better understand why your creative was rejected. The disapproval reasons are sorted in ascending order by ID (0 to 35).

| ID | Disapproval Label | Description | Recommendation |
|---|---|---|---|
| 0 | length_of_image_animation | The length of the image animation exceeds the Google Ad Manager animation length limit (30 seconds). | Revise the creative to be 30 seconds or less and re-upload it. |
| 1 | broken_url | The clickthrough URL assigned to your creative is not working properly. | Replace the clickthrough URL with one that is properly working. |
| 2 | media_not_fuctional | Something is wrong with the creative. | Retest the creative's functionality. |
| 3 | invalid_fourth_party_call | The creative makes a fourth-party call to an unapproved vendor. | Confirm that the creative's calls are being made to Google Ad Manager-approved vendors. For more information, see the relevant Google documentation. <br> If you have modified your creative content to add users to segments when the creative is viewed, this will trigger Microsoft Advertising to call User ID Syncing, which will in turn cause your creative to be rejected by Google Ad Manager due to calls to undeclared vendors. Instead of modifying your creative content so that it can make calls to User ID Syncing, you should associate segment pixels with creatives, which will not cause usersync pixels to get called. For more information, see [Associate Segment Pixels with Creatives](associate-segment-pixels-with-creatives.md). If you do decide to modify the creative content in this manner, be sure to append `&no_redir=1` to the query string of the segment ad call to prevent usersync pixels from getting called. |
| 4 | incorrect_remarketing_declaration | The creative targets consumers using remarketing lists and/or collects data for subsequent use in retargeting, but does not correctly declare that use. | Ensure that the creative explicitly states the use of targeting consumers who are leveraging remarketing lists and/or collecting data for subsequent retargeting. |
| 5 | landing_page_error | Clicking on the creative leads to an error page. | Replace the landing page URL with one that is up and running. |
| 6 | ad_size_does_not_match_ad_slot | The creative size when rendered does not match the declaration. | Ensure that the correct creative size has been associated with the creative. |
| 7 | no_border | Creatives with a white background require a contrasting border, which was missing. | Add a clearly defined border to the creative. |
| 8 | fourth_party_browser_cookies | The creative attempts to set cookies from a fourth party that is not certified. | Ensure that the creative is setting cookies from a certified fourth party. |
| 9 | lso_objects | The creative sets an LSO (Local Shared Object), such as Flash cookies, browser helper objects, or HTML5 Local Storage. | Remove all LSO objects. |
| 10 | blank_creative | The creative renders a blank at the time of Google Ad Manager's audit. | Ensure that the creative is viewable by all users. |
| 11 | destination_urls_undeclared | The creative uses rotation, but not all the destination URLs were declared. | Provide the missing destination URLs. |
| 12 | problem_with_click_macro | There is a problem with the way the click macro is used. <br><br> **Note**: All creatives must contain the Google Ad Manager `CLICK_URL_MACRO`. It must exist to pass the programmatic audit. It must be able to pass a human audit. Microsoft Advertising automatically appends this to every bid response for Google Ad Manager. | Submit a [support request](https://support.ads.microsoft.com). |
| 13 | incorrect_ad_technology_declaration | The ad technology declaration is not accurate. <br> You must declare all ad servers and data providers upon upload in order for creatives to serve on Google Ad Manager. During the audit process, Google Ad Manager checks all calls that the tag makes. If there is a discrepancy between the ad servers and data providers that were declared upon upload and the calls that the creative actually makes, your creative will be rejected. | Update the list of declared ad servers and data providers for your creative using the UI. Confirm what you have declared is accurate, and then reach out to the Microsoft Advertising audit team. If your adsever/technology vendor is not currently approved by Google Ad Manager, see [Google Ad Manager third- and fourth-party vendor declarations](https://developers.google.com/third-party-ads/adx-vendors). |
| 14 | incorrect_destination_url_declaration | The URL that you declared for this creative does not match the actual `landing_page_url`. | Ensure that the declared click-through URL matches the actual landing page URL. |
| 15 | expandable_incorrect_direction | The declared expanding direction does not match the actual direction. | Ensure that the creative is actually expanding in the direction that has been specified. |
| 16 | expandable_direction_not_supported | The creative does not expand in a supported direction. | Ensure that the creative is expanding in a supported direction. |
| 17 | expandable_invalid_vendor | The creative uses an expandable vendor that is not supported. | Ensure that the creative is using a supported expandable vendor. |
| 18 | expandable_functionality | There was an issue with the expandable creative. | Retest the expandable creative's functionality. |
| 19 | video_invalid_vendor | The creative uses a video vendor that is not supported. <br> You must declare all ad servers and data providers upon upload for creatives to serve on Google Ad Manager. During the audit process Google Ad Manager checks all calls that the tag makes. If your creative makes a call to an unapproved video vendor your creative will be rejected. | Confirm that the calls your creative makes are to Google Ad Manager-approved video vendors. For more information, see the relevant Google documentation. |
| 20 | video_unsupported_length | The length of the video creative is not supported. <br> If your VAST creative differs from the Google Ad Manager length parameters (15 or 30 seconds), it will be rejected. | Revise the VAST creative's duration to 15 or 30 seconds. |
| 21 | video_unsupported_format | The format of the video creative is not supported. | Save the video creative in a format that is supported. For more information, see [Video Creative Guidelines and Specifications](video-creative-guidelines-and-specifications.md). |
| 22 | video_functionality | There was an issue with the video creative. | Retest the video creative's functionality. |
| 23 | landing_page_disabled | The landing page does not conform to the Ad Exchange policy. | Ensure that the landing page associated with your creative conforms to [Google Ad Manager's policy](https://support.google.com/adspolicy/topic/1310885?hl=en&guide=1308259&rd=1). |
| 24 | malware_suspected | The creative may contain malware. | Remove all malware from the creative. |
| 25 | adult_image_or_video | The creative contains adult images or video content. | Remove any inappropriate adult images or video content. |
| 26 | inaccurate_ad_text | The creative contains text that is unclear or inaccurate. | Revise the creative text. |
| 27 | counterfeit_designer_goods | The creative promotes counterfeit designer goods. | Remove any content that promotes counterfeit designer goods. |
| 28 | pop_up | The creative causes a pop-up window to appear. | Remove the pop-up. |
| 29 | invalid_rtb_protocol_usage | The creative does not follow policies set for the RTB protocol. | Ensure that the creative conforms to policies set for the [RTB protocol](https://developers.google.com/authorized-buyers/rtb/response-guide/bid-multiple). |
| 30 | raw_ip_address_in_snippet | The creative contains a URL that uses a numeric IP address for the domain. | Remove calls made to IP addresses. |
| 31 | unacceptable_content_software | The creative or landing page contains unacceptable content because it initiated a software or executable download. <br> A creative that initiates a software or executable download goes against the Google Ad Manager and Microsoft Advertising policy. | Confirm that the creative does not initiate a software or executable download. |
| 32 | unauthorized_cookie_on_google_domain | The creative sets an unauthorized cookie on a Google domain. | Remove the calls that set unauthorized cookies. |
| 33 | undeclared_flash_objects | Flash content found where no Flash declared. | Remove all Flash content from the creative. |
| 34 | invalid_ssl_declaration | SSL support declared but not working correctly. <br> Google Ad Manager allows buyers to bid on secure inventory. If your creative is submitted as a secure creative, then Microsoft Advertising will pass back a secure flag in the bid response. If Google Ad Manager finds that your creative is not actually SSL supported, it will be rejected. | Remove any unsecure content from the creative. |
| 35 | direct_download_in_ad | Rich Media - Direct Download in Ad (For example, a PDF download). <br> A direct download that results from clicking on the creative goes against the Google Ad Manager and Microsoft Advertising policy. | Remove any direct downloads from the creative. |

If you can't locate your disapproval reason in the table above, you may find it in the **Disapproved ad reasons** column of the [Google Ad Manager's Troubleshoot disapproved ads](https://support.google.com/authorizedbuyers/answer/10063840?hl=en&visit_id=638387368664163806-1106416724&rd=1) page.

If you don't see your disapproval reason listed there, you may be able to find it in [Google's Snippet Status Report](https://developers.google.com/authorized-buyers/rtb/relnotes#whats-new-in-snippet-status-report-proto-version-31). In the Snippet Status Report, search for "`enum DisapprovalReason`". The full list of Google Ad Manager disapproval reasons is contained with curly brackets {} followed by `enum DisapprovalReason`.

The disapproval reasons are in all caps. An explanation of the disapproval reason appears above each approval code, which is demarcated by two slashes (//). For example, the LENGTH_OF_IMAGE_ANIMATION disapproval code corresponds to `//The length of the image animation is longer than allowed` disapproval reason. ID numbers have been assigned to each disapproval reason. For example, `LENGTH_OF_IMAGE_ANIMATION = 1`.

## Related topics

- [Google Ad Manager Creative Audit Process](adx-creative-audit-process.md)
- [Resubmit Creatives for Google Ad Manager Auditing](resubmit-creatives-for-adx-auditing.md)
