---
title: Microsoft Curate - Set up Consent Mode in Universal Pixel
description: Explore this article to learn how to set up consent mode in Universal Pixel, which provides control over the reading and writing of both first-party and third-party cookies based on customer consent.
ms.date: 08/05/2024
---

# Microsoft Curate - Set up consent mode in Universal Pixel

Consent mode in Universal Pixel allows you to configure cookie access based on customer consent. This feature enhances privacy by controlling the reading and writing of both first-party and third-party cookies.

This document outlines how you can set up consent mode in Universal Pixel. However, it's your responsibility to comply with local legal requirements and industry practices.

## How it works?

Use the `ad_storage` property in Universal Pixel to configure consent mode. The possible values for `ad_storage` are listed as follows:

| Property | Value | Description |
|:--|:--|:--|
| `ad_storage` | `granted` | Third-party cookies might be read and written for Universal Pixel.<br><br>**Note:** Consent mode is not enabled by default. It must be enabled and set to "`granted`". |
| `ad_storage` | `denied` | Third-party cookies are not read and written. |

> [!NOTE]
> For noscript pixie calls, ensure that you update the URLs with the correct consent parameters.

## Examples

This section provides an example for setting up and updating the consent settings for every webpage.

### Set up consent settings

To set the default consent settings for every webpage on your website, use the following code:

```
<script 

!function(e,i){if(!e.pixie){var n=e.pixie=function(e,i,a){n.actionQueue.push({action:e,actionValue:i,params:a})};n.actionQueue=[];var a=i.createElement("script");a.async=!0,a.src="//acdn.adnxs.com/dmp/up/pixie.js";var t=i.getElementsByTagName("head")[0];t.insertBefore(a,t.firstChild)}}(window,document); 

pixie(‘consent’, ‘default’, { ‘ad_storage’:  ‘denied’, ‘wait_for_update’: 1000}); 

pixie('init', ‘REPLACE_WITH_UP_PIXEL_ID'); 

pixie('event', 'PageView'); 

</script>

<noscript><img width="1" height="1" style="display:none;" src="https://ib.adnxs.com/pixie?pi=REPLACE_WITH_UP_PIXEL_ID&e=PageView&script=0&consent=REPLACE_WITH_A_1_OR_0" />
</noscript>
```

You can set `ad_storage` to `granted` or `denied` by default. In the preceding example, consent is set to `denied` by default. The initialization of the Universal Pixel and event tracking is delayed by 1000 milliseconds to wait for a consent update. You can modify your existing Universal Pixel tag or you can replace it. If you're copying the preceding example, ensure that you replace `REPLACE_WITH_UP_PIXEL_ID` and `REPLACE_WITH_A_1_OR_0` with your specific values before deploying the code.

> [!NOTE]
>
> Due to our current rollout changes, `ad_storage` defaults to "`denied`" for the European Economic Area (EEA), Switzerland, and the UK.

### Update consent settings

After a customer provides or denies consent, update the consent settings on every webpage with the following code:

```
pixie ('consent', 'update', { 

'ad_storage': 'granted' 

});
```

Run this script on subsequent webpages after the initial Universal Pixel script (see [Set up consent settings](#set-up-consent-settings)) as long as the consent is valid.

As a best practice, it's recommended that you place the consent script in the `<head>` tag of your webpages. This approach ensures that consent mode is set by default and updated whenever a customer changes their consent settings.
