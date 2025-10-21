---
title: Microsoft Monetize - Add Basic Line Item Details
description: In this article, find step-by-step instructions for how to add basic details to a line item.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Add basic line item details

You can set the name, state, and ad type, as well as associate additional insertion orders to the line item, all from the **Basic Settings** section. You can also optionally assign an external code.

1. Enter the name that you will use to search for and report on the line item.

    The name of the line item must be unique per advertiser.

1. Click **+External Code** and enter a code if you want to report on a line item using your own code (rather than the internal ID that Microsoft Advertising assigns automatically).

    External codes must follow these guidelines:
    - They can contain only alphanumeric characters, periods, underscores, or dashes.
    - Codes are not case-sensitive (upper-case and lower-case characters are treated the same).
    - No two objects can use the same code per advertiser. For example, two line items cannot both use code "ABC."

1. Set the **State**.

    We recommend that you set the state to **Inactive** until everything on the buyside has been set up and verified. Therefore, spending won't occur until you're ready.

    > [!NOTE]
    > If a user's settings require them to receive approval before activating a line item, a banner message will display stating that peer approval is required.

1. Associate additional insertion orders to the line item by doing the following:
    1. Click the pencil icon above the existing insertion order that displays.

        A list of corresponding insertion orders displays automatically.

    1. Search for additional existing insertion orders if necessary.

    1. Select the corresponding check marks to associate the necessary insertion orders that display.

        You won't be able to select particular insertion orders if their billing periods overlap or conflict with the billing periods of the insertion order that was previously associated to the line item.

    1. Click **Save**.

1. Leave **Banner** selected as the **Ad Type** or select a different option.

    The ad type must match the creative types that you will associate with the line item. This setting determines how auction items are tracked for the line item's buying strategy, payment strategy, optimization options, creative association, and targeting options.

## Related topics

- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
- [Creative Types](creative-types.md)
- [Peer Approval](peer-approval.md)
