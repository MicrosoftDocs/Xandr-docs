---
title: Creative Troubleshooting FAQ
description: This topic covers Creative Troubleshooting FAQs. 
ms.date: 10/28/2023
---

# Creative troubleshooting FAQ

This page deals with FAQs on Creative Troubleshooting.

## Recommended technical specifications for creatives

There are few technical requirements imposed on creatives by Xandr's platform. A number of networks and publishers do have such requirements. Follow the recommendations listed here to ease your use of the platform and access as much inventory as possible.

**General recommendations**

Follow these recommendations when building creatives of any type:

- Limit initial load size to less than 40 KB. This will meet the [Google Display Network's limit of 50 KB](https://support.google.com/adspolicy/answer/94230?hl=en) as well.
- Xandr provides standard [Creative Templates](creative-template-service.md) for all [Supported Media Types](expandables-and-rich-media.md). You may also create your own custom templates. You can use the [Creative Template API Service](creative-template-service.md) to create your own template.
- Avoid auto-initiated audio; it's frequently blocked by publishers.

**Video**

Follow these recommendations when building video creatives:

- Use H264 video encoding
- Use MP3/AAC audio
- Use the MP4 video container format
- Use at least VAST version 2.0 (See the [VAST Documentation](https://www.iab.com/) for details.)

The VAST standard specifies that VAST creatives be represented in XML (Extensible Markup Language).

In a single-file video, the VAST XML contains only one video file. However this one video file may not be compatible with all operating systems and browsers. A multi-file video VAST XML contains many video files (to confirm, all of the same ad).The upside is that at least one video file will be compatible with all operating systems and browsers.

**Expandables**

Follow these recommendations when creating expandables:

- Use the 'click to expand' or 'mouseover to expand' methods to access the most supply.
- For more details, see [Expandables and Rich Media](expandables-and-rich-media.md).

In order to properly run expandables, the creative must expand correctly in the Impression Bus preview, in other words, when loaded outside of an iFrame. Creative must expand correctly in a friendly iFrame (an iFrame where the domain of the webpage it loads matches the domain of the webpage that it is placed on), without assistance from the publisher page. Some expandable tags only expand correctly out of friendly iFrames if the publisher declares them as being friendly with the following JavaScript code:

`var inDapIF=true; var inFIF=true; var RMIF=true;`

Unfortunately we can’t guarantee that this JavaScript will be present, so this can’t be relied on by an expandable tag.

Creative must display a backup image in an unfriendly iFrame (iFrame where the domain of the webpage it loads does not match the domain of the page that it is on), or in any environment where it cannot expand (hard). Some expandable tags rely on an iFrame buster file which is provided by the ad server and is installed on the publisher web server. This allows the expandable tag to expand out of unfriendly iFrames. We can’t guarantee that an iFrame buster file will be present on all our publishers, so your tag needs to be prepared to display a backup image in the event it cannot expand properly.

**Flash**

Follow these recommendations when building Flash creatives:

- Develop your Flash creatives to be viewable in Flash version 8 or lower
- Use the standard click variable name `clickTAG`

Flash creatives are generated using ActionScript and rely on browser plugin to properly render. The Flash file controls user interactions, so when they are clicked, they click-through to a new window by loading the following ActionScript function (depending on the version):

``` 
getURL([URL], “_blank”); (ActionScript 2.0)
navigateToURL([URL], “_blank”); (ActionScript 3.0)
```

Flash files control their own click throughs, which means that the landing page has to be defined within the Flash file which is done with a clickTAG macro. The Flash developer inserts the macro in place of where they would insert the landing page. In turn the ad server will provide the landing page by defining this “clickTAG” value in the context of a JavaScript wrapper. The advertiser can now upload a Flash file and specify the landing page. We can also dynamically pass in our click tracker, which allows the creative to track clicks.

> [!TIP]
>
> - The clickTAG macro is case sensitive. The variant of clickTAG used by the developer needs to be the same as that of the ad server in order to work. Many ad servers get around this by passing in multiple variants (ClickTag,clickTag,clicktag) with the same click URL value, hoping that one of them works. You can find the variant of clickTAG that your Flash Developer used by decompiling the Flash file.
> - Using [Tamper Data](https://addons.mozilla.org/en-US/firefox/addon/tamper-data-for-ff-quantum/), If you click on a creative and the first URL you see is the Advertiser landing page, then you know the Flash file has a hardcoded URL. Decompile the Flash file to confirm.
> - The clickTAG variants, as well as the clickTAG value, can be found by using the Developer tools for Chrome or Firefox. Right click on the creative and choose Inspect Element.Look for: “flashvars&clickTAG=\[URL1\]&clickTag=\[URL2\]"

## Creative doesn't display

**My creative isn't showing up. What's wrong?**

There are a few things you can look for before sending a ticket into Xandr Support. First, does the trafficking code (html, javascript, etc.) match the creative? A javascript tag that is interpreted as pure html (e.g. \<script\>\</script\>) should be trafficked as html. Raw javascript (e.g. var x = "my tag") should be trafficked as such. The tag code determines how that impression bus will deliver the ad (i.e. if it will be wrapped within a doc.write or not), so it is often the problem behind blank creatives.

If your tag code is correct, load a creative preview using our server URL:

`https://creative-preview-an.com/cached/creative/insert creative id here`

After refreshing a few times, if the page is blank, you should inspect the creative's tag content. Check to see if there are any glaring format errors in spacing, etc. Please note that we do not support javascript comments at this time. If the tag has comments, remove the comment wrappers:

`<!//---- {your creative content / code would be here} ----//>`

When you edit and save the creative, wait 10-15 seconds before refreshing several times to check if the changes worked.

If none of the above steps work, you can test to see if the problem is on our end: copy your tag into a text file, save it as an html, and open the html file with your browser. If it doesn't load, then the issue lies with the tag or 3rd party content. If the creative loads, the issue may be due to how we are previewing the creative. If removing comment wrappers or altering incorrect formatting doesn't remedy the problem and the creative is loading in your browser, feel free to submit a support ticket.

**Allowing our audit IPs and domains**

Another reason why the creative may not be displaying is the creative contains geotargeting elements that control where the creative is allowed to render. If this is the case, you will have to allow our Audit IPs and Domains:

- LA servers:
  - Input 68.67.139.192 /26 (netblock)
  - Input 68.67.136.192 /26 (netblock)
  - Input 68.67.139.0   /26 (netblock)
- NY office:
  - Input 207.237.150.0 /24 (netblock)
  - 68.67.164.193
  - 68.67.164.194
  - 68.67.164.195
- Offshore:
  - 115.112.103.132
  - 123.201.61.176
  - 115.248.62.88
  - 118.185.207.40
  - 14.143.143.24
  - 118.185.184.184
  - 14.98.34.200
  - 182.74.78.216
  - 14.143.179.218
  - 223.31.25.162
  - 107.178.218.71
  - 169.47.132.71
  - 169.55.107.131
  - 111.93.148.126
  - 182.72.26.38
  - 14.98.201.134
  - 38.132.110.83
  - 35.238.185.16
  - 182.75.97.18
  - 216.73.161.182
  - 2.57.168.149
  - 157.97.121.97
  - 45.146.55.72
  - 136.144.42.114
- Domains:
  - `adnxs.net`
  - `adnxs.com`
  - `creative-preview-an.com`
  - `cq-preview.adnxs.net`
  - `new-audit.adnxs.net`
  - `cq-auditor.adnxs.net`
  

**Why did I receive an email saying my creative was deactivated?**

If your creative (1) has not run and (2) has not been modified in 15 days, then it will be automatically deactivated and will not serve on any inventory. Email notifications will go out automatically to the corresponding member(s) of any deactivated creatives. As of March 2018 expired creatives will be automatically reactivating if your bidder resumes bidding with the creative.

**Ad verification services**

If your client is using Ad Verification services, the creative may not display, by default, in our Audit UI or in the impbus preview url. We have created the macro, ${IS_PREVIEW}, to signal the ad verification vendor that the creative should render. This macro will be replaced with a 1 when we are previewing it.

``` 
<IFRAME SRC="https://fw.adsafeprotected.com/rjsi/dc/54321/123456/adi/N1068.151790.ABCDE/B6797568.72;sz=160x600;click=${CLICK_URL};ord=${CACHEBUSTER}?adsafe_preview=${IS_PREVIEW}" WIDTH=160 HEIGHT=600 MARGINWIDTH=0 MARGINHEIGHT=0 HSPACE=0 VSPACE=0 FRAMEBORDER=0
SCROLLING=no BORDERCOLOR='#000000'>
    <SCRIPT language='JavaScript1.1' SRC="https://fw.adsafeprotected.com/rjss/dc/54321/455394/adj/N1068.151790.ABCDE/B6797568.72;abr=!ie sz=160x600;click=${CLICK_URL};ord=${CACHEBUSTER}?adsafe_preview=${IS_PREVIEW}">
    </SCRIPT>
    <NOSCRIPT>
        <A HREF="${CLICK_URL}https://ad.doubleclick.net/jump/N1068.151790.ABCDE/B6797568.72;abr=!ie4;abr=!ie5;sz=160x600;ord=${CACHEBUSTER}?">
            <IMG SRC="https://fw.adsafeprotected.com/rfw/dc/54321/455392/ad/N1068.151790.ABCDE/B6797568.72;abr=!ie4;abr=!ie5;sz=160x600;ord=${CACHEBUSTER}?adsafe_preview=${IS_PREVIEW}" BORDER=0 WIDTH=160 HEIGHT=600 ALT="Advertisement">
        </A>
    </NOSCRIPT>
</IFRAME>
```

In order for ad safe creatives to properly click through to their landing page from our UI and audit UI preview, adsafe_preview macro must be used in both the \<script\> and \<no script\> sections.

``` 
<IFRAME SRC="https://fw.adsafeprotected.com/rjsi/dc/23354/1869069/adi/N3867.456584.XAXIS.COM/B7976864.14;sz=300x250;pc=[TPAS_ID];ord=${CACHEBUSTER};click=${CLICK_URL}?adsafe_preview=${IS_PREVIEW}" WIDTH=300 HEIGHT=250 MARGINWIDTH=0 MARGINHEIGHT=0 HSPACE=0 VSPACE=0 FRAMEBORDER=0 SCROLLING=no BORDERCOLOR='#000000'>
<SCRIPT language='JavaScript1.1' SRC="https://fw.adsafeprotected.com/rjss/dc/23354/1869070/adj/N3867.456584.XAXIS.COM/B7976864.14;abr=!ie;sz=300x250;pc=[TPAS_ID];ord=${CACHEBUSTER};click=${CLICK_URL}?adsafe_preview=${IS_PREVIEW}">
</SCRIPT>
<NOSCRIPT>
<A HREF=”${CLICK_URL}https://ad.doubleclick.net/jump/N3867.456584.XAXIS.COM/B7976864.14;abr=!ie4;abr=!ie5;sz=300x250;pc=[TPAS_ID];ord=${CACHEBUSTER}?adsafe_preview=${IS_PREVIEW}">
<IMG SRC="https://fw.adsafeprotected.com/rfw/dc/23354/1869068/ad/N3867.456584.XAXIS.COM/B7976864.14;abr=!ie4;abr=!ie5;sz=300x250;pc=[TPAS_ID];ord=${CACHEBUSTER}?" BORDER=0 WIDTH=300 HEIGHT=250 ALT="Advertisement"></A>
</NOSCRIPT>
</IFRAME>
```

> [!TIP]
> If Your Creative Failed Audit And You See a "} catch(e){ }" in the preview, then creative is using the wrong format. Adjust the format to be a javascript url.


``` 
<script type="text/javascript">
document.write('<scr' + 'ipt src="https://bs.serving-sys.com/BurstingPipe/adServer.bs?cn=tf&c=19&mc=imp&pli=&PluID=0&ord=&rtu=-1 "></scr' + 'ipt>');
</script>
```

**How do I know if my third-party tag is HTML or JavaScript?**

Before deciding how Xandr should serve the creative, you must determine the tag format: HTML or JavaScript. HTML creatives are recognizable by their angle brackets (e.g. \<html\>). We often see issues where the tag was labeled with the wrong tag format. JavaScript, on the other hand, is a scripting language that defines variables and functions, which result in a certain output. Xandr must wrap JS creatives in HTML so that the browser is told that it is looking at a language.

> [!NOTE]
> Often, JavaScript tags come pre-wrapped in HTML. Please note, if the JS is surrounded by HTML markup tags, then the creative is HTML!

**When should I use the 'Serve in iFrame' option?**

An iFrame is an inline frame that contains another document. If you are trafficking expandables or rich media ads, you should not have this feature selected as this will cause the ad to not expand beyond the ad slot. This is because the JavaScript cannot reference anything outside of the contained iFrame document.

Serve in iFrame checked:

- Xandr will always serve the tag in an iFrame, even if we have to make one.

Serve in iFrame not checked:

- Xandr won’t serve the tag into an iFrame on purpose. It is important to note that there is no way Xandr can guarantee the tag won’t land in an iFrame due to the nature of the RTB marketplace.

**How can I fix my expandable tag if it is not expanding?**

Sometimes Expandable creatives do not pass audit because, by default, they may not render correctly in our preview environments. However, a simple adjustment can allow the expandable to serve well in our preview, in our audit UI, and most importantly, in a live environment. Let's take the following tag as an example:

**Example tag**

``` 
<script src="https://bs.serving-sys.com/BurstingPipe/adServer.bs?ncu=$$${CLICK_URL_ENC}$$&cn=rsb&c=28&pli=XXXXXXX&PluID=0&w=728&h=90&ord=${CACHEBUSTER}">
</script>
<noscript>
<a href="${CLICK_URL}https://bs.serving-sys.com/BurstingPipe/adServer.bs?cn=brd&FlightID=XXXXXXX&Page=&PluID=0&Pos=7636" target="_blank">
<img src="media/adServer.bs?cn=bsr&FlightID=XXXXXXX&Page=&PluID=0&Pos=7636" border=0 width=728 height=90>
</a>
</noscript>
```

The change needs to be made in the first part of the tag, specifically in the "src" URL. A "&ifrm=-1" value needs to be added to the URL, as shown below:

**Modified tag (\*\*please scroll over\*\*)**

``` 
<script src="https://bs.serving-sys.com/BurstingPipe/adServer.bs?ncu=$$${CLICK_URL_ENC}$$&cn=rsb&c=28&pli=XXXXXXX&PluID=0&w=728&h=90&ord=${CACHEBUSTER}&ifrm=-1">
</script>
<noscript>
<a href="${CLICK_URL}https://bs.serving-sys.com/BurstingPipe/adServer.bs?cn=brd&FlightID=XXXXXXX&Page=&PluID=0&Pos=7636" target="_blank">
<img src="media/adServer.bs?cn=bsr&FlightID=XXXXXXX&Page=&PluID=0&Pos=7636" border=0 width=728 height=90>
</a>
</noscript>
```

This "ifrm=-1" value allows for auto-detection of the environment the tag is loaded in, allowing it to expand properly out of a friendly iFrame or stand-alone, and display a backup default in an unfriendly iFrame.

**What is the maximum allowed file size?**

There is no maximum file size, but some sellers may block creatives that have an initial load size that is greater than 40kb.

**Why is my creative skewed/truncated?**

Most likely the the wrong tag size was selected.

## SSL

**What is SSL inventory?**

Many sites, such as Facebook and large email providers, require users to log in securely (https) so as to encrypt communication to and from the site and protect against eavesdropping and tampering. When a user visits a page that is behind a secure connection, a non-secure ad, or non-secure pixels served with the ad, would cause the browser to show a warning prompt. If the user decides not to load the non-secure content, this would result in wasted impressions and reporting discrepancies.

**Does serving on SSL cost me anything extra?**

Xandr does not charge an additional platform audit fee to audit the creative for SSL compliance.

**What must be secure for SSL ad serving?**

The creative itself must be secure. All files loaded by the creative, and all files loaded by those files, etc., must be secure as well. This applies to pixels and piggyback pixels.

**Will I serve the SSL "Secure" version of my creative on non-SSL "Standard" impressions?**

No. Xandr will serve your “Standard” creative tag on standard placements and your “Secure” tag on secure placements.

**If my creative fails SSL audit, is non-SSL serving affected?**

No. If your creative fails SSL audit but passes platform audit, it will serve on non-SSL inventory.

**How can I submit a creative for SSL audit?**

On the creative object within the API, set the field, allow_ssl_audit, to true.

**Will I receive any notifications if SSL audit fails?**

Yes. An email notification is sent out for each creative that fails SSL audit. The notification will include the following information:

- Creative ID
- Information about the violation(s), for example, the non-secure URLs that were called
- Link to the audit report, which shows the whole call chain
- Instructions for contacting support

Please note, you will not receive notifications for successful audits.

**If my creative fails SSL audit, how can I get it to pass?**

Correct the violations listed in the notification email and resubmit the creative for SSL audit.

**If my creative fails SSL audit, is non-SSL serving affected?**

No. If your creative fails SSL audit but passes platform audit, it will serve on non-SSL inventory.

**Do piggyback pixels need to be secure?**

Yes. All files loaded by the creative must be secure. This applies to pixels and piggyback pixels.

**Sherlock testing**

Sherlock, our automated creative quality testing engine, will scan your creatives to ensure that all content associated with a creative is secure.

- If any creatives are rejected, it was because they were detected loading at least one insecure URL, or the SSL certificate was invalid.
- Automated emails will be sent that will tell you what domain served the insecure content. You can setup the email addresses to receive these notifications on your member. Please see the [Member Service](member-service.md) and look for the audit_notify_email and sherlock_notify_email fields.
- Work with the developer to ensure only secure URLs are returned, then opt the creative back into SSL audit.

For more information about our automated testing engine, see [Sherlock - Creative Quality Control](sherlock-creative-quality-control.md).

## Creative templates

Each creative needs a template that meets the following criteria.

- Creative Template Media Type/Subtype meets Creative Media Type/Subtype
- Creative Template Format equals Creative Format

Creative template are required because our placement tags are expecting HTML or JavaScript content. To be compatible, our creatives need to be HTML or JavaScript as well. Templates are actually wrapper around the creative which enable a creative to render properly. Without a creative template users would need to upload HTML and JavaScript tags for every ad you would want to run on Xandr, which is not efficient.

Creative templates are never creative specific and are general in scope. Each template can be assigned using API the [creative template service](creative-template-service.md). Creative specific elements of the template are denoted using macros. The Impression Bus will populate these macros automatically given the creative information.

Important fields in the template :

- content_html – The creative wrapper in HTML

  ``` 
  <a href="${CLICK_URL}" target="_blank">
  <img width="${CREATIVE_WIDTH}" height="${CREATIVE_HEIGHT}" style="border-style: none" src="${MEDIA_URL}" /> </a>
  ```

- content_js – The creative wrapper in JavaScript.

  ``` 
  document.write('<a href="${CLICK_URL}" target="_blank"><img width="${CREATIVE_WIDTH}" height="${CREATIVE_HEIGHT}" style="border-style: none" src="${MEDIA_URL}"/></a>');
  ```

**HTML image template**:

- The \<a\> (anchor) HTML tag makes its contents “clickable”
- “href” (hyperlink reference): Contains the URL loaded on click
- “target”: specifies where the URL should load
  - “\_self”: Load in same window/tab \<= This is the value used if nothing is specified
  - “\_blank”: Load in new window/tab \<= This is needed in all of ad serving

> [!TIP]
> If Your Creative Contains An \<a\> HTML Tag Without A target=“\_blank” Parameter, And It Clicks Through In The Same Window, you need to add the \_blank element.

- On “tt” (iFrame) call:
  - If the creative template has a “content_html”, then that will be returned.
  - If Creative Template does not have a “content_html”, but does have a “content_js”, then return the “content_js” wrapped in \<script\> (making it HTML).
  - The API validates against having neither, but if this were allowed, the creative would blank.
- On “ttj” (JavaScript) call:
  - If the creative template has a “content_js”, then that will be returned.
  - If creative template does not have a “content_js”, then blank, even if the template has a “content_html.4”

> [!TIP]
> If you don’t define content_js In your template, then the creative will not display properly to users with no javascript. The creative will still preview correctly in the audit UI.

## Standard creative macros:

``` 
${CLICK_URL} – Xandr click tracker + landing page URL
${CREATIVE_WIDTH}
${CREATIVE_HEIGHT}
${MEDIA_URL} – The URL of the image. Speaking about creative templates in general, the URL of the output type is specified when a creative is set up. 
```

## Audit related

**Can I pass macro values into the creative audit that are used when the creative is previewed?**

No. The creative must serve without any dynamic parameters being passed in when the creative is previewed as part of the creative audit.

Example: Say the creative url is `"https://cnd.server.com/123.js?camp={CAMP}"`, and the value passed for CAMP in the bid response would result in a creative being served for brand ABC. Then calling the URL `"https://cnd.server.com/123.js?camp={CAMP}"`, without any macro replacement, must also result in a creative being returned for brand ABC.

**Can I serve one creative in the audit and another when I win an auction?**

No. The creative that is uploaded into Xandr must show an advertisement for the underlying brand when it is previewed, as well as when it is delivered in RTB. This means that the creative must be able to serve without any macros being populated.

**Do I have to pay separately for the MSFT audit and the Xandr audit?**

No. When the auditors review a creative, they will audit it for both Microsoft and Xandr. This is all included in the same audit fee. The fields audit_status and msft_audit_status will be populated accordingly.

**How can I set a creative to be active?**

This can be done using the [creative-service](creative-service.md) by setting the active field to "active." This can also be done through the [bidder UI](https://bidder.xandr.com/login) in the Creatives tab, by selecting the creative, then checking the "active" box in the full edit screen.

**How do I make sure my creatives aren't audited?**

Using the [creative-service](creative-service.md), set the audit status to "no-audit".

**How do I put my creative in the audit queue?**

Using the [Creative Service](creative-service.md), set the allow_audit field to true. This can also be done through the [bidder UI](https://bidder.xandr.com/) in the Creatives tab, by selecting the creative, then checking "resubmit" in the "Audit Status" field. The creative must also be active and the member the creative is registered under must also be active.

**If I disagree with the results of an audit, what should I do?**

Use our [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com) form to contact the Ad Quality team.

**What does it mean when is_expired=1?**

This means that the creative both has not served and has not been modified in over 45 days, and it is effectively inactive. The creative must be set to active and re-audited if it has expired.

**How can I get the audit status of my creatives?**

There are three methods that are available:

1. Using the [Creative Service](creative-service.md):
    - You can make daily calls using the min_last_modified parameter, in the format of YYYY-MM-DD to see all creatives that have had their status changed. You should also use the num_elements and start_element parameter.
    - For example, if you run `https://api.adnxs.com/creative/12345?min_last_modified=2018-05-15&num_elements=100&start_element=0`, the results will include 100 creatives modified since May 15, 2018. The "count" parameter will include the total number of creatives, but because the API will only return up to 100 objects at a time, you can page through the results by using the start_element parameter.
1. Use the [audit notify request](audit-notify-request.md):
    - When creatives are audited, audit notify requests are sent to the handler if this has been set up in the [Bidder Service](bidder-service.md).
    - In order to set use an audit notify request handler, you must have a single endpoint that can receive and process these requests as they are sent.
1. Use an excel export
    - If you would like a weekly report of your creative status sent by email, please speak with your Xandr technical and account team.
1. Use the [bidder UI](https://bidder.xandr.com/login) to view the creatives.

**What is returned when I call the creative service?**

The entire creative object is return when you call the creative service, so you will need to parse out the relevant audit status parameters.

**My creative's landing page isn't opening in a new tab or window. Why was it marked unauditable?**

We require that clicking on an ad opens a new tab or window so that users aren't forced to navigate away from the publisher's page. If your creative is a third party tag, you can add a simple macro to ensure that this happens:

TARGET="\_blank"

**Can I rotate brands in my creative or show more than one brand at the same time?**

No. Each creative may show only one brand. This may not change during the lifetime that the creative is used on the platform unless the creative stops serving, set put into the queue for re-audit, and is audited for the new brand. Creatives also may not show more than one brand. If the creative is clearly for an online retailer and shows a product now made by that retailer, but is a sample product you can buy at that retailer, and if the creative clicks through to that retailer's website, then this is fine.

**Do I have to set the brand of my creative?**

No. This is done by our auditing team.

**What exactly is a brand?**

BMW is a brand. BMW 5-series is not considered a separate brand.

**Why are my creatives not serving?**

There are a number of reasons a creative may not be serving:

- If a creative has active=0, it will not serve.
- If a creative has is_expired=1, it both has not served and has not been modified in over 45 days and will need to be re-audited.
- If a creative has failed the Microsoft audit, it will not serve on Microsoft inventory.
- If a creative is "pending" for the Xandr audit, it will only serve on the portion of the inventory that allows unaudited creatives.

Sellers in Xandr can also choose to ban by the brand, category, language, technical attribute or buyer, so an otherwise-valid creative may be banned by a seller.

## Uploading creatives

**Can I upload multiple creatives in one API call?**

No. But you can programmatically upload multiple creatives in consecutive POSTs to the API. Please note that you only make 60 writes in a rolling 60-second window.

**How can I upload creatives?**

You can upload creatives through the [Creative Service](creative-service.md) API.

**How do I upload a Flash creative?**

In the [Creative Service](creative-service.md) API, you can either provide a link in the "media_url" field, or provide a tag using the "content" field. If you host a javascript file that delivers the flash, you would specify the URL of your javascript in the media_url, and the format would be url-js. The media_url may be, for example:

`https://ad.sample_site.com/ad_server/ads.js?my_ad_id=12345&price_paid=${PRICE_PAID}&custom_macro=${custom_macro}`

In the alternative, you may want Xandr to deliver the javascript or iframe that delivers the flash. For example, you may use format "iframe-html" (or raw-js, if you enter the raw javascript - not if you use an html tag that calls javascript) and set the content to be:

``` 
<SCRIPT 
 TYPE="text/javascript" 
 SRC="https://ad.sample_site.com/ad_server/ads.js?my_ad_id=12345&price_paid=${PRICE_PAID}&custom_macro=${custom_macro}">
</SCRIPT>
```

**What is the creative code?**

The code is your internal ID for a creative. When a creative is made in Xandr, it is given an ID in our system (e.g. 12345). If you internally refer to this creative as 'abc', you would specify the code of the creative as 'abc'. When you bid, you then submit either 12345 as the ID or 'abc' as the code.

**What is the correct format to use?**

The format can be one of: 'url-html','url-js', 'flash','image','raw-js', 'iframe-html', or 'text'. The values, url-html and url-js, are to be used when you're using the media_url parameter in the creative. This means that the creative is defined purely by a reference to a website that has html or javascript content. The format raw-js should be used when the creative is purely javascript. This mean that the creative is only javascript. If the creative is in the following format:

`<script language="JavaScript" type="text/javascript">javascript here....</script>`

then the creative is iframe-html and not raw-js.

If there's a javascript tag, you can still bid with iframe creatives (and vice-versa) - Xandr will format the content of your creative appropriately. For example, we will use document.write(...) around your iframe creative for javascript tags.

## content vs. original_content

- original_content: The tag exactly as it is uploaded to the api.
- content: The tag exactly as the ${CONTENT} macro of the creative template is expecting it.
- In the case of an HTML tag, if the **serve in iFrame** option is checked, both content and original content will be exactly the same.
- HTML Tag with the serve in iFrame option unchecked, content and original content will be different.

**How can I fix the following error message "There was an error with the request: Vast Wrapper tracker URL is not valid"?**

Ensure that there is no invalid or unsupported character present in the VAST url as well as in the 3rd party segments attached to the creative. For example,

- This is the set of valid VAST characters: `ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789-._~:/?#[]@!$&'()*+,;=.`
- This is a set of common invalid characters: `|, <, >, ^, {,}.`

Additionally:

- If there are curly brackets `{ }` present in the VAST url or segment, then they **must** have `$` in front of the bracket.
- Ensure that there is no double `%` present in the VAST url or segment.
