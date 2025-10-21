---
title: Microsoft Curate - Use Events and Parameters
description: Learn how Standard events allow you to capture the interactions that matter most to an advertiser. You can enhance events by adding additional information in the form of parameters.  
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-curate
ms.author: shsrinivasan
---


#  Microsoft Curate - Use events and parameters

After you have configured your universal pixel, you can add value by configuring it to identify events, such as adding an item to a shopping cart. Standard events allow you to capture the interactions that matter most to an advertiser. You can enhance events by adding additional information in the form of parameters.

> [!NOTE]
> You can also create custom events and parameters. For more information, see [Create Custom Events and Parameters](create-custom-events-and-parameters.md).

For example, using the standard event `AddtoCart`, you can track when users add an item to a shopping cart. Using parameters, you can configure the `AddToCart` standard event to also gather the product ID, product name, and total cart/purchase value. This information can provide you with better insights for building audience segments and more granular tracking of user interactions.

Standard events are implemented as snippets of code placed on relevant webpages that indicate when users perform typical actions. For example, if you place the code snippet on the landing page where a user arrives after they select **Add to Cart**, the pixel is triggered by the script code, and the event can be tracked.

The following table shows the benefits of adding events and parameters to the basic pixel implementation.

| Universal Pixel with Events | Universal Pixel Without Events |
|--|--|
| Page views and other typical events such as cart adds and purchases | Only page views and URLs |
| Advanced rule logic combining:<br> - URLs <br> - standard and custom events <br> - standard and custom parameters | Only URL-based rules and page view events |

## Related topics

- [Create Custom Events and Parameters](create-custom-events-and-parameters.md)
- [Standard Events and Parameters](standard-events-and-parameters.md)
