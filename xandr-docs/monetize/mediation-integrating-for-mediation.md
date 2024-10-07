---
title: Integrating for Mediation
description: This page describes the types of integrations supported, how to set them up, and how they work.
ms.date: 10/28/2023
---

# Integrating for mediation

> [!NOTE]
> Mediation is available only to Microsoft Monetize Ad Server customers.

## Microsoft Monetize Ad Server mediation

Microsoft Monetize Ad Server mediation allows demand from sources not integrated into the Monetize exchange or [Prebid Server Premium](prebid-server-premium.md) to compete for publisher inventory. Both known partners, such as Google, as well as custom networks are supported.

This page describes the end-to-end process of setting up mediation connections in partner platforms and how those connections function. For more information on Monetize-specific steps, see the links below:

- [Mediation Networks](mediation-networks.md)
- [Mediation Bids](mediation-bids.md)

> [!NOTE]
>
> - Mediated Networks are not connected directly to the Monetize exchange and do not submit bids into the auction in real time. Publishers must regularly review reports from each network and adjust Bid CPM values to ensure they represent a realistic price. Otherwise, an inaccurate mediated bid could win auctions over higher bids from other sources.
> - The examples below are simplified for learning purposes and do not account for all the complex interactions and edge cases involved in real auctions.
> - If a mediated Network does not return an ad, even the second-highest bid might not serve for a variety of reasons. Example: The brand of a real-time bidding (RTB) buyer’s creative is banned in the publisher ad quality settings. The impression would then go to the third-highest bidder.

### Web passbacks

A **significant portion** of demand is not available via real-time bidding (RTB) and is instead accessed using tags. When the mediation Network does not return an ad, passbacks default to the original ad call to retrieve more demand.

Web passbacks initiate the ad call from the browser, allowing cookies to be matched to Network user IDs. This increases the value of the impression through targeting, frequency capping, and attribution.

To set up each web Network:

1. In the mediated Network's UI, for each placement (or ad slot) to be called for mediation, set this JavaScript snippet as the default creative: `mediation.noad()`.
1. In the Monetize UI, follow guidance to set up [Mediation Networks](mediation-networks.md) to represent each partner.
1. In the Monetize UI, follow guidance to set up [Mediation Bids](mediation-bids.md) to represent the network demand for specific inventory.
1. Once Bids have been created and enabled, requests will be sent to the network partners for demand.

> [!NOTE]
> The JavaScript format might vary slightly depending on the requirements of the mediation network's UI.
> For example:
>
> - **HTML**: The JavaScript might need to be wrapped in `<script>` tags to upload as HTML
> - **URL**: If a URL is required, use `http://cdn.adnxs.com/mediation/noad.md` or the secure version: h`ttps://cdn.adnxs.com/mediation/noad.md`

### Web request and response process

When following the standard setup described above, the web request and response process begins:

1. The tag on the page calls the Microsoft Monetize Ad Server.
1. Monetize Ad Server runs an auction across its demand sources. Mediated bids are ranked according to the Bid CPM entered by the publisher, alongside RTB bids.
1. Monetize Ad Server responds differently depending on the auction outcome:
   1. If the winning bid is an RTB bid, Monetize serves the ad from the RTB buyer directly.
   1. If the winning bid is a mediated bid, Monetize responds to the page's request with a list of mediated Bids (a waterfall), as well as a JavaScript file `mediation.js`, which manages the waterfall directly from the browser.
   1. **For the rest of this example, assume the winning bid is a mediated bid**.
1. `mediation.js`, running in the browser, calls the mediated Networks in the order specified by the waterfall. For each network:
    a. If the Network returns an ad, the ad is served, and `mediation.js` notifies Monetize Ad Server to report the impression.
    b. If the Network does not return an ad, the Network calls the function mediation.noad(), which causes `mediation.js` to call the next network in the waterfall.

## Web browser support

Monetize mediation scripts currently support the browsers below.

When the mediation script encounters an unsupported browser, it bypasses all mediated Bids and calls back to Monetize for alternative demand. The Monetize response could be RTB demand, a public service announcement (PSA), default creative, or blank, based on default action settings for the seller and placement.

#### Desktop

- Chrome
- Firefox
- Internet Explorer
- Edge
- Opera
- Safari

#### Mobile

- Safari
- Android
- Chrome

### App SDK mediation

Software development kit (SDK) mediation allows mobile app developers and publishers to access demand from mediation Networks. Microsoft Advertising offers specific Mobile SDKs for this purpose.

SDK mediation requires coordination between ad ops teams and mobile engineers:

- Ad ops teams must ensure the right information is being pulled from, and entered into, mediation network UIs and the Monetize UI.
- Mobile engineers need to ensure that mediation adaptors are properly configured to allow different Networks' SDKs on the device to operate correctly with each other.

To set up each app SDK Network:

1. Integrate one of [Microsoft Advertising’s Mobile SDKs](../mobile-sdk/xandr-mobile-sdks.md) with the app. Microsoft’s SDKs come bundled with mediation adaptors that allow us to mediate SDKs from popular networks.
1. If the desired mobile ad network **already has a supported mediation adaptor**, the mediation should occur automatically once setup is complete. Follow the instructions in these pages to get started:
    a. In the Monetize UI, follow guidance to set up [Mediation Networks](mediation-networks.md) to represent each partner.
    b. In the Monetize UI, follow guidance to set up [Mediation Bids](mediation-bids.md) to represent the Network’s demand for specific inventory.
1. If the desired mobile ad network **does not have a supported mediation adaptor**, publisher engineers must write a custom adaptor that allows the Microsoft SDK to communicate with the ad network's SDK. Once the adaptor is available, the custom mobile Network can be created along with bids.
    1. Create [Android Custom Adaptors](../mobile-sdk/android-custom-adaptors.md)
    1. Create [iOS Custom Adaptor](../mobile-sdk/ios-custom-adaptors.md)
    1. In the Monetize UI, follow guidance to set up [Mediation Networks](mediation-networks.md) to represent each partner, specifically as a Custom Mobile Network.
    1. In the Monetize UI, follow guidance to set up [Mediation Bids](mediation-bids.md) to represent the Network’s demand for specific inventory.
1. Once Bids have been created and enabled, requests will be sent to network partners for demand.

### App request and response process

When following the standard setup described above, the app request and response process begins:

1. The Microsoft Advertising SDK calls Monetize Ad Server.
1. Monetize Ad Server runs an auction across its demand sources. Mediated Bids are ranked in the auction according to the Bid CPM entered by the publisher, alongside RTB bids.
1. Monetize Ad Server responds differently depending on the auction outcome:
    a. If the winning bid is an RTB bid, Monetize serves the ad from the RTB buyer directly
    b. Otherwise, Monetize returns a list of mediated Networks (a waterfall) which Microsoft Advertising's SDK will use to communicate with other ad networks SDKs installed on the device
1. The Microsoft Advertising SDK calls the mediated Networks' SDKs running on the same device in the order specified by the waterfall response from Monetize Ad Server.
1. Each of the mediated SDKs listed in the waterfall has an opportunity to respond with an ad. The mediated SDK that serves, notifies the Microsoft Advertising SDK to report the impression.

### Server-side mediation

Server-side mediation only requires setup of Networks and Bids in Monetize to represent external demand sources.

To set up server-side mediation:

1. In the Monetize UI, follow guidance to set up Mediation Networks to represent each partner.
1. In the Monetize UI, follow guidance to set up Mediation Bids to represent the Network’s demand for specific inventory.
1. Once Bids have been created and enabled, requests will be sent to Network partners for demand.

### Server-side request and response process

When following the standard setup described above, the server-side request and response process begins:

1. The tag on the page calls the Microsoft Monetize Ad Server
1. Monetize Ad Server runs an auction across its demand sources. Mediated Bids are ranked in the auction according to the Bid CPM entered by the publisher, alongside RTB bids.
1. Monetize Ad Server responds differently depending on the auction outcome:
    a. If a mediated bid wins, it attempts to load an ad from the mediated Network. If the mediated Network does not return an ad, the impression goes to the next highest bid (the next network in the waterfall, or an RTB buyer).
    b. If an RTB bid wins, Monetize will serve the ad from the RTB buyer directly.

## Related topics

- [Selling Your Inventory through Mediation](mediation-selling-your-inventory-through-mediation.md)
- [Mediation Networks](mediation-networks.md)
- [Mediation Bids](mediation-bids.md)
- [Android Custom Adaptors](../mobile-sdk/android-custom-adaptors.md)
- [iOS Custom Adaptors](../mobile-sdk/ios-custom-adaptors.md)
  