---
title: Yield Analytics 8.9
description: Learn about Internationalization and how this feature affects items within Yield Analytics like Currency symbols and local settings. 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Yield Analytics 8.9

**Internationalization:**  This feature enhances the following items within Yield Analytics :

1. Currency symbols will be updated to reflect the currency that is used for all revenue values in the system.
1. Users will have the ability to override their locale setting to have date, number, and currency formats be representative of their defined locale format.
1. Excel exports will read the preference set on the user who is downloading the reports, and export the report in the proper format.

**Details**

Our international clients have long asked for the Yield Analytics UI to more accurately reflect the currency symbol that they use for reporting, along with respecting local formats for both numbers and dates. This week’s release will address both requests, with several changes:

- Currency Symbols: This represents the currency that the publisher is set to and display the proper symbol.
- Locale Settings: Clients will be configured to a locale based on the default for the publisher. However, individual users can set their locale setting through the Preference page of. In the case of no network configuration, users will default to using the United States (en-US) locale.

This is a view of the preference page where locale can be configured.

> [!NOTE]
> The “Country Format” field is where locale is specified in a new selection box on the existing preference page. There is not a new page for this.

:::image type="content" source="media/f.png" alt-text="Screenshot of preference page where locale can be configured.":::

A look at dates/numbers using the default en-US locale:

:::image type="content" source="media/g.png" alt-text="Screenshot of dates and numbers using the default en-US locale.":::

A look at dates/numbers using the new fr-FR locale:

:::image type="content" source="media/h.png" alt-text="Screenshot of dates and numbers using the new fr-FR locale.":::

Our Excel exports will also support localized formatting. We will begin respecting the Language & Region settings configured on a user’s computer when they open a Yield Analytics export in Excel. This will allow them to see data within Excel identical to how it will be displayed in the Yield Analytics UI.
