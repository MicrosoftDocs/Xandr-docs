---
title: Creative Audit Feedback
description: Learn about the creative standards set by Xandr, Google Ad Manager, and Microsoft. The page lists dos and dont's for creatives and inventory, and reasons why a creative can get rejected. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Creative audit feedback

Microsoft Advertising has foundational policies that all creative and inventory content must follow. Creatives that violate these policies will be removed from the platform, and will be ineligible for both real-time bidding (RTB) and in-network buying. Repeated violation of these policies may result in strikes against offending members.

> [!NOTE]
> Please visit [Microsoft Advertising Policies and Guidelines](https://help.ads.microsoft.com/#apex/ads/en/n5096/0) for a full list of disallowed and restricted content. 

## Prohibited content

Ensure that your creatives and inventory do not contain any of the following.

| Ban Reason | Description |
|:-|:-|
| Creative contains deceptive content | - Creative has no clearly defined background nor border.<br>- Creative contains non-functional elements (video player interface, closing icon, etc.)<br>- Creative mimics email/messaging/social media interface implying notification or new message.<br>- Creative claims visitor is a visitor number, ex. “You’re our 100,000th visitor!”<br>- Creative features “Download/Play Now” buttons as majority of creative content |
| Displays fake errors or warnings to induce user action | - Creative imitates mobile phone interface to drive traffic<br>- Creative imitates a dialogue/OS box, displays fake errors or warnings to drive traffic |
| Enabling or permitting piracy | - Copyright-infringing pirated media content<br> &nbsp;&nbsp;- Film/TV<br> &nbsp;&nbsp;- Books<br>&nbsp;&nbsp; - Music<br> &nbsp;&nbsp;- Etc.<br>- File-sharing services without a DMCA (Digital Millennium Copyright Act) take-down policy |
| Features the sale of drugs, pharmaceuticals, or drug paraphernalia that is illegal | - Pro-marijuana content<br>- Promotion or sale of marijuana<br>- Marijuana accessories<br>- Marijuana culture sites<br>- Investment or career opportunities in the marijuana industry. |
| Features the sale of or instructions to create bombs, guns, ammunition, or other weapons | Creative advertises a site whose main purpose is to sell and promote guns or ammunition |
| Features the sale of third party government services | Advertising for government products and services that is not submitted by the government or by government-authorized entities. |
| Misappropriation of a copyright, trademark, trade secret or patent of another party | Creative deceptively uses a major brand’s logo in an offer not affiliated with that brand |
| Pornography, nudity, obscenity, or other "adult" content | - Major nudity (female nipples, genitalia, etc.)<br>- Depiction of sexual acts<br>- Escort services<br>- Realistic sex toys<br>- Sales or distribution of pornography |

For more information, see our [Part of Service Policies](../policies-regulations/index.yml).

## Disapproval reasons

The following table outlines reasons why a creative may be rejected from serving on Xandr inventory and recommendations for resolving the potential issue. Our policies apply to nearly all inventory sources with some minor exceptions. All creatives must meet these criteria in order to be approved. Xandr reserves the right to update audit policies and integrate or amend acceptance criteria at any time.

| Failure Reason | Description | Recommendations |
|:-|:-|:-|
| Auto-Refreshing Creative | Creative and/or browser tab refreshes automatically resulting in multiple impressions | Auto-refreshing creatives are not allowed. Please update the creative and re-submit it to the audit. |
| Creative brand does not match creative landing page | The brand that the creative displays and the brand of the landing page are not the same or related | It is recommended to use the creative Brand website as a landing page. |
| Creative clicks through in the same window | - The creative's landing page loads in the same page instead of opening a new window or tab.<br>- The creative loads the entire landing page into the frame. | It is recommended to update the creative in order to have a new window or tab open when a user click on the creative. |
| Creative contains content prohibited by policy | - Excessive blood or gore.<br>- Excessive or disparaging profanity.<br>- Racial slurs and hate speech.<br>- Creative advertises online-only pharmacy selling prescription drugs.<br>- Prescriptions drugs offered without a prescription. | Full Xandr policy here [Part of Service Policies](../policies-regulations/index.yml) |
| Creative does not click through properly | - The creative is clicked and does not open a landing page. <br> - Creative clicks through to unbranded landing page (ex. 404 errors, non-functional pages, etc.) <br> - Creative click opens multiple landing pages off one click. <br> - The creative is clicked, and a landing page opens, but no content loads. <br> - The creative is clicked, and a landing page loads, but an error keeps any content from being displayed. | Ensure that the creative is redirecting to a live, functional and branded landing page.<br><br>**Warning**: A landing page cannot have a geo targeting applied to it. How audit team needs to be able to see the landing page content. |
| Creative does not display a clear brand | - The creative does not display a brand.<br>- The creative displays a brand, but it is not sufficient notification. | It is advised to update the creative content in order to clearly show a brand.<br><br>**Note**: <br>**Definition of “sufficient”**<br>When evaluating a creative for appropriate brand notification, the audit team looks for at least one of three things:<br>- a logo<br>- a landing page URL<br>- a distinct brand name<br>If the only branding on the creative is a logo, then that exact logo must also be on the landing page to be sufficient. If the only branding on the creative is a landing page URL, then that must be the URL the creative has as its landing page.<br><br>**Distinct brand name** is sufficient notification in one of the following ways:<br>- The brand name is not an actual word and when it appears on the creative it cannot be confused for other, non-branded text (e.g. Cygnas)<br>- The brand name is a distinct set of actual words, and the landing page exactly matches this and/or has a distinct, matching typeface as the creative (For example, "The Best Wedding Music" goes to [thebestweddingmusic.com](https://thebestweddingmusic.com) and/or is written in red bold Helvetica on both the creative and the landing page) |
| Creative does not display properly | - Creative brands or offers are cut off.<br>- Creative displays too briefly for branding and clickthrough.<br>- Creative displays extraneous text tail. | Review and preview the creative and see if the content is displaying as expected. If it is not the case, it is recommended to update and correct the creative. |
| Creative does not meet minimum standards | - Creative does not display on certain operating systems.<br>- Creative is entirely text only. | It is recommended to update the creative to make is match with our minimum standards. |
| Creative has no assigned landing page. Please assign a campaign and resubmit | Creative has no direct landing page assigned | A landing page is mandatory to get creative approved. You can assign it at the creative UI level or at the LI level. |
| Creative improperly rotates brands or advertiser | - The creative has multiple versions with different brands under a single ID.<br>- A single creative represents and clicks through to multiple different brands' landing pages.<br>- For video creatives, a pre-roll ad for a different brand play before the actual offer.<br>If a creative is co-branded (for example, Brand X and Brand Y collaborating), the brand will be set based on which of the brands owns the landing page URL. | - Ensure that all the creatives that are rotating in the tag are all from the same brand.<br>- Ensure that the creatives are all redirecting to the creative brands’ landing page. |
| Creative is blank | Creative doesn’t render due to geo/IP issues. Creative doesn’t render due to typo/error in creative content/tag or hosted ad server issue | It is recommended to run the following checks:<br>- Check if the creative displays correctly on an external tool. If not, coming from the creative directly and not the Xandr platform. Please, correct it and resubmit it to the Xandr audit.<br>- Make sure to allowlist or unblock our previews domains in the creative ad server: adnxs.net, adnxs.com, creative-preview-an.com, audit.adnxs.net, cq-preview.adnxs.net<br>- If an Ad Verification service (Adsafe) is implemented in the creative, it is advised to use the `${IS_PREVIEW}` macro.<br><br>**Note**: We created the macro, `${IS_PREVIEW}`, to signal the ad verification vendor that the creative should render. This macro will be replaced with a 1 when we are previewing it. More information about the macro's implementation [here](./click-tracking-and-cache-busting-examples.md). |
| Creative/Landing Page prompts download | Creative or landing page prompts user to download a file | Creative that contains content that depicts, contains, or provides access to any files that execute or download without intentional user interaction are prohibited. Policy here: |
| Declared tag size does not match creative’s actual dimensions | Incorrect creative tag size. The size in Xandr UI does not match the actual size of the creative. | - Check if the declared size in the UI matches your creative size. If not, please update the declared size to make it match with your creative size.<br>- In case of a high impact or expandable creative: It is recommended to upload and create the creative as a standard banner with 1x1 (or 1x2) size. This way, we won’t look at the primary size and will focus on the expandable creative size. |
| Political creative does not contain clear “paid for by” disclaimer | US political creatives without “paid for” disclaimer | Update the creative and add the “paid for” disclaimer |

## CBA standards

All creatives must meet the Coalition for Better Ads (CBA) standards in order to serve on desktop and mobile inventory. For more information, see [Better Ads](https://www.betterads.org/standards/).

## Related topics

- [Auditing Creatives](../invest/auditing-creatives.md)
- [General Guidelines for Passing Creative
  Audits](../invest/general-creative-guidelines-to-pass-auditing.md)
