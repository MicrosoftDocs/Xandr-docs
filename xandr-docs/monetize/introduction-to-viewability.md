---
title: Microsoft Monetize - Introduction to Viewability
description: In this article, find an overview of viewability in digital media, why viewability is important, how it works, and current Microsoft Advertising support for viewability.
ms.date: 10/28/2023
---

# Microsoft Monetize - Introduction to viewability

This page provides an overview of viewability in digital media as well as information about why viewability is important, how it works, and current Microsoft Advertising support for viewability.

## What is viewability and why is it important

Marketers buy media to reach "eyeballs" in an effort to create awareness for their brand and influence consumers. If a marketer's advertisement goes unseen, there is no opportunity for the message to have an impact. An ad being seen by a human is therefore a fundamental requirement for all advertising. Digital media presents a unique and exciting opportunity to directly measure whether an ad was in-view of a consumer.

Today, viewability is commonly used to assess the quality and value of digital media, and it is often included as a mandatory goal in advertisers' campaigns.

### Buy-side impact

Viewability is useful to the buy side because it allows buyers to select websites that provide good quality exposure. Branding campaigns can focus on viewability as a key performance indicator. Maximizing ad viewability is a goal for the media buyer.

Additionally, viewability can be used to boost the performance of direct response ad campaigns. When evaluated in the light of direct response, viewability can be utilized as a metric to select quality sites where ads are in-view increasing the chance for potential conversions.

Viewability could also allow buyers to use new attribution models for post-view conversions.

### Sell-side impact

Because more and more buyers value media based on viewability metrics, publishers have incentive to be aware of how viewable their sites are. Understanding and managing viewability for inventory presents the opportunity to create high viewability packages and improve overall inventory quality.

## How does viewability measurement work for display ads

Viewability measurement is the technological answer to a longer-lasting business need. In order for a creative to be viewable, all the following conditions must be met:

- The browser window must be in the focus.
- More than 50% of the area of the creative (30% of the area for large size creatives) must be in the viewable part of the screen. This takes into account the size of the screen, the size and position of the creative on the page, and any scrolling action by the user.
- For large Ads, the creative size (including video creatives) is 242,500 pixels minimum.

The following are examples of creatives that are not viewable:

:::image type="content" source="media/not-viewable.png" alt-text="Diagram that shows examples of creatives that are not viewable.":::

Viewability depends on a myriad of parameters: screen size, creative loading duration, and so on.

Viewability measurement is achieved through a technology that is embedded with the creative, executes in the browser of the user, and measures the actual behavior of each individual user who is served the creative.

Viewability measurement is, by its nature, an exhaustive measurement of every single impression.

### Technical summary

Viewability measurement is achieved by JavaScript embedded within the creative. This script is called for each individual ad-impression. It launches automatically as the page loads, and immediately starts measuring if and when the creative is viewable.

:::image type="content" source="media/viewability-tech.png" alt-text="Diagram that shows how viewability is measured.":::

The primary method that the script will use to determine whether an ad is viewable is "page geometry", which takes into account the size of the screen and the size and position of the creative on the page among other factors such as scrolling and window focus. However, if only a part of the required information is available, other techniques must be used so that the measurement is consistent across all platforms.

### Technical challenges

Viewability measurement must work in all environments and provide consistent results. IFrames are the most challenging of technical environments. When the creative and the measurement script are served within an IFrame, regular geometric methods cannot be applied. Alternative methods, such as browser optimization, must be developed. Depending on the technologies used by ad-viewability vendors, the potential success rate can be very limited.

:::image type="content" source="media/iframe-measurement.png" alt-text="Diagram that shows the challenges of viewability measurement for creatives within IFrames.":::

:::image type="content" source="media/viewability-tech-final.png" alt-text="Diagram that shows the success rate of viewability measurement across devices.":::

In some instances, viewability cannot be measured with success. In these cases, no assumption can be made on the viewability of the impression.

### Using viewability data

Several aggregations are feasible from impression-level viewability data. The most common metrics include:

- Number of viewable impressions
- Viewability rate
- Measurement success rate

It is possible to use these metrics to gain insight into the comparative quality of various media. A buyer can compare the viewability rate of one ad campaign to:

- Industry benchmarks
- Internal benchmarks
- Other advertisers in a portfolio
- Other campaigns for the same advertiser

It is also possible for a media buyer to:

- Generate reports that provide viewability data broken down by domains or line items, allowing for comparison of different inventory sources.
- Choose to exclude (blocklist), or include (allowlist), a selection of domains or line items, enabling control over the viewability of inventory purchased.

### Measurement technology

Viewability measurement on Microsoft Advertising is tested continuously across all major browser versions, including web, mobile app, and mobile web context.

:::image type="content" source="media/viewability-measurement.png" alt-text="Diagram that shows the various contexts in which viewability measurement is tested.":::
