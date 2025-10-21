---
title : Microsoft Monetize - Click Track Test
description: Explore Microsoft Advertising's pre-upload checks, highlighting the click track test's role in ensuring platform integrity.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Click track test

## Overview

Prior to uploading to the Microsoft Advertising platform, a series of automated checks are performed on a creative to ensure that it is compliant and optimal to serve on an inventory. Click track test is one of those checks. The goal of the click track test is to ensure that a creative's tag is properly set up to measure clicks for reporting purposes. For a creative to pass the click track test, Microsoft Advertising's click-tracker URL must load once when the creative is clicked.

Note that the purpose of the click track test is not to test whether the creative clicks through properly. That can be done by simply clicking on the creative and observing its behavior. The primary intention of the test is to verify whether Microsoft Advertising has the ability to track clicks on the creative. There is a possibility that for a certain creative though the click through happens properly, it may not load in Microsoft Advertising's click tracker.

If the click tracker loads properly, you'll see a status saying "Click tracking is working" whereas if the click tracker doesn't load properly, you'll see a "Click tracking is not working" status. Receiving a status of "Click tracking is not working" doesn't always mean that we won't be able to track clicks on the creative. In cases where creatives have rotating brands, it is possible that the click tracker will only load for certain creatives that have been loaded. For example, external systems may only click track when a default creative is not served in the slot, or when a creative is served in certain countries. Being said that, at times, when the system encounters click tracking test issues, you may need to troubleshoot them.

### Workflow

- When Microsoft Advertising's Click Tracker URL is loaded, a request to Microsoft Advertising's server is made to register the click.
- After the click is logged, the user will be redirected to the final landing page.

An example of a Microsoft Advertising Click Tracker URL is `https://nym1-ib.adnxs.com/click2?`.

For a creative to pass the click track test, the above URL must fire in the network calls when the creative is clicked. If the URL fires, it implies that the creative has been set up properly to measure the clicks.

> [!NOTE]
>
> - If the Microsoft Advertising click tracker URL does not load when you click the creative, then it will not measure the clicks. The click track test determines if your creative is setup properly to load the Microsoft Advertising's click-tracker URL and measure the clicks.
> - You can manually test click tracking if there are occurrences of strange creative behavior or there are UI issues that result in unreliable outcome of the click tracking test within the UI. For more information, see [Test Click Tracking Manually](test-click-tracking-manually.md).

### Common click tracking test failures

| Failures | Reasons and Recommended Solutions |
|--|--|
| Failed to click on creative that appears blank | The creative may be configured with blocklists on Microsoft Advertising-domains that control where the creative is allowed to render. Ensure that your server-configurations have no blocks on the following domains:<br><br> - [adnxs.net](https://about.ads.microsoft.com/en-us/solutions/xandr/xandr-premium-programmatic-advertising)<br> - [adnxs.com](http://audit.adnxs.net/)<br> - [creative-preview-an.com](https://about.ads.microsoft.com/en-us/solutions/xandr/xandr-premium-programmatic-advertising)<br> - [audit.adnxs.net](http://audit.adnxs.net/) |
| Failed to click on a creative | - The creative might not be clickable. The recommandation would be to verify the creative's behavior and update it if it is needed.<br> - The creative only has a specific area that is clickable: Our **Click Track Test** tool might not be able to detect this. If this is the case, please manually test the creative to see if Microsoft Advertising click tracker fires while a click is initiated. All the instructions are on this [page](test-click-tracking-manually.md).<br> - Microsoft Advertising performs click-track testing from a Firefox Browser. So, if your creative fails to click on Firefox environments, it will fail the test. Ensure that your creative renders and is clickable on all supported browsers such as Chrome, Firefox, Safari, and Edge. |
| Creative loads landing page in the same browser window | Ensure that Microsoft Advertising's click macro is properly embedded within your creative's tag and that the creative clicks through to a new tab and/or window. |
| Microsoft Advertising's Click tracker URL did not fire | Ensure that the Microsoft Advertising click macro is properly embedded in your creative's tag. This macro is a placeholder value for Microsoft Advertising's click-tracker URL, which is used to measure clicks on Microsoft Advertising's Server. |
| Click Tracker URL fired before click | Please verify if the Microsoft Advertising click macro is placed before the **source** URL either of the creative iFrame or Javascript tag, rather than adding it into the query string.<br><br>```<script src="${CLICK_URL}http://ad.mysampleadserver.com/myAdOnAppNexus/Ad-MediumRectangle-300x250"type="text/javascript"></script>```<br><br>This means that every time the creative loads, it will load Microsoft Advertising click URL along with the creative entire source code, causing clicks to be tracked 100% of the time. Please, ensure that the Microsoft Advertising click Macro is placed in the query string. |

### Common click tracking test issues

| Issues | Recommended Solutions |
|--|--|
| The creative isn't rendering during the click track test because geographic fencing or third-party protection has been enabled. | Remove any geographic fencing or third-party protection from the creative. |
| The creative didn't respond to clicking because it may be expecting the user to click on a particular **Call to Action** button. | The user simply chose not to click the **Call to Action** button, so there's nothing you can do to resolve this issue. |
| The creative is interfering with the browser's navigation, so its landing page is loading in the same browser window. | Contact your creative developer to resolve this issue. |
| The creative didn't load the click tracker URL, so it hasn't been fired. | Ensure that the click tracker URL or click tracking macro is inserted and that it's inserted properly. For more information, see [Click Tracking](click-tracking.md). |
| The click tracker is getting lost between ad servers when testing click tracking on third-party video creatives although the click tracking URL macro has been inserted properly. The most common reason for this is that our click tracker may get lost between ad servers. This may occur in cases where the video creative on the third-party side is another third-party tag. | The setup on the third-party side needs to pull in our click tracker and insert it into the tag, which requires the use of macros on the tag. One of the following configurations can be used:<br>**Tag with script/noscript sections and click tracking URL example**: Many third-party tags will include both script and noscript HTML tags. If a user has JavaScript enabled in their browser, only the script sections will load. If a user does not have JavaScript enabled, then the noscript sections will be able to load. It is imperative that the click tracking URL macro be included in the script section since the vast majority of users will have JavaScript enabled. However, including the click macro in both sections will allow for proper click tracking on all users. For example:<br><br> ```<script src="http://ad.mysampleadserver.com/myAdOn/Ad-MediumRectangle-300x250?click=${CLICK_URL_ENC}"type="text/javascript"> </script> <noscript> <a href="${CLICK_URL_ENC}http://www.cnn.com"><img src="http://upload.wikimedia.org/wikipedia/commons/2/24/Ad-MediumRectangle-300x250.jpg" width="300" height="250"></a> </noscript>```<br><br>**Note**: If the click tracking test runs on a browser with JavaScript enabled and the click tracking URL macro is included only in the noscript section, then the creative will fail the test.<br>**Tag with embedded iFrames example**: An iFrame loads a web page within itself. It will load the URL provided in the "src" (source) parameter. An iFrame will only load its inner contents (in this case the script and noscript sections) if the user's browser does not support iFrames. For example:<br><br>```<iframe src="http://ad.mysampleadserver.com/myAdOn/Ad-MediumRectangle-300x250?format=iFrame" width="300" height="250"> <script src="http://ad.mysampleadserver.com/myAdOn/Ad-MediumRectangle-300x250"type="text/javascript"> </script> <noscript> <a href="http://www.cnn.com"><img src="http://upload.wikimedia.org/wikipedia/commons/2/24/Ad-MediumRectangle-300x250.jpg" width="300" height="250"></a> </noscript></iframe>```<br><br>Essentially, this is what takes place after the creative is loaded:<br> - If the browser does support iFrames, it will load the source URL in the iFrame.<br> - If the browser does not support iFrames, it will:<br>&nbsp;&nbsp;&nbsp; - load only the script sections if the browser does support JavaScript.<br>&nbsp;&nbsp;&nbsp; - load only the noscript sections if the browser does not support JavaScript.<br>For proper click tracking on all users, it's necessary to include the click tracking URL macro in all three sections: iFrame source, script section, and noscript section. |
| The creative passes the click tracking test but tracks clicks on all impressions or is flagged for auto-clicking. This scenario will occur when the click tracking macro has been prepended to the src URL of either the JavaScript or iFrame tag. As a result, it will not accurately track clicks although it has passed the click tracking test.<br>An invalid example of this configuration using JavaScript would be:<br><br>```<script src="${CLICK_URL_ENC}http://ad.mysampleadserver.com/myAdOn/Ad-MediumRectangle-300x250"type="text/javascript"></script>```<br><br>Another invalid example of this configuration using an iFrame would be:<br><br>```<IFRAME SRC="${CLICK_URL_ENC}></IFRAME>```<br><br>In both of these examples, the src URL represents where the creative is loaded from. If the click tracker macro is inserted in that URL (as shown above), it will load each time when the creative loads. This results in the number of clicks equaling the number of impressions, which results in 100% CTR. | Instead of prepending the click macro, ensure it is passed in using the query string. For examples of how to do this, contact your creative developer.Instead of prepending the click macro, ensure it is passed in using the query string. For examples of how to do this, contact your creative developer. |

## Related topics

- [Click Tracking](click-tracking.md)
- [Test Click Tracking Manually](test-click-tracking-manually.md)
