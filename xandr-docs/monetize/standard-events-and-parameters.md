---
title: Microsoft Monetize - Standard Events and Parameters
description: Explore tracking Standard Events and Parameters with the universal pixel to streamline data collection. View standard events and query parameters. 
ms.date: 10/28/2023
---

# Microsoft Monetize - Standard events and parameters

The following table shows the standard events you can track using the universal pixel.

| Standard Event | Description |
|---|---|
| `PageView` | Track any type of page view (default event included in Universal Pixel script) |
| `LandingPage` | Track landing page views |
| `ItemView` | Track key page views (for example, product page or article) |
| `AddToCart` | Track when items are added to a shopping cart (for example, by visiting a landing page from an **Add to Cart** button) |
| `InitiateCheckout` | Track when users enter the checkout flow (for example, by visiting a landing page from a **Checkout** button) |
| `AddPaymentInfo` | Track when payment information is added in the checkout flow (e.g., landing page on billing info) |
| `Purchase` | Track purchases or checkout flow completions (for example, landing on a "Thank You" or confirmation page) |
| `Lead` | Track when users express interest in an offering (for example, submit a form, sign up for a trial, or register) |

The following table shows the standard query parameters you can pass as part of a standard or custom event. Parameters are passed in a JSON file on the event call, and have a 100-character maximum. Parameters can accept a single value or a comma-delimited array.

| Parameter | Query String Key in Image Tag Implementation | Variable Type | Supports Arrays/Lists | Description |
|---|---|---|---|---|
| `item_id` | `ii` | String | True | The item id associated with the event, for example, the product or catalog id |
| `item_name` | `in` | String | True | The name of the page or product |
| `item_type` | `itp` | String | True | The category of the page or product |
| `value` | `va` | Float | False | The numerical value associated with the event, for example, the price or cart value. |

## Related topic

 [Create Custom Events and Parameters](create-custom-events-and-parameters.md)
