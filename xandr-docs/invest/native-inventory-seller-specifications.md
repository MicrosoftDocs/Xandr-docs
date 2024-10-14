---
title: Microsoft Invest - Native Inventory Seller Specifications
description: This page outlines requirements defined by sellers for serving creatives on their native ad inventory. It can also help troubleshoot creatives that aren't serving.
ms.date: 10/28/2023
---

# Microsoft Invest - Native inventory seller specifications

Sellers of native ad inventory define requirements you must meet to serve creatives on their inventory. The specifications on this page
outline the requirements for individual sellers and allow you to compare requirements across the various sellers if you want to target only specific sellers. This page might also help troubleshoot if your creatives aren't serving on the sellers you're expecting.

> [!NOTE]
> [Buying Native Inventory](./buying-native-inventory.md) provides instructions for a global approach in which you reach all sellers simultaneously with a single campaign. Scaling is the approach we recommend over using any of the seller-specific settings shown here.

## Creative settings

Creatives that will serve on native inventory require specific settings when the creative is added. To add a creative, navigate to the
**Creative Manager** screen. Select **Create New** and create a single creative.

## Target your inventory

When you set up your line item you need to target your inventory to reach the seller's inventory. See [Buy-Side Targeting](./buy-side-targeting.md) for more information.

## Seller-specific guidelines and settings

Shown below are seller-specific guidelines and requirements that you must follow to serve on that seller's inventory. All sellers listed here use a **Type** of **Native**.

If a parameter is not mentioned in the tables below, enter whatever values make sense for your line item. Any value entered in a field listed as "Not supported" will be ignored. For detailed information on additional fields and uploading a native creative see [Add a Creative](./add-a-creative.md) and [Add Creatives in Bulk](./add-creatives-in-bulk.md). You can also review our [Native Sell-Side Best Practices](https://download.microsoft.com/download/6/f/7/6f755603-e9af-4148-9e52-02e1fb7262b0/xandr/Sell-Side-Native-Best-Practices.pdf).

> [!WARNING]
> Do not use JavaScript piggyback pixels on native creatives. Only image pixels can be used on native creatives.

## AdYouLike

| Parameter   | Value/Limit   |
|:---|:---|
| Member ID | 7664 |
| Landing Page | [https://support.adyoulike.com/](https://support.adyoulike.com/) |
| Title | 60 character maximum |
| Description | 200 character maximum |
| Icon (sizes in pixels) | 300 pixels |
| Image (sizes in pixels) | Recommended 1200x627 |
| Call to Action Text | 50 character maximum |
| Sponsored By | 25 character maximum |
| Platform Audit (Creative Attributes tab) | Required |

### Creative best practices

- **Evoke Emotion**: Associate your product or service with an emotion, i.e, Try to make the user recall memories or familiar and well-liked situations.
- **Help users project themselves**: Show your product or service in action by giving priority to close-up pictures. Use visuals that are clear and visible. (no brand logo, no text)
- **Tell a story**: Use context words with time, motion or insight. Make the user want to find out more; the more words, the more interactions.
- **Create an independent headline**: Users must understand your headline regardless of the description.

## Axelspringer

| Parameter   | Value/Limit   |
|:---|:---|
| Member ID | 7823 |
| Title | 25 characters recommended |
| Description | 80 characters recommended |
| Icon (sizes in pixels) | No icon is required |
| Call to Action Text | 20 characters recommended |

## Figaro Medias

| Parameter   | Value/Limit   |
|:---|:---|
| Member ID | 3273 |
| Title | 25 character maximum |
| Description | 90 character maximum |
| Image (sizes in pixels) | Recommended 1200x520 |
| Call to Action Text | 15 character maximum |
| Sponsored By | 25 character maximum |

## Kargo

| Parameter   | Value/Limit   |
|:---|:---|
| Member ID | 8173 |
| Title | - Length: 25 characters maximum<br> - is_required: yes |
| Description | - Length: 90 characters maximum<br> - is_required: no |
| Icon (sizes in pixels) | - min_width: 80<br> - min_height: 80<br> - is_required: no |
| Image (sizes in pixels) | - min_width: 620<br>- min_height: 375<br>- is_required: no |
| Call to Action Text | - Length: 14 characters maximum<br> - is_required: no |
| Sponsored By | - Length: 90 characters maximum<br> - is_required: no |
| Video | - maxduration: 30<br> - minduration: 5<br> - Protocol: VAST 2.0, VAST 3.0<br> - API: VPAID 2.0<br> - is_required: no<br> - recommendations: Less than 15 seconds, 16:9 ratio |

## L'Agora

| Parameter   | Value/Limit   |
|:---|:---|
| Member ID | 7037 |
| Title |  - 25 character maximum<br> - Advertiser/brand name preferred<br> - Could be used to resume the offer or service or as a Call to Action |
| Description | 90 character maximum |
| Icon (sizes in pixels) | Not supported |
| Image (sizes in pixels) |  - 1.9:1 ratio<br> - 1200x638 |
| Call to Action Text | Not supported |
| Sponsored By | Not supported |

L'Agora native adspaces or widgets are displayed alongside page content, which provide superior interaction and engagement to traditional display advertising. As a buyer, when you set up a line item to buy L'Agora, you will be bidding on a slot within the widget.

### Creative guidelines and best practices

| Category | Best Practices and Guidelines |
|:---|:---|
| **Text** |  - We highly recommend short text that is easy to understand with attractive offers.<br> - May not contain contact details as telephone number.<br> - Do not overuse capital letters or exclamation marks. |
| **Images** | - Images must be clearly relevant to the product or service being advertised.<br> - There should be a clear, simple, attractive, and logical link between the image and the copy.<br> - Avoid images with text embedded directly in the image. The text could easily be distorted depending on the adjustments made when the image is rendered.<br> - Images that represent your target (images of people) generate high engagement.<br> - Images that represent your product perform well. Don't mislead users by showing products that are not available or are not the ones that you are selling.<br> - Sexually suggestive images are not allowed. Images should be appropriate for a general audience.<br> - Opt for bright, eye-catching images. Avoid black and white images, as they will tend to blend in with the other elements of the galleries around them.<br> - The resolution of the image is important. Low quality images will appear blurry and adversely affect the impact of the ad.<br> - Images must not contain your logo.<br> - Images must not have borders.<br> - Images must be static (no movement). |

### Prohibited products and services

You may not promote any of the following products or services using the L'Agora Network. This is not an exhaustive list, and it may change without notice.

- Weight Loss
- Sexual Health
- Ringstone/Mobile subscriptions
- Sexual References
- Get Rich Quick
- Sexually Suggestive
- Mobile app downloads
- Moderate Nudity
- Sexual Toys and Accessories
- Strip Club/Gentlemen Club
- Underwear/Lingerie

Generally speaking, L'Agora does not allow you to promote any products or services in any of these categories that is illegal in any applicable jurisdiction.

## Leboncoin

| Parameter   | Value/Limit   |
|:---|:---|
| Member ID | 3296 |
| Title | 50 character maximum (mobile) |
| Description | 60 character maximum (mobile)<br>3 line maximum (mobile) |
| Icon (sizes in pixels) | Do not use |
| Image (sizes in pixels) | Recommended 600x315<br>Minimum 300x160 |

Leboncoin lets advertisers and marketers display sponsored content, products and services within the native ad units available on [leboncoin.fr](https://leboncoin.fr/").

When you set up your Inventory Targeting, include the following:

- Schibsted Media Group
- FR-Leboncoin-app_phone_android
- FR-Leboncoin-app_phone_ios
- FR-Leboncoin-app_tablet_android
- FR-Leboncoin-app_tablet_ios

## LiveIntent

| Parameter   | Value/Limit   |
|:---|:---|
| Member ID | 8171 |
| Title | 50 characters maximum; 25 characters minimum |
| Description | 90 characters maximum |
| Icon (sizes in pixels) | - 1:1 aspect ratio<br> - 100x100 minimum |
| Image (sizes in pixels) | - 1.91:1 aspect ratio<br> - 1200x627 |
| Call to Action Text | 15 characters maximum |
| Sponsored By | 25 characters maximum |
| Platform Audit (Creative Attributes tab) | Not required |
| Video | Not supported |

For additional information about LiveIntent API, see [LiveIntent Landing Page](https://support.liveintent.com/programmatic-bidding-api/).

## Mittmedia

| Parameter   | Value/Limit   |
|:---|:---|
| Member ID | 9234 |
| Title | 60 character maximum |
| Description | 250 character maximum |
| Icon (sizes in pixels) | 300 pixels |
| Image (sizes in pixels) | 4:3 ratio, recommended 1000x562 |
| Call to Action Text | None |
| Sponsored By | 25 character maximum |
| Platform Audit (Creative Attributes tab) | Required |

## Mopub

| Parameter   | Value/Limit   |
|:---|:---|
| Member ID | 1813 |
| Title | 25 character maximum |
| Description | 100 character maximum |
| Icon (sizes in pixels) | 80x80 minimum |
| Image (sizes in pixels) | Recommended 712x400; minimum 350x350 |
| Call to Action Text | 15 character maximum |
| Sponsored By | - 50 character maximum<br> - Advertiser name |

Mopub native ads match the look and feel of an app's user interface. Here are a few additional tips recommended by Mopub to get the most out of your native ads:

- Leverage the five required assets for optimal performance.
- A/B test different copy and CTA to see which performs best, then scale.
- Native delivers on client objectives. High CTR (2-4%) is great for content marketing and driving page views.
- Re-use FBX or other social assets for quick creative.
- Native supports all UTF-8 language & alphabets.
- Expect a delay in impression notifications after auction wins due to pre-caching.
- Do not use macros in URLs in the imptracker field.
- Host on stable CDNs and ensure you don't return broken links.
- Always test creatives with the sample app and proofread content.

## MSN

| Parameter | Value/Limit |
|:---|:---|
| Member ID | 280 |
| Title | 25 character maximum |
| Description | 300 character maximum |
| Icon (sizes in pixels) | 1:1 aspect ration |
| Image (sizes in pixels) | 1200x627 |
| Sponsored By | 25 character maximum |

### Best practices

- Turbo-charge your call-to-action: Immediately highlight your main point with eye-catching wording to create urgency and drive engagement.
- Choose compelling images: People, particularly shown experiencing an emotion associated with your headline, increase impact. Also, avoid text overlays on image assets.
- Center main content: Avoid clutter and ensure important visual elements, particularly people, are centered in your image asset.
- Be bold with color: Use vibrant colors to create focus and interest in your native ads.

## Nativo

| Parameter | Value/Limit |
|:---|:---|
| Member ID | 8035 |
| Title | - 60 characters recommended <br> - 80 character maximum |
| Description | - 90 characters recommended <br> - 120 character maximum |
| Icon (sizes in pixels) | - JPG or PNG <br> - 150px75px <br> - Transparent background |
| Image (sizes in pixels) | - JPG or PNG <br> - 800x600 recommended <br> - 3MB max |
| Call to Action Text | Not supported |
| Sponsored By | 90 character maximum |

Nativo reserves the right (but has no obligation to) to decline to run or link to any advertiser-provided content, assets, products, services or campaign (or any component thereof) (collectively, the “Content”), without notice, in our sole discretion. This may include Content that does not follow federal or state law, FTC guidance, Nativo’s own brand guidelines (including these Content Guidelines), or publisher guidelines. These Content Guidelines are subject to change at any time.

Nativo is not responsible for securing or enforcing the copyright, trademark or other intellectual property rights in any Content a client provides for distribution through a Nativo campaign. Further, all Content must reflect best practices in truth-in-advertising and consumer protection standards, as more specifically outlined in [Nativo Native Advertising Guidelines](https://www.nativo.com/native-advertising-guidelines-advertisers). For example, content must not be false, misleading, or deceptive, and an advertiser must have a reasonable basis to support all advertising claims in the Content.

This is not an exhaustive list of prohibited or restricted content on the Nativo platform. This list does not constitute, and should not be used as a replacement for, legal advice. Each brand is solely responsible for determining the legality of its ad content. If you have any questions about legal issues related to your Content, including with respect to clearance obligations or Nativo truth-in-advertising requirements, you must consult your own legal counsel.

| Content Category | Description |
|:---|:---|
| **Prohibited Content** | The following types of Content are NOT permitted on the Nativo platform: <br> - Adult Content, Products, or Services <br> - Children under 13 <br> - Dangerous Items <br> - Defamation and Libel <br> - “False News” <br> - Fear or Scare Tactics <br> - Free Streaming Sites- <br> - “Get Rich Quick” Pyramid Schemes <br> - Hateful Content <br> - Herbal or Homeopathic Remedies <br> - Illegal Activity <br> - Illicit Drugs <br> - Illicit Drug Paraphernalia <br> - Name or Likeness of an Individual <br> - Online Poker/Gambling <br> - Pay Per Call (900 numbers) <br> - Politics & Religion <br> - Pregnancy and Fertility Related Products <br> - Psychics <br> - Replicas <br> - Sensitive Health Topics <br> - Spam and Mail Fraud <br> - Surveillance Equipment <br> - Tobacco <br> - Third-Party Rights Violation |
| **Restricted Content** | The following types of Content will be flagged for further review by Nativo: <br> - Alcohol <br> - Brick and Mortar Gambling & Gaming <br> - Claim Substantiation <br> - Contraceptives <br> - Cryptocurrencies <br> - Dating Services <br> - Diamonds and Jewelry <br> - Endorsement and Testimonials <br> - Financial Services <br> - Green Products <br> - Loan companies <br> - Made in USA Products <br> - Online Pharmacies <br> - Pharmaceutical and Medical Procedures <br> - Political <br> - Profanity <br> - Rehab Providers <br> - State Lotteries <br> - Supplements <br> - Weight Loss Claims |

> [!NOTE]
> Find more information on Nativo’s content guidelines, visit [Nativo Content Guidelines](https://www.nativo.com/policies-and-guidelines).

## Outbrain

| Parameter | Value/Limit |
|:---|:---|
| Member ID | 7597 |
| Title | - 40 characters or less recommended <br> - 60 character maximum |
| Image (sizes in pixels) | - 1200x627 <br> - 1.91:1 ratio <br> - Maximum 1 MB |
| Sponsored By | 25 character maximum (shorter preferred) |

Outbrain's network exposes all-direct-code-on-page widgets that are customized per publisher for the maximum native look-and-feel. The network contains multi-Recommendation widgets, yielding the best results for marketers looking for engaged users, and In-Feed widgets, yielding best performance to marketers looking for high exposure to their brand.

### Inventory and setup

- Mobile Web and Desktop
- Global publisher availability
- Accessing via a deal is recommended to achieve better network accessibility

### Guidelines and best practices

| Category | Best Practices and Guidelines |
|:---|:---|
| **Best Practices** | - Properly label your content <br> - Draw from social media when determining what types of headlines to use <br> - Use copy to smoothly lead the reader to your intended next step <br> - Do Not use inaccurate, misleading, or overly sensational headlines or ad copy <br> - Do Not write headlines that are "too good to be true" <br> - Do Not create articles with duplicate content based on another affiliate offer <br> - Do Not encourage accidental clicks by implementing ads (or images) that appear to be organic content |
| **Content Guidelines - Prohibited Categories** | - Adult <br> - Controlled or Illegal Substances <br> - Hate, Violence, or Discrimination <br> - Gambling <br> - Fake News <br> - Malware <br> - Religion (Cannot promote one religion over another) <br> - Unsafe Products or Supplements |
| **Landing Page Guidelines** | - No excessive overlays/pop-ups <br> - No misleading advertising methods <br> - Must be authentic <br> - Must be updated/current |
| **Headline** | - No inaccurate, misleading, or overly-sensational headlines <br> - No offensive headlines <br> - No excessive use of capitalization <br> - Attention to grammar and punctuation <br> - No excessive use of symbols |
| **Image Guidelines** | - Relevant to the linked content <br> - Good quality <br> - Cannot employ deception to entice a click <br> - No nudity or sexual imagery <br> - Not designed to provoke, offend, or shock <br> - No circles or arrows placed <br> - No violence, gore, or dead bodies <br> - No zoomed-in body parts <br> - No before/after photos |

> [!NOTE]
> You can find Outbrain's full content guidelines [here](https://www.outbrain.com/amplify/guidelines/).

## Plista

| Parameter | Value/Limit |
|:---|:---|
| Member ID | 7790 |
| Title | - 25 characters recommended <br> - 50 character maximum |
| Description | - 70 characters recommended <br> - 100 character maximum |
| Icon (sizes in pixels) | Not supported |
| Image (sizes in pixels) | - 600x600 or greater <br> - Maximum 1 MB |
| Call to Action Text | Not supported |
| Sponsored By | - 50 character maximum <br> - Required: Must be the brand name |

### Plista: Best practices

The following are some recommended creative best practices for serving on Plista:

- Do not embed any text in the image.
- Use between 3-4 creatives.
- Make use of images that elicit positive feelings in the observer. A strong emotional impact gets the attention of the user.
- Highlight the advantages of your product by using, for example, close-ups, packshots or application examples. Be sure to use clear colors and sharp contours so that your motif stands out immediately.
- The ad should be pleasing to the eye. Using natural colors help to accomplish this while maintaining a native feel.
- Address the user personally to achieve a positive effect on the CTR.
- Match your ads with your landing page and make sure that the advertised offers in your ad can be found on your landing page.
- Keep your promise: when users do not know what to expect on your website, the visit will often be cancelled prematurely.

## Ringier

| Parameter | Value/Limit |
|:---|:---|
| Member ID | 9178 |
| Title | 25 characters maximum |
| Description | 75 characters maximum |
| Image (sizes in pixels) | 1200x627 px and 1200x1200 px |
| Targeting | Options: <br> - Sociodemographic <br> - Interest <br> - B2B (business-to-business) |

## Sanoma Finland

| Parameter | Value/Limit |
|:---|:---|
| Member ID | 7459 |
| Landing Page | Required |
| Title | 80 character maximum |
| Description | 150 character maximum |
| Image (sizes in pixels) | - 2:1 ratio, 1200x628 recommended <br> - File types: jpg, png <br><br> **Note**: images will be scaled down to accommodate placement size |
| Sponsored By | Required |

### Sanoma Finland: Best practices

- Land your ads on the client's content instead of a product page.
- Ensure that the ad matches the landing page content.
- Write the ad content according to the selected media.
- Content is what's important - avoid selling too aggressively.
- Utilize the wide reach of media to get more readers to the client's content.

## Schibsted Norway

| Parameter | Value/Limit |
|:---|:---|
| Member ID | 1860 |
| Title | 50 character maximum |
| Icon (sizes in pixels) | - Logo <br> - 1x1 ratio <br> - Maximum 150x150 |
| Image (sizes in pixels) | - 1.91:1 ratio <br> - 1200x628 |

You can serve native creatives on Schibsted Norway's desktop, mobile web and mobile app inventory. You can preview your native creatives to see what they'll look like on Schibsted websites. Use the following URLs, replacing *Xandr_creative_id* with your creative ID.

| Website | Category | Desktop? | Tablet Web? | Tablet App? | Smartphone Web? | Smartphone App? | Preview URL |
|:--|:--|:--|:--|:--|:--|:--|:--|
| [e24.no](https://e24.no/) | News | Y | Y | Y | Y | Y | **Desktop**: [Link](https://e24.no/?ast_override_div=ad-smartboard_1:Xandr_creative_id) <br> **Mobile web**: [Link](https://e24.no/?ast_override_div=ad-board_3:APPNEXUS_CREATIVE_ID) |
| [vg.no](https://www.vg.no/) | News | Y | Y | Y | Y | Y | **Desktop**: [Link](https://www.vg.no/?ast_override_div=ad-front-smartboard_1:Xandr_creative_id) <br> **Mobile web**: [Link](https://www.vg.no/?ast_override_div=ad-front-board_1:Xandr_creative_id) |

When you set up your targeting, you'll need to target **Schibsted Media Group (3296)** and the **domains** listed in the available inventory table.

## Sharethrough

| Parameter | Value/Limit |
|:---|:---|
| Member ID | 3425 |
| Title | - 90 character maximum <br> - The Title is where the bulk of storyline gets told and should be as long as possible to engage the user |
| Description | 140 character maximum |
| Icon (sizes in pixels) | - A smaller version of the Image that is uploaded, to be displayed on mobile devices. <br> - A mobile thumbnail is recommended to be greater than 320x180 |
| Image (sizes in pixels) | - Main image <br> - 16:9 ratio <br> - Minimum 800x450 <br> - Maximum 100 KB |
| Sponsored By | - 40 character maximum <br> - Required: Must be the brand name |
| Platform Audit (Creative Attributes tab) | Required |

You can buy native inventory and promote sponsored content on premium websites using <a href="https://www.sharethrough.com/" class="xref"
target="_blank">Sharethrough</a>. The look and feel of Sharethrough's inventory, known as "widgets," are tailored to each partner on the Sharethrough network for a native experience. When you set up a line item to buy Sharethrough, you will be bidding on the in-feed space where your native ad will display.

> [!NOTE]
> Buyers can only buy on a CPM basis.

You can preview your creative in the [Sharethrough Native Ad Generator](https://generator.sharethrough.com/dsp).

## Taboola

| Parameter | Value/Limit |
|:---|:---|
| Member ID | 3364 |
| Landing Page | Landing URL character maximum is 2048 |
| Title | - Required <br> - 35 - 45 characters, 60 maximum |
| Description | Not supported |
| Icon (sizes in pixels) | Not supported |
| Image (sizes in pixels) | - 1000 x 600px minimum (Feed) <br> - Image file: 1 MB Max, JPEG preferred |
| Call to Action Text | 15 characters maximum |
| Sponsored By | - The name of the brand associated with the ad <br> - 30 characters maximum |
| Platform Audit (Creative Attributes tab) | Required |
| Video | - Media Type: MP4, MOV <br> - 3rd Party Tag Specifications: VAST 2.0, VAST 2.0 with VPAID 2.0 JS, VAST 3.0 <br> - Video Size Limit: 150 MB <br> - Bit Rate: >=2500 kbps <br> - Video length: 6-30 seconds (preferred), 90 seconds maximum |

[Taboola](https://taboola.com/) helps people discover what's interesting and new on the open web, by recommending products and services to consumers while they are in that discovery mind set. The look and feel of Taboola's Infeed Placements are customized to each partner on the Taboola network, to provide a seamless user experience.

### Benefits of buying programmatically from Taboola

- **Exclusive Inventory** - Taboola placements are hard-coded on publisher's sites in multi-year agreements. Taboola is ads.txt
  compliant.
- **High Impact Units** - In-Feed and Homepage Placements capture user attention when users are looking for what's next.
- **Use Existing Native & Social Assets** - Extend your existing social and native campaigns into familiar ad formats.
- **For Video, buy on a CPM**
- **For Native Display, buy on a Viewable CPM** - Guarantees 100% viewability
- Transact via **Open Exchange** and/or **PMPs**

### Ad products

- **Taboola Native Display** - Activated through DSP via open auction or PMPs (pricing models: vCPM - guarantees 100% viewability, or CPM)
  - High impact native placements, including Top of Feed, Homepage as well as an Ad Adjacency solution are available via PMP.
- **Taboola Video** - Activated through DSP via open auction or PMPs (pricing model: CPM)
- **Native Video** - Soon to come with Microsoft Invest.

### Supply types

Taboola's inventory is exclusive via hard-coded placements through multi-year publisher partnerships. Taboola is ads.txt compliant.

- **Feed** - Taboola Feed brings the scrolling newsfeed experience customers love on social networks across our publisher partnerships.
- **Open Web Editorial Placements** - Taboola's open web placements position your brand seamlessly into the content experience of
  thousands of the world's top sites.
- **In-App/SDK** - Take full advantage of Taboola's premium in-app supply, across iOS and Android devices on traditional and utility apps using Taboola's proprietary SDK.
- **Native Video** - Add a title and brand name to existing video assets to create a more engaging video experience for users, soon to come with Microsoft Invest.
- **Taboola News** - Taboola News is an editorial environment pre-installed in highly visible device placements, enabling you to reach people at pivotal moments throughout their day, the moment they open their phones.

### Brand safety

- Control the placement and the content that surrounds your ad with a high impact unit available for both native display and video.
- Ad Adjacency - Create a buffer between your ad placement and any other sponsored placement, surrounding your brand message by high, organic content.
- Taboola maintains partnerships and integration with IAS, supporting DoubleVerify.

### Native creative best practices

| Category | Best Practices and Guidelines |
|:---|:---|
| **Image Best Practices** | - People are always preferable - Even better if they're at medium zoom from the shoulders-up, or even closer. <br> - Avoid image clutter. Clean images with a single center of focus will help you stand out. <br> - Utilize eye-catching colors to attract the user's attention. |
| **Title Best Practices** | - Taboola recommends running titles that are 35 - 45 characters, 60 maximum <br> - Your title can be a powerful targeting tool. <br> - Call out your audience or your product when possible. <br> - Front-load titles with an eye-catching main point. <br> - Numbered lists can be a good way to entice a user to click. <br> - Intrigue and mystery can help draw in users. <br> - Don't forget that titles should be capitalized, just as you would an article headline. |

> [!NOTE]
> To know more, you can visit [Taboola's Native and Video Creative Best Practices](https://help.taboola.com/hc/en-us/articles/360026664414-Programmatic-Creative-Best-Practices).

### Ad policies

Refer to Taboola's [Help Center](https://help.taboola.com/hc/en-us/categories/115001003987) to review the Advertising Policies which include restricted or prohibited content, products, and services.

### Contact Taboola

Reach out to your Taboola representative if you have any questions. If you do not have a Taboola rep, or would like to request more information - send an email to [programmatic@taboola.com](mailto:programmatic@taboola.com) with the subject line "Opt in to Taboola".

## Tamedia

[Tamedia](https://www.tamedia.ch/) provides over 700 million native impressions per month, mainly in the Swiss market. Across its News and Classified websites, with a reach over 85% of Swiss users, buyers have the opportunity to operate their native campaigns at scale. Target buyer Tamedia AG (3646).

## TripleLift

| Parameter | Value/Limit |
|:---|:---|
| Member ID | 1314 |
| Title | 30 character maximum |
| Description | 200 character maximum |
| Icon (sizes in pixels) | - Logo <br> - 300 pixel minimum <br> - jpg or transparent png recommended <br> - Recommend two versions (light and dark) |
| Image (sizes in pixels) | - Recommended 320x180 <br> - Aspect ratio 16:9 <br> - Maximum 30 KB <br> - No text, logos, or animations |

### General guidelines

| Category | Guidelines |
|:---|:---|
| **Third-Party Trackers** | All 3rd party trackers are accepted as long as they are 1x1 image tag. All trackers must be secure (https://). |
| **Creative technical attributes** | The creative has to be self-audited or platform-audited with the technical attributes **Image** (Technical attribute ID 1) and **Native: In-Feed Standard** (Technical Attribute ID 93) in order to pass TripleLift's Ad Quality Profile on the Microsoft Advertising platform. |
| **Suggested Do's and Don't's** | - Do choose engaging photos. <br> - Do use products set in real environments. Historically, these have tended to perform better than products in isolation. <br> - Do pick a click-through URL that is somewhat associated with the creative. <br> - Do explore all the image options at your fingertips. From blogs to product pages, you likely have a treasure trove of impactful images. <br> - Don't use images with too much text. <br> - Don't crop the image. TripleLift will ensure the image fits perfectly across every placement. <br> - Don't use an image with a logo overlaid on top. <br> - Don't use banner ad creative. |

## UIM

| Parameter | Value/Limit |
|:---|:---|
| Member ID | 1578 |
| Landing Page | `https://web.de/www.gmx.de/www.1und1.de` |
| Title | 25 character maximum (including spaces) |
| Description | 45 character maximum (including spaces) |
| Icon (sizes in pixels) | Not supported |
| Image (sizes in pixels) | - 500x500 minimum <br> - 1200x1200 recommended <br> - Valid file types: jpg, png <br> - File size must be less than 2 MB <br> - 300x250 display/scale down to 1:1 mobile |
| Call to Action Text | Not supported |

### Recommendations and guidelines

| Category | Recommendations and Guidelines |
|:---|:---|
| **General Recommendations** | - Note that a semi-transparent overlay with your text is placed over the image. It occupies approximately 300x100 pixels in the lower image area. <br> - Our headline = 1 line and the description = 2 lines <br> - Only German language |
| **Teaser Text Guidelines** | - No special characters in your text <br> - No exclamation marks |
| **Image Guidelines** | - No purely text-based graphics <br> - No plain text as image <br> - No frame around your image <br> - No pure logo as image <br> - No important image component in the margin, as image can be scaled on smaller screens. Position important parts centrally. <br> - Image has to be static, not animated = GIF/JPEG 40KB maximum. |

> [!NOTE]
> For further information and examples, visit [Native Teaser (Multi Screen)](https://www.united-internet-media.de/en/products-and-solutions/nativeadvertising/native-teaser/).
