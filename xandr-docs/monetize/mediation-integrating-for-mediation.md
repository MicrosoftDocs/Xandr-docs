---
title: Integrating for Mediation
description: This page describes the types of integrations supported, how to set them up, and how they work.
ms.date: 10/28/2023
---


# Integrating for mediation

> [!NOTE]
> Mediation is available only to Microsoft Monetize Ad Server customers.

In order to sell your inventory to buyers that are not directly connected to our exchange, you will need to set up your technical integration. This page describes:

- The types of mediation integrations we support
- How to set them up
- How they work

## Web passbacks

A significant portion of demand is not available via RTB, and is instead traded using tags. In order to access this demand, you need to be able to "pass back" the impression to your original ad call if the top bidding ad network defaults.

With web passbacks, the ad call is initiated from the browser. This makes your impressions more valuable since passbacks give mediated network buyers access to their own cookies. Networks can then match cookies to their own user IDs for frequency capping, targeting, and attribution purposes.

This page describes web passbacks and contains instructions for setting up browser-based mediation using web passbacks.

**Setting up**

For each network you'd like to mediate, do the following:

1. Log in to the mediated network's UI.
1. In the mediated network's UI, for each placement (or ad spot) you'd like to run through the mediation tool, set this JavaScript snippet as your default creative: `mediation.noad();`

    > [!NOTE]
    > In some cases, you may need to change the format slightly depending on the requirements of the mediation network's UI. For example:
    > - HTML: You may need to wrap the JS in `<script>` tags to upload it as HTML.
    > - URL: You may need to provide a URL. Use `http://cdn.adnxs.com/mediation/noad.md` or the secure version: `https://cdn.adnxs.com/mediation/noad.md`.

1. Log in to the UI.
1. In the UI, [Mediation Networks](mediation-networks.md) to represent the mediated networks in our system.
1. In the UI, [Mediation Bids](mediation-bids.md) to represent the demand tied to the placement or ad spot you just created in that network (which has a passback if needed).
1. After you've created all of your bids, activate your bids to start serving ads.

## How it works

> [!TIP]
> See the diagram below for more details.

Assuming you've set up your integration as described above, the ad call flow looks like this:

1. The tag on the page calls the Microsoft Advertising ad server.

1. The ad server runs an auction for the impression. Mediated bids are ranked in the auction according to bid price, alongside RTB bids.

1. The ad server responds differently depending on the auction outcome:

    1. If the winning bid is an RTB bid, it will serve the ad from the RTB buyer directly.
    1. If the winning bid is a mediated bid, it responds to the page's request with a list of mediated bids (a waterfall), as well as a JavaScript file `mediation.js`, which will manage the waterfall directly from the browser.

    (We will assume for the rest of this example that the winning bid is a mediated bid.)

1. `mediation.js`, running in the browser, calls the mediated networks in the order specified by the waterfall. For each network:
    1. If the network returns an ad, it is served, and `mediation.js` notifies the ad server so we can report on the impression.
    1. If the network does not return an ad, it calls the function `mediation.noad()`, which triggers `mediation.js` to call the next network in the waterfall.

   :::image type="content" source="media/mediation-client-side-web.png" alt-text="Screenshot of mediation client.":::

## SDK mediation

SDK mediation allows mobile app developers and publishers to access demand from mediation networks. Microsoft Advertising has built [Microsoft Advertising Mobile SDKs](../mobile-sdk/xandr-mobile-sdks.md) that allow app developers to monetize their inventory.

SDK mediation requires coordination between ad ops teams and mobile engineers:

- Ad ops teams will need to make sure the right information is being pulled from, and entered into, mediation network UIs.
- Mobile engineers will need to make sure that mediation adaptors are properly configured to allow different networks' SDKs installed on the device to interoperate correctly.

**Setting up**

Follow these steps to set up SDK mediation integration:

1. Integrate one of our [Microsoft Advertising Mobile SDKs](../mobile-sdk/xandr-mobile-sdks.md) with your app. Our SDKs come bundled with mediation adaptors that allow us to mediate SDKs from popular networks such as AdMob. For a complete list of networks that we support with SDK adaptors, see [Mediation Networks](mediation-networks.md).
1. If the mobile ad network you need to mediate already has a supported mediation adaptor, the mediation should occur automatically once you're set up. Follow the instructions in these pages to get started:
    1. [mediation-networks](mediation-networks.md)
    1. [Mediation Bids](mediation-bids.md)
1. If the mobile ad network you need to mediate does not have a supported mediation adaptor, you will have to have your engineers write a custom adaptor that allows our SDK to communicate with the ad network's SDK. Then you can set up that network and start creating bids. Follow the instructions in these pages to write a custom adaptor and set up your network and bids:
    1. [Android Custom Adaptors](../mobile-sdk/android-custom-adaptors.md)
    1. [iOS Custom Adaptors](../mobile-sdk/ios-custom-adaptors.md)
    1. [Mediation Networks](mediation-networks.md) (specifically, a Custom Mobile Network)
    1. [Mediation Bids](mediation-bids.md)
1. Activate your bids to start selling to those networks.

## Learn how SDK mediation integration works

> [!TIP]
> See the diagram below for more details.

Assuming you've set up your integration as described, the ad call flow looks like this:

1. The Microsoft Advertising SDK calls our ad server.
1. The ad server runs an auction for the impression. Mediated bids are ranked in the auction according to bid price, alongside RTB bids.
1. The ad server responds differently depending on the auction outcome:
    1. If there is a winning RTB bid, it returns the ad directly.
    1. Otherwise, it returns a list of mediated networks (a waterfall) which Microsoft Advertising's SDK will use to communicate with other ad  networks' SDKs installed on the device.
1. The Microsoft Advertising SDK will call the mediated networks' SDKs running on the same device in the order specified by the waterfall response from the ad server.
1. Each of the mediated SDKs listed in the waterfall gets the chance to respond with an ad. The mediated SDK that ends up serving notifies the Microsoft Advertising SDK that an ad was served.

:::image type="content" source="media/mediation-sdk-integration.png" alt-text="Diagram of sdk Mediation.":::

## Server side mediation

Server Side Mediation is easy to get started with. It requires only that you set up networks and bids in our system. These networks and bids are used to represent your external demand sources in our system, and to gather reporting data from external systems. Server-side mediation is available for a number of popular networks, including Google AdMob, MoPub, and Amazon.

> [!TIP]
> For a complete list of supported networks, see [Mediation FAQs](mediation-faqs.md).

**Setting up**

Follow these steps to set up a server side mediation integration:

1. [Mediation Networks](mediation-networks.md) to represent the mediation network in our system.
1. [Mediation Bids](mediation-bids.md) to represent the demand coming from that network.
1. Activate your bids to start selling to those ad networks.

## Learn how server side mediation integration works

Assuming you've set up your integration as described, the ad call flow looks like this:

1. The tag on page calls Microsoft Advertising's ad server.
1. The ad server runs an auction for the impression. Mediated bids are ranked in the auction according to bid price, alongside RTB bids.
1. The ad server behaves differently depending on the auction outcome:
    - If a mediated bid wins, it tries to load an ad from the mediated network. If the mediated network has no ad to show, the impression goes to the next highest bid (the next network in the waterfall, or an RTB buyer).
    - If an RTB bid wins, it will serve the ad from the RTB buyer directly.

:::image type="content" source="media/mediation-server-side-integration.png" alt-text="Screenshot of Server Side Mediation.":::

## Related topics

- [Mediation Networks](mediation-networks.md)
- [Mediation Bids](mediation-bids.md)
- [Mediation Bid Setup Best Practices](mediation-bid-setup-best-practices.md)
- [Mediation FAQs](mediation-faqs.md)