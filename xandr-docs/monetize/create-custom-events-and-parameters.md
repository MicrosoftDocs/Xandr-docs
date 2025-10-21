---
title: Microsoft Monetize - Create Custom Events and Parameters
description: In this article, find step-by-step instructions on how to create and set up custom events and parameters.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Create custom events and parameters

If you click the pencil icon next to a pixel on the **Universal Pixels** page, you can create custom events and parameters for the universal pixel using the UI and include them in your generated pixel code.

Custom events are values set on the event key. Custom parameters are dynamically populated key-value pairs that contain additional metadata about an event, and are always associated with a standard or custom event.

To set up custom events and parameters:

1. On the **Universal Pixel** page, click the pencil icon next to the name of the pixel.
1. In the right pane, click the **Events** tab.
1. Click **Manage Custom Fields**.
1. Click **+New**.
1. In the **Create New Custom Field** screen, click **Event** or **Parameter** and provide a name for the event or parameter.

    > [!NOTE]
    > Event names are typically capitalized like `AddCart`, and parameter names use lowercase characters. Monetize will modify your parameter names if they don't match this convention.

1. If you’re creating a custom parameter, specify whether the expected value is a string or a number.
1. Provide any additional description in the **Description** field.
1. Click **Save** to save the event or parameter.

    Custom events will be displayed below the standard events in the **Events** tab. Custom parameters will be available to associate with any event (standard or custom) during event configuration.

## Related topics

- [Universal Pixel Object Limits](universal-pixel-object-limits.md)
- [Standard Events and Parameters](standard-events-and-parameters.md)
