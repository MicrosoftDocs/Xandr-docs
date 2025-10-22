---
title: Industry Reference - Introduction to Viewability
description: Learn about viewability and how it can be measured in Digital Media. This page covers different aspects of viewability and how it is useful to advertisers and publishers.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: industry-reference
ms.author: shsrinivasan
---

# Industry Reference - Introduction to viewability

## Importance of viewability

Marketers buy media to reach "eyeballs" in an effort to create awareness for their brand and influence consumers. If a marketer's advertisement goes unseen, there is no opportunity for the message to have an impact. An ad being seen by a human is therefore a fundamental requirement for all advertising. Digital media presents a unique and exciting opportunity to directly measure whether an ad was in-view of a consumer.

### Viewability in digital media

Presently, most online ads are paid for the moment they are served on a page, the moment the page starts loading. Depending on where the ad is displayed within the page, the creative may or may not be viewable immediately after the page loads. For instance, ads that are displayed “below the fold” are not viewable until the user scrolls down the page. Then, depending on the user's interest in the content of the page, the user may scroll down to be potentially exposed to the creative. In some instances, the location of the creative is so low on the page that very few users actually see the creative.

:::image type="content" source="media/viewability-in-digital-media.png" alt-text="Screenshot of viewability in Digital Media.":::

Viewability is difficult to estimate manually because it depends on user interaction across a given audience, as well as the layout of the page.

For example, premium content on a poorly formed page could have very low viewability rates. It's also possible for a website with a very good post-view conversion rate to have a low viewability rate. While this could mean that visitors to the website are very likely to convert, it is possible the ads served on the page were not responsible for driving the user to conversion.

### Viewability grows up

Over time, viewability has become an increasingly available and trusted metric for digital media.

- In 2007, Alenty was the first company to successfully measure ad-viewability. Alenty was later acquired by Xandr in 2014.
- In 2012, the Interactive Advertising Bureau (IAB) defined a "viewable impression."
- In 2014, the Media Rating Council (MRC) lifted its ban on trading viewable impressions.

:::image type="content" source="media/viewability-grows-up.png" alt-text="Screenshot of how viewability has grown.":::

> [!TIP]
> IAB Viewability definition: 50% of the pixels of a regular creative or 30% of the pixels of a large size creative (242,500 pixels or greater), are on an in-focus browser tab, on the viewable space of the browser page, for a minimum of one continuous second.

Today, viewability is commonly used to assess the quality and value of digital media, and it is often included as a mandatory goal in advertisers' campaigns.

### Advertiser impact

Viewability is useful to the buy-side because it allows buyers to select web sites that provide good quality exposure. Branding campaigns can focus on viewability as a key performance indicator. Maximizing ad-viewability is a goal for the media buyer.

Additionally, viewability can be used to boost the performance of direct response campaigns. When evaluated in the light of direct response, viewability can be utilized as a metric to select quality sites where ads are in-view increasing the chance for potential conversions.

Viewability could also allow buyers to use new attribution models for post-view conversions.

### Publisher impact

Because more and more buyers value media based on viewability metrics, publishers have incentive to be aware of how viewable their sites are. Understanding and managing viewability for inventory presents the opportunity to create high viewability packages and improve overall inventory quality.

## Measuring viewability

Viewability measurement is the technological answer to a longer-lasting business need. In order for a creative to be viewable, all the following conditions must be met:

- The browser window must be in the focus.
- More than 50% of the area of the creative (30% of the area for large size creatives) must be in the viewable part of the screen. This takes into account the size of the screen, the size and position of the creative on the page, and any scrolling action by the user.

The following are examples of creatives that are not viewable:

:::image type="content" source="media/not-viewable.png" alt-text="Screenshot of non viewable creatives.":::

Viewability depends on a myriad of parameters: screen size, creative loading duration, etc.  

This makes it nearly impossible to manually estimate if an ad on a page was viewable or not. Viewability measurement is achieved through a technology that is embedded with the creative, executes in the browser of the user, and measures the actual behavior of each individual user who is served the creative.

Viewability measurement is, by its nature, an exhaustive measurement of every single impression.

### Technical summary

Viewability measurement is achieved by javascript embedded within the creative. This script is called for each individual ad-impression. It launches automatically as the page loads and immediately starts measuring if and when the creative is viewable.

:::image type="content" source="media/technical-summary.png" alt-text="Screenshot of measuring viewability.":::

The primary method that the script will use to determine whether an ad is viewable is "page geometry", which takes into account the size of the screen and the size and position of the creative on the page among other factors such as scrolling and window focus. However, if only a part of the required information is available, other techniques must be used so that the measurement is consistent across all platforms.

### Technical challenges

Viewability measurement must work in all environments and provide consistent results. IFrames are the most challenging of technical environments. When the creative and the measurement script are served within an IFrame, regular geometric methods cannot be applied. Alternative methods, such as browser optimization, must be developed Depending on the technologies used by ad-viewability vendors, the potential success rate can be very limited.

:::image type="content" source="media/technical-challenges.png" alt-text="Screenshot of technical challenges in viewability.":::

### Using viewability data

Several aggregations are feasible from impression-level viewability data. The most common metrics include:

- Number of viewable impressions
- Viewability rate
- Measurement success rate

It is possible to use these metrics to gain insight into the comparative quality of various media. A buyer can compare the viewability rate of one campaign to:

- Industry benchmarks
- Internal benchmarks
- Other advertisers in a portfolio
- Other campaigns for the same advertiser

It is also possible for a media buyer to:

- Generate reports that provide viewability data by domains or by placements, allowing for comparison of different inventory sources.
- Choose to exclude (blocklist), or include (allowlist), a selection of domains or placements, enabling control over the viewability of inventory purchased.