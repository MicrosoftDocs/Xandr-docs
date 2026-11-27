---
title: Microsoft Monetize - Troubleshooting VAST Creatives
description: In this article, find information about troubleshooting display issues with VAST creatives.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Troubleshooting VAST creatives

Currently, our support for VAST creatives is limited to third-party URL type creatives. This means that the actual content of your VAST creative is hosted elsewhere and relies fully on this third party to properly deliver the content. If you find that your creative is not displaying and/or is failing our audit, there are steps that can be taken to troubleshoot these issues.

## Confirm that your URL is returning valid VAST XML content

When placing the URL in a browser, it should return VAST compliant XML as per IAB Standards.

Check the HTTP status and response body for the affected request. An empty body and a VAST document with no `<Ad>` element have different meanings. An ad server can return HTTP 200 with a valid, empty VAST document when it has no eligible ad. Confirm expected fill and targeting with the hosting service. If the response contains a `<Wrapper>`, follow its `<VASTAdTagURI>` and check the next response.

If otherwise malformed, the URL may no longer be returning the correct content, or a change was made on the third party end. If this has changed since the creation of the creative, you can re-run the [VAST Check](vast-check.md) to clarify any issues. Contact your third party hosting service with this information.

## Test your URL in a VAST validator

For an XML error, validate a sanitized copy of the captured response with a tool such as [VASTlint](https://vastlint.org/validate/) and include the affected element in your report to the ad server. To check playback, open a QA tag URL in the [JWX Ad Tester](https://developer-tools.jwplayer.com/ad-tester) and select the ad client used by your integration.

:::image type="content" source="media/third-party-vast-validator.png" alt-text="Screenshot of JW Player Ad Tester that shows the ad tag field.":::

If the content is returned successfully, you'll see the ad impression fire in the events log, and your ad will play in the validator's player.

:::image type="content" source="media/successful-vast-validation.png" alt-text="Screenshot of JW Player Ad Tester that shows the ad events log for a successful validation.":::

If no ad is returned or any errors are seen, reach out to your third party hosting service to confirm that the URL is indeed live, and whether there is any logic, or targeting on their end that may prevent the content from being returned in certain geos, on certain IP addresses, or certain domains.

:::image type="content" source="media/vast-validation-error.png" alt-text="Screenshot of JW Player Ad Tester that shows the ad events log for a failed validation.":::

> [!NOTE]
> The test player can play its content video even when no ad plays. Check its ad events log to see whether an ad started or the player reported an error.

## Correct URL but creative is not displaying/displaying incorrectly in Monetize

If an ad is returned by the URL in a validator, but the creative is not displaying in Monetize or is failing audit for improper display, ensure that your third-party hosting service is not blocking the **adnxs.com** or **adnxs.net** domains, the **US/NY** geo, or any of the range of [Microsoft Advertising IP Addresses](../digital-platform-api/ip-range-list-service.md).

## What does the error message "Heavy ad intervention" mean?

This error message signifies that the resource use for a creative exceeds one or more threshold(s) set by [browser intervention](https://iabtechlab.com/blog/chrome-will-block-heavy-ads-soon-get-vast-video-ads-ready/) introduced by Chrome. Since September 2020, Chrome has introduced a new [browser intervention](https://iabtechlab.com/blog/chrome-will-block-heavy-ads-soon-get-vast-video-ads-ready/) that monitors ad iframes and may redirect them to an error page (Heavy ad intervention) if resource use exceeds specified criteria. Video advertisements, in particular, may be vulnerable to this intervention, which impacts iframes that load more than 4 MB of data.

If a creative satisfies any of the following criteria, it is considered heavy:

- The main thread is used for more than 60 seconds in total.
- In any 30 second window, the main thread is used for more than 15 seconds.
- More than 4 MB of network bandwidth is consumed.

It is recommended that the creative is compliant with the technical specifications detailed above.

## Related topic

[VAST Check](vast-check.md)
