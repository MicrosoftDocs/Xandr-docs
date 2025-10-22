---
title: Introduction to Ad Serving
description: This page gives an overview on Ad Serving along with a list of different parties that get involved in online advertising.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: industry-reference
ms.author: shsrinivasan
---


# Introduction to Ad serving

In traditional offline advertising, a company creates an ad campaign and then purchases advertising slots using different kinds of media, for example, on television, in magazines and newspapers, and on roadside billboards. With online advertising, the same thing happens, but the logistics behind media planning, or selecting where and when you will run your ads, are different.

That's because the Internet is a much more fractured, individualized medium. There are far more websites run by far more organizations than there are TV networks and shows, and the interaction between consumer and media event has been narrowed down to a single person viewing a single webpage or using a single mobile app. Think about that versus a newspaper being printed once a day and read by thousands or a TV ad aired to a large population. Another large difference is the ability to tag consumers via their browser's [cookie file](online-advertising-and-ad-tech-glossary.md#cookie) or by their [mobile device ID](online-advertising-and-ad-tech-glossary.md#mobile-device-id), which allows advertisers and other parties to segment consumers and collect data on ad effectiveness on an individual level.

## Different parties involved in online advertising

Many different parties interact in the online advertising ecosystem:

- **Publishers** (sellers) provide inventory, or the space where ads are displayed. This may be a website or a mobile app.  For example, [www.nytimes.com](https://www.nytimes.com/), [www.cnn.com](https://edition.cnn.com/) and [www.imdb.com](https://www.imdb.com./) are all publishers who sell ad space.
- **Advertisers or marketers** (buyers) purchase inventory for the display of advertisements.  For example, Microsoft, Amazon, and Target are all advertisers.
- **Ad networks** serve as brokers between groups of publishers and groups of advertisers. Networks traditionally aggregate publishers and advertisers and also handle [remnant](online-advertising-and-ad-tech-glossary.md#remnant-inventory) inventory, but they can have a wide variety of business models and clients.
- **Users** are the target customers for advertisements.
- **Data providers** provide information useful for targeting.  This can be contextual information about the web site or web page where the ad is displayed (for example, you wouldn't want to display a vacation ad next to a newspaper article about a plane crash), behavioral data about users, [viewability](introduction-to-viewability.md) data about advertisements, or other kinds of data.
- **Data management platforms (DMPs)** are centralized systems for gathering first-party data, integrating with third-party data, and applying this data to one's advertising strategy. A DMP may offer the following features: estimating the likely reach for a user segment, measuring the lift from using data, acting as a financial clearing house between data buyers and sellers, and assisting publishers in monetizing data on their users. DMPs most commonly work with [user data](online-advertising-and-ad-tech-glossary.md#user-data) but may also work with [contextual data](online-advertising-and-ad-tech-glossary.md#contextual-data), or other types of data. For example, Sizmek and Rocket Fuel are large DMPs.
- **Demand side platforms (DSPs)** enable advertising clients to buy digital media on many different selling networks, exchanges, and platforms through a single interface. For example, Xandr, ONE by AOL,  Rocket Fuel, and Turn can act as DSPs.  
  **Supply side platforms (SSPs)** enable publishers to access demand from many different networks, exchanges, and platforms through a single interface.  For example, Xandr, Liverail, OpenX, and Pubmatic can act as SSPs.
- **Rich media vendors** create, serve and manage rich media advertising.  Rich media refers generally to advertisements with audio, video, or other interactive elements.

Publishers, advertisers, and networks interact through unified ad trafficking systems called **ad exchanges**.  An ad exchange allows advertisers and publishers to use the same technological platform, services, and methods, and "speak the same language" in order to exchange data, set prices, and ultimately serve an ad.  Major ad exchanges include DoubleClick, OpenX, Facebook's FBX, and Xandr.

## Ad serving overview

Ad serving is the process of determining which advertisement goes in which ad slot on a publisher's webpage or mobile app and then delivering the advertisement.  The computer or group of computers that's responsible for this is called an ad server. Major publishers, networks, and advertisers sometimes have their own ad servers.  Most large ad servers also:

- Choose the ad that will most benefit the advertiser or the publisher, and that meets each party's criteria.
- Record how many ads were served and on what pages or screens.
- Record performance data, for example, whether the ad was clicked on, when the viewer stopped playing a video ad, or if the ad can be tied to a purchase or some other action.
- Funnel performance data back into the matching process.
- Capture and make available user data, which is information about a consumer (user) including browser habits and demographic data.

An ad server can be a publisher's ad server, where the publisher decides who gets the impression, or an advertiser's ad server, where the advertiser decides which creative goes in the slot they have been assigned. Or it can be an intermediary ad server that attempts to maximize the benefit to both sides. Some ad servers are small, in-house decisioning systems, and others are major ad servers used by many clients such as Xandr or Google's various ad serving products.

## Working of Ad serving

:::image type="content" source="media/working-of-ad-serving.png" alt-text="Screenshot of the working of Ad Serving.":::

In order to understand ad serving, it's important to understand the following concepts:

- **Placement** - The slot on the publisher's page or location in an app where the advertisement will appear.
- **Creative** - The actual advertisement.
- **Impression (imp)** - A creative served to a single user at a single point in time.
- **Ad Tag** - A snippet of code that requests or passes along data. The data may be the size of the placement, the publisher's URL, or some other kind of information, or a creative or other content.  For more information, see [Ad Tags](ad-tags.md).

In offline print advertising, publishers sell ad space.  In online advertising, publishers typically sell impressions – a combination of ad space and the number of times an ad displays. Payment terms are sometimes based on impressions, but they can also be based on **conversions**, or actions taken by end users, such as purchasing an item or signing up for a mailing list.

Determining which ad to serve depends on the advertiser and publisher requirements for logistics, targeting, advertising preferences, and pre-existing relationships.  An ad server may need to:

- Deliver guaranteed buys, where a publisher has promised a certain number of impressions to an advertiser over a particular time period.
- Conduct auctions in real time as the page is loading to choose the highest eligible bidder.
- Predict expected performance (how often users click on the ad or respond to the ad) based on past performance metrics. This is generally part of optimization algorithms.

When targeting ads or evaluating bids, the ad server must take into account many considerations such as:

- Advertiser parameters, for example, site lists, time of day, geography, or browser type.
- User data, which is information about a consumer's past web behaviors or demographic collected by the advertiser, a data company, or the publisher.
- Frequency and recency, which means limiting how often someone sees a particular ad.
- Publisher parameters, for example, constraints about which types of advertisers or ads a publisher will allow on its site.

## Further reading

The above explanation is a conceptual version of ad serving, which can be a very complicated world with a lot of hops between a page loading and an ad being served. If you are new to ad serving and ad tags and all the hops that go into a single impression event, please see [Ad Tags](ad-tags.md) and the other pages below.

- [Ad Tags](ad-tags.md)
- [Creatives](creatives.md)
