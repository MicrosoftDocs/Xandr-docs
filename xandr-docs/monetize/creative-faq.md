---
title: Microsoft Monetize - Creative FAQ
description: In this article, find answers to frequently asked questions regarding creatives.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Creative FAQ

## Why is my creative skewed/truncated?

Most likely the the wrong tag size was selected.

## My creative isn't showing up. What's wrong?

A quick note: most creative issues can be mitigated by uploading content directly onto our server and then inputting click/tracking URLs in the designated field. Our server is approved across all supply partners, so if your creative passes our auditing, it may be more likely to be permitted on restrictive supply sources like Google Ad Manager than if it is hosted by a third-party ad server.

There are a few things you can look for before sending a ticket into Microsoft Advertising Support. First, does the trafficking code (html, javascript, etc.) match the creative? A javascript tag that is interpreted as pure html (e.g. `<script></script>`) should be trafficked as html. Raw javascript (e.g. `var x = "my tag"`) should be trafficked as such. The tag code determines how that impression bus will deliver the ad (i.e. if it will be wrapped within a doc.write or not), so it is often the problem behind blank creatives.

If your tag code is correct, load a creative preview using our server URL:

`https://creative-preview-an.com/cached/creative/insert creative id here`

After refreshing a few times, if the page is blank, you should inspect the creative's tag content. Check to see if there are any glaring format errors such as spacing, etc. Please note that we do not support javascript comments at this time. If the tag has comments, remove the comment wrappers:

`<!//----\ ----//>`

When you edit and save the creative, wait 10-15 seconds before refreshing several times to check if the changes worked.

If none of the above steps work, you can test to see if the problem is on our end: copy your tag into a text file, save it as an html, and open the html file with your browser. If it doesn't load, then the issue lies with the tag or 3rd party content. If the creative loads, the issue is specific to Microsoft Monetize. If removing comment wrappers or altering incorrect formatting doesn't remedy the problem and the creative is loading in your browser, feel free to submit a support ticket.

## I'm not seeing any clicks, so why does my creative appear to be serving?

We now have a built-in click-tracking test in the creative Full Edit pane.

**Flash creatives**: Make sure that the **clickTAG** macro is capitalized correctly as it is case sensitive. However, note that some flash creatives use other capitalization variations (e.g. clickTag). You can decompile the flash file using a free software utility (e.g. Flare) to check.

Please see [Click Tracking](click-tracking.md) for further details on click tracking. If you are still having problems, please contact Microsoft Advertising Support.

## Can I run creatives in different languages?

Please see [International Creatives](../bidders/international-creatives.md).

## What happens if multiple creatives are attached to the same line item?

If the creatives are different sizes, then the appropriate size will be chosen for the publisher's tag. If there are several creatives of the same size, one creative will be chosen at random for each impression, assuming they are all eligible based on frequency and recency parameters.

## Why won't my creative click through properly in Full Edit mode?

Currently, the creative preview in Full Edit is not intended to be fully functional. You can click through outside of Full Edit mode, or use the following URL to serve your creative:

`https://creative-preview-an.com/cached/creative/insert creative id here`

## Gambling creatives

Please see our [Part of Service Policies](../policies-regulations/index.yml) for information on what kinds of gambling ads are allowed to serve and under what conditions.
