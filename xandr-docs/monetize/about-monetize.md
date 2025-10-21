---
title: About Microsoft Monetize
description: In this article, find information on Microsoft Monetize and its features along with technical details.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# About Microsoft Monetize

Microsoft Monetize is a web-based application for your programmatic advertising. Whether you’re buying or selling ad space, or both, Monetize provides all the tools that you need to manage your accounts.

## Buyers

Monetize can manage both traditional media buys and real-time bidding through a single, unified interface. Instead of operating an ad server and a buying platform, Monetize can perform both functions, eliminating double-trafficking, discrepancies, and another set of fees.

Monetize offers:

- Seamless integration with major ad networks, exchanges, aggregators, and SSPs.
- Site list with volume and price estimates.
- Direct and managed media buys and auction-based buys through one simple interface.
- Built-in fraud protections and inventory quality protections.
- No need for contracts with each publisher or exchange.

A number of other key features help Microsoft Monetize optimize your ad buying revenue and increase buying efficiency.

## Sellers

Monetize has a number of features that allow you to maintain business and technical relationships with your managed publishers. With Monetize, you can:

- Set up publishers and traffic campaigns on managed inventory.
- Resell inventory on the Microsoft Advertising platform for better monetization.
- Apply optimization strategies to your direct campaigns since optimizing direct campaigns is as important as optimizing on third-party inventory.
- Manage individual publishers' ad quality requirements, ensuring that you meet expectations about the quality and content of ads served on their sites.

## Ad server

As an ad server user, you have access to your end-to-end setup of advertiser and publisher information. You can set up publishers and available inventory, as well as advertisers and their selling specifications. With an ad server, you can set up and manage your buy-side systems and your sell-side systems, as well as manage forecasting, priorities, and many other types of functionality between the two.

## Technical details - process flow

- **Ad Calls Initiation**: Ad calls are received from various inventory supply partners, including exchanges, SSPs, ad networks, and valued publishers. These calls can be either client-side (directly from Microsoft Advertising tag on the page) or server-side (initially handled by partners then forwarded to Microsoft Advertising).
- **Data Overlay**: Upon receiving the ad call, Microsoft Advertising overlays segment data from its server-side cookie store. This data is accumulated either through segment pixels or by clients sending data files. Third-party data providers may also contribute additional data.
- **Bid Request to Bidders**: Microsoft Advertising contacts all bidders on its platform, providing them with the ad call data, including user data and inventory information. Bidders have a limited time frame (milliseconds) to respond with a bid and the creative they intend to serve.
- **Monetize Bidder Processing**: Microsoft Advertising's proprietary bidder, Monetize, processes the bid request. Monetize offers various features such as campaigns, targeting options, bidding algorithms, and multi-currency support. It can be accessed either through a user interface (UI) or an Application Programming Interface (API).
- **Bid Evaluation by Impression Bus**: The impression bus evaluates the bids received, considering factors such as bid amount and any preferences set by the publisher regarding ad serving. Based on these criteria, the impression bus determines the winning bid.
- **Ad Serving**: If the ad call originated client-side, Microsoft Advertising serves the ad directly to the user. If the ad call was server-side, Microsoft Advertising communicates the winning bid and the location of the creative to the partner responsible for ultimately serving the ad.

## Get started

[Get in touch](https://about.ads.microsoft.com/en-us/solutions/xandr/contact-xandr) with a Microsoft Advertising representative today so you can get started! Already have an account? Log in to [Monetize](https://monetize.xandr.com/login).
