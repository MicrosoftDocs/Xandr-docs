---
title: Set Up AST Tags for Native Ad Types
description: Set up seller tag (AST) for native ad types. AST tags are defined and loaded in the page header and are activated by showing the tags in the page body.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: seller-tag
ms.author: shsrinivasan
---

# Set up seller tags for native ad types

Microsoft Advertising's Seller Tag (AST) is an asynchronous Java script tag that runs in the header of the page. AST tags are defined and loaded in the page header and are activated by "showing" the tags in the page body. For native ads, there are different methods available to help render the ad on the page.

> [!TIP]
> For selected use cases, AST can also be defined, loaded, and shown in the page body.

## How it works

A native ad unit can be added to a web page in various locations decided by the publisher, such as:

- At the start of an article
- In between paragraphs of text in an article
- At the end of an article

In each of the scenarios above (and others), the native ad unit is generally included as a hidden `<div>` element in the page body. The `<div>` element in the page body refers to the native ad unit using a Target Identifier, which corresponds to a definition of that Target Identifier in the page header. When the container comes into view, the native ad unit is displayed on the page to show the content.

While the above is the general approach taken by most ad units managed through AST, there is some additional flexibility with native ad units that may interest publishers. Native ad units rely on the presence individual native assets to create the ad experience, some examples of these assets are Title text, Body text, a main Image, Sponsored By text, etc. Given the native assets are like pieces of a collage, publishers have the choice to assemble how these assets are arranged to display the content in the ideal manner for their page.

The manner to arrange the assets can be handled in different ways. This Set Up page will provide some context on two general ways the arrangement can be handled, with some examples of how the set-up of the AST code may differ accordingly.

The main difference between the two ways noted below is where the arrangement (or the native creative template) will exist, in the Microsoft Monetize system (using the Native Assembly feature) or on the web page itself (self-managed by site-developers).

## Native assembly example

The [Native Assembly](../monetize/native-assembly.md) feature helps publishers to choose (and customize) a variety of native creative templates preset within the Microsoft Monetize system. Through the feature, you're able to create specific Native Assembly renderer objects (that define the overall layout and cohesion of the native assets) and assign them to specific placements, so that when the placement returns a native bid - it will include this Native Assembly renderer to help ensure the native ad appears in the desired format on the page.

In the case of AST, the set up needed to use Native Assembly is not so different from the standard setup for other ad types. The native object within the `defineTag` should be included, with the particular asset requirements specified in the object config. The `tagId` (i.e. `placementId`) used in the `defineTag` should have a Native Assembly renderer object assigned to it (in Microsoft Monetize) to ensure the renderer is included in any returning native bids.

The `showTag` piece in the body of the page should be included in the desired area where the ad should display.

```
// in page header
apntag.defineTag({
tagId: 3456,
targetId: 'native_slot',
// example native config
native: {
body: {required: true},
title: {required: true},
image: {required: true, sizes: [{ width: 300, height: 250 }]},
sponsoredBy: {required: false},
},
});

...

// later in page body
<div id="native_slot">
<script type="text/javascript">
apntag.anq.push(function() {
apntag.showTag('native_slot');
});
</script>
</div>
```

## Self-managed native example

As opposed to the Native Assembly approach, this set up is primarily managed on the page itself by the publisher's site developers or maintainers. This approach affords the ability for the publisher to define the creative template code in a way that directly meshes with the site's structure and behind-the-scene coding. In addition, it is a ready option always available for use if the Native Assembly feature is not currently enabled on your Microsoft Monetize seat.

The primary mechanism this approach uses are the AST event handlers, primarily the event for `adAvailable`. This event represents the point in the auction process where the bid has returned to AST and is 'available' for use. The additional code seen after the `defineTag` in the example is one way to register a function for the AST `adAvailable` event; additional details how to use AST events can be found [here](./on-event.md).

The code presented in the example below is just a basic approach to reference the native assets from the returning native bid and to render the combined HTML into a predesignated spot on the page. There are many ways this code can be written by the site developers as to fit the needs of the creative and the context of the page.

> [!IMPORTANT]
> For this approach, there are two AST functions [fireImpressionTrackers](./fire-impression-trackers.md) and [attachClickTrackers](./attach-click-trackers.md) that are included within rendering function. As their names suggest, both functions play important roles to load the impression and click tracking URLs for the creative. If they are not included, the creatives will not track, and it will impact the performance.

If you are using this type of set up for the first time, allow some time to thoroughly test the code in different environments, browsers, etc. to ensure all pieces are working as expected.

```
// in page header
apntag.defineTag({
tagId: 13232354,
targetId: 'native_slot',
// example native config
native: {
body: {required: true},
title: {required: true},
image: {
required: true,
aspect_ratios: [{
min_width: 300,
min_height: 250,
ratio_width: 2,
ratio_height: 3
}]
},
sponsoredBy: {required: false},
},
});

apntag.onEvent('adAvailable', function(tag) {
const native = tag.native;

// render the native assets with this template
document.getElementById('native_slot').innerHTML = `
<div class="sponsored-post">
<div class="thumbnail" style="background-image: url(${native.image && native.image.url});"></div>
<div class="content">
<h1><a href="${native.clickUrl}" target="_blank">${native.title}</a></h1>
<p>${native.body}</p>
<div class="attribution">${native.sponsoredBy}</div>
</div>
</div>
`;

apntag.fireImpressionTrackers(tag);
apntag.attachClickTrackers(tag, 'native_slot');
});

...

// in page body
<div id="native_slot">
<script type="text/javascript">
apntag.anq.push(function() {
apntag.showTag('native_slot');
});
</script>
</div>
```
