---
title: Microsoft Invest - Troubleshoot VAST Creative Display Issues
description: In this article, learn essential best practices and effective techniques to troubleshoot and resolve VAST creative display issues.
ms.date: 10/28/2023
---

# Microsoft Invest - Troubleshoot VAST creative display issues

Currently, our support for VAST creatives is limited to third-party URL type creatives. This means that the actual content of your VAST creative is hosted elsewhere and relies fully on this third party to properly deliver the content. If you find that your creative is not displaying and/or is failing our audit, there are steps that can be taken to troubleshoot these issues.

## Confirm that your URL is returning valid VAST XML content

When placing the URL in a browser, it should return VAST compliant XML as per [IAB Standards](https://www.iab.net/media/file/VAST-2_0-FINAL.pdf).

If the response is empty, the URL may no longer be live. Contact your third-party hosting service to confirm.

If otherwise malformed, the URL may no longer be returning the correct content, or a change was made on the third party end. If this has changed since the creation of the creative, you can re-run the [VAST Check](vast-check.md) to clarify any issues. Contact your third party hosting service with this information.

## Test your URL in a VAST validator

Place the URL in a third party VAST validator (such as [JWPlayer](https://demo.jwplayer.com/ad-tester/)). Confirm with your third party adserver whether content will be returned in both Flash and HTML5 player types, and test accordingly.

:::image type="content" source="media/third-party-vast-validator.png" alt-text="Screenshot of a third-party VAST validator, J W player.":::

If the content is returned successfully, you'll see the ad impression fire in the events log, and your ad will play in the validator's player.

:::image type="content" source="media/successful-vast-validation.png" alt-text="Screenshot of the validator's player with the ad event log.":::

If no ad is returned or any errors are seen, reach out to your third-party hosting service to confirm that the URL is indeed live, and whether there is any logic, or targeting on their end that may prevent the content from being returned in certain geos, on certain IP
addresses, or certain domains.

:::image type="content" source="media/vast-validation-error.png" alt-text="Screenshot of the validator's player with the ad event error log.":::

> [!NOTE]
> Since these are in-stream video creatives, they must be delivered before, between or after another video, therefore each VAST validator will have its own video content that will play regardless of whether an ad has served. Each validator will have an ad events log that will confirm whether your ad has been delivered, or if there were any errors.

## Correct URL but creative is not displaying/displaying incorrectly in Microsoft Invest

If an ad is returned by the URL in a validator, but the creative is not displaying in Microsoft Invest or is failing audit for improper display, ensure that your third-party hosting service is not blocking the **adnxs.com** or **adnxs.net** domains, the **US/NY** geo, or any of the range of Microsoft Advertising IP Addresses.

## Explain "Heavy ad intervention" error message

This error message signifies that the resource use for a creative exceeds one or more threshold(s) set by [browser intervention](https://iabtechlab.com/blog/chrome-will-block-heavy-ads-soon-get-vast-video-ads-ready/) introduced by Chrome. Since September 2020, Chrome has introduced a new [browser intervention](https://iabtechlab.com/blog/chrome-will-block-heavy-ads-soon-get-vast-video-ads-ready/) that monitors ad iframes and may redirect them to an error page (Heavy ad intervention) if resource use exceeds specified criteria. Video advertisements, in particular, may be vulnerable to this intervention, which impacts iframes that load more than 4 MB of data.

If a creative satisfies any of the following criteria, it is considered heavy:

- The main thread is used for more than 60 seconds in total.
- In any 30 second window, the main thread is used for more than 15 seconds.
- More than 4 MB of network bandwidth is consumed.

It is recommended that the creative is compliant with the technical specifications detailed above.

## Related topic

[VAST Check](vast-check.md)
