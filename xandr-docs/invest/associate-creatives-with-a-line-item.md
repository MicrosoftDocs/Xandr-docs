---
title: Microsoft Invest - Associate Creatives with a Line Item 
description: Learn to associate creatives with an augmented line item (ALI) in this page.
ms.date: 10/28/2023
---


# Microsoft Invest - Associate creatives with a line item  

From the **Creatives** section, you can associate creatives with an augmented line item (ALI), schedule when the creatives will serve, determine how the creatives will rotate through line item inventory, and optionally add creative landing page URLs.

1. Select a [creative rotation strategy](creative-rotation-ali.md) to set the rotation strategy for multiple creatives of the same size that will be trafficked to the ALI:

   | Radio Button | Description |
   |--|--|
   | **Auto-optimize creative weight** | The creative with the highest click-through-rate (CTR) delivers the most. |
   | **Evenly weight creatives** | Our system will evenly serve creatives of the same size. |
   | **Manually weight creatives** | Rotation is based on a user-supplied weight. |
   | **Inherit creative weight from splits** | Rotation is based on a user-supplied weight defined per split. |

    If you're using a [custom model](https://docs.xandr.com/bundle/data-science-toolkit/page/custom-models.html) to deliver creatives, a message will display in the **Creatives** section identifying the model attached.

1. Associate the appropriate creatives to your ALI by doing one of the following:
    - Enter a name or ID of an existing creative in the **Search creative name or ID** search field, and select the corresponding checkboxes that display. You can also narrow your search by choosing a creative folder from the dropdown.

      > [!TIP]
      > You can also place your cursor in the **Search creative name or ID** search field and existing creatives that are associated to the same advertiser as the ALI will display.

    - Select the **Paste List of IDs** button and enter all  the associated creative IDs separated by commas or hard returns in the  modal and select **Add**.

      Each associated creative displays at the bottom of the **Associated Creatives** subsection, with associated active creatives on the first tab and associated inactive creatives on the second tab. Creatives will automatically serve for all flights unless you apply specific flights or custom dates that fall within the date ranges for a specific flight. When creatives are scheduled to serve for all flights and additional flights are added to the ALI, the creatives will continue to serve until the last flight ends.

1. Enter a value in the **Weight** field for each corresponding creative if the **Manually weight creatives** radio button was selected.
1. Select specific flights or custom dates that fall within the date ranges for these specific flights to schedule when associated creatives will serve by doing the following if necessary:
    1. Select corresponding checkboxes for the necessary creatives and select **Associate dates**. You can select multiple checkboxes if several of the creatives will serve during the same flights or custom dates.
    1. Select the **Select dates** button from the **Associate Dates** dialog if the creative will serve during specific flights.
    1. Select any of the available checkboxes to apply specific flights, or select the **Custom date range** checkbox and select start and end dates to specify a date range that doesn't include any dates before the start date or after the end date for one of the available flights. For example, if the flight has a start date of November 1 and an end date of December 1, then the custom date range cannot be any date before November 1 or after December 1.
    1. Select **Apply**.
1. Enter a **Landing Page URL** that the user will be redirected to upon selecting each creative.

## Related topics

- [Object Hierarchy](object-hierarchy.md)
- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
