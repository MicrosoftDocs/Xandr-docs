---
title: Microsoft Curate - Create Custom Events and Parameters
description: Generate custom pixel parameters on Universal Pixels page. Select pencil icon, create events/parameters via UI, integrate into pixel code.
---

# Microsoft Curate - Create custom events and parameters

If you select the pencil icon next to a pixel on the **Universal Pixels** page, you can create custom events and parameters for the universal pixel using the UI and include them in your generated pixel code.

Custom events are values set on the event key. Custom parameters are dynamically populated key-value pairs that contain additional metadata about an event, and are always associated with a standard or custom event.

To set up custom events and parameters:

1. On the **Universal Pixel** page, select the pencil icon next to the name of the pixel.
1. In the right pane, select the **Events** tab.
1. Select **Manage Custom Fields**.
1. Select **+New**.
1. In the **Create New Custom Field** screen, Select **Event** or **Parameter** and provide a name for the event or parameter.

  > [!NOTE]
  > Event names are typically capitalized like `AddCart`, and parameter names use lowercase characters. Curate will modify your parameter  names if they don't match this convention.

1. If you’re creating a custom parameter, specify whether the expected value is a string or a number.
1. Provide any additional description in the **Description** field.
1. Select **Save** to save the event or parameter. Custom events will be displayed below the standard events in the **Events** tab. Custom parameters will be available to associate with any event (standard or custom) during event configuration.

## Related topics

- [Universal Pixel Object Limits](universal-pixel-object-limits.md)
- [Standard Events and Parameters](standard-events-and-parameters.md)
