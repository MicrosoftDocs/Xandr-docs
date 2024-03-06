---
title: Microsoft Monetize - Set Up Line Item Budgeting and Scheduling
description: Explore enhanced budgeting/scheduling; define parameters, revenue type, payment model, budget, flight duration for optimal campaign management.
ms.date: 10/28/2023
---

# Microsoft Monetize - Set up line item budgeting and scheduling

You can add revenue type, payment model, budget, flight, daily pacing allocation, underspend catch-up, and daypart details for the line item.

The **Budgeting & Scheduling** section defines how you will pay for media, as well as the financial relationship between you and the advertiser.

- **Payment Model** - The basis on which you will pay for media purchased through the line item
- **Budget** - How much the advertiser has allocated for you to spend (in money or impressions)
- **Revenue Type** - The basis on which the advertiser has agreed to pay you
- **Pacing** - How the budget is allocated over the duration of the advertising campaign
- **Budget Overview** - A helpful tool that shows you what your daily budgets will be throughout the life of your line item

Depending on how you have set the date and budget options on the parent insertion order, different configuration options will be available to you here. You can view the settings inherited from insertion order(s) in the panel to the right. This includes the **Budget Type**, **Currency**, **Total Lifetime Budget**, **Pacing**, **Start Date**, and **End Date**. If you have multiple insertion orders associated with a line item, use the arrows to scroll through them.

> [!NOTE]
> You can not modify your budget setup selection after you have created your line item.

To set up line item budgeting and scheduling:

1. Select a **Payment Model** to define the basis on which you will pay for the media. The payment model you choose will limit the **Revenue Type** options that are available.

   The following payment model types are available for selection:

   | Option | Description |
   |--|--|
   | **Standard** | Select this payment model type to pay media cost on a per impression basis. Enter the amount that the advertiser will pay you per thousand impressions in the **Revenue Value** field. |
   | **Outcomes** | Select this payment model type to use Guaranteed Outcomes, so you pay only for impressions that achieve a desired outcome. Available outcome depend on the line item ad type. For more detailed information and configuration instructions, see [Guaranteed Outcomes](guaranteed-outcomes.md). |

1. Select a **Revenue Type** to define how the advertiser has agreed to pay you. Available revenue types will depend on the previously selected ad type and payment model.

    **Fixed Revenue** pricing models indicate that your revenue will be the same regardless of media cost. Those options are:

   | Option | Description |
   |---|---|
   | **CPM** | Select this revenue type if the advertiser will pay you a flat amount per thousand impressions. Enter the amount that the advertiser will pay you per thousand impressions in the **Revenue Value** field. |
   | **CPC** | Select this revenue type if the advertiser will pay you a flat amount per click. This option is only available if the line item's **Budget Type** is set to **Revenue**. Enter the amount that the advertiser will pay you per click in the **Revenue Value** field. |
   | **Viewable CPM** | Select this revenue type if the advertiser will pay you a flat amount per thousand viewable impressions. Only measured viewable impressions will be counted, according to the Microsoft Advertising viewability measurement. Enter the amount in the **Revenue Value** field.<br>**Note**: If you select **Viewable CPM** (vCPM), you also have the opportunity to pay only for impressions that have been shown to be viewable. To do that, click **Outcomes** > **Guaranteed Views** under **Payment Model**. |
   | **CPCV** | Select this revenue type if the advertiser will pay you for videos that have been viewed through completion. Enter the amount that the advertiser will pay you per completed video in the **Revenue Value** field. This setting is available under **Revenue Type** only when **Video** is selected as the **Ad Type** and **Completes** is selected as the **Payment Model**. |

    **Flexible Revenue** pricing models indicate that your revenue may fluctuate depending on media/cost/spend. Those options are:

    | Option | Description |
    |---|---|
    | **Dynamic CPM** | Select this revenue type if you want to optimize to an average CPM goal. Select the **Maintain an average revenue CPM** checkbox if there is a business requirement. For example, if you're only paid when the average revenue CPM is below a certain cost, you can enter a maximum and/or minimum value for average revenue CPM. However, it's best not to specify these values unless you have to, because it may lead to decreased delivery. If you do specify one of the values, it is not required to set both a minimum and a maximum. The maximum average CPM is required when optimization is off, and no custom models are attached. However, if splits are being used, you're required to enter the maximum revenue bid but you don't have to enter the maximum average CPM.<br>**Note**: If you select **Dynamic CPM** as a revenue type, **Partner Fees** and **Data Costs** won't be subtracted from revenue. Instead, they'll be added to your **Media Cost**. Therefore, we can't guarantee a positive or break-even margin for your line item. |
    | **Cost Plus** | Select this revenue type if the advertiser will pay you your media cost (whatever you spend on buying inventory) plus an extra percentage of what you spend (margin). You can set the margin as a percentage of revenue (%) or a fixed CPM fee (**CPM margin**). Select the **Maintain an average revenue CPM** checkbox if there is a business requirement. For example, if you're only paid when the average revenue CPM is below a certain cost, you can enter a maximum and/or minimum value for average revenue CPM. However, it's best not to specify these values unless you have to, because it may lead to decreased delivery. If you do specify one of the values, it is not required to set both a minimum and a maximum. The maximum average CPM is required when optimization is off, and no custom models are attached. However, if splits are being used, you're required to enter the maximum revenue bid but you don't have to enter the maximum average CPM. |

1. Define your budget setup by selecting one of the following options:

   | Radio Button | Description |
   |---|---|
   | **Set Budgets** | Allows you to set an individual budget for each flight. You can set this value in the **Budget** field that displays for the individual flights. You must select this radio button if you decide to set **No End Date** on the individual flights. |
   | **Unlimited Budget** | Allows you to set an unlimited budget. The **Budget** field that displays for the individual flights is auto-populated with "Unlimited". |

1. If you have set the **Revenue Type** to **CPC** and would like to avoid potential overspend, set your **Lifetime Budget** to the *revenue value of your CPC x your revenue budget* (e.g., the number of clicks you would like to achieve). For example, if you had a CPC revenue value of $2 and a revenue budget of 10,000 clicks, you would set the **Lifetime Budget** field to $20,000. If you were setting budgets on each flight instead, you would divide that number accordingly across the flight budgets.
1. Set up flights by specifying their start and end dates, budgeting, and pacing.
Each line item must have at least one flight. Flights are subject to the following constraints:
    - Flights cannot overlap.
    - Flights must be at least one day long.
    - Flights must occur in the future.
    - Flight dates must fall inside the billing period dates of the parent insertion order(s).

   You can add a new flight by copying the billing period dates from the parent insertion order or by manually setting the start and end dates.

   1. To copy the flight dates from the parent insertion order, click **Copy from insertion order**.

      You can still edit the copied dates and add more flights.
  
   1. To set up flights manually, enter a start and end date. If you don't want to set an end date, click **No end date**.

      The **No end date** option is only available if you selected the **Set budget on individual flights** for the line item and if the parent insertion order has no end date.

      > [!NOTE]
      >  If you don't set an end date:
      > - You can only have one flight.
      > - You won't be able to create any additional flights for this line item.
      > - You won't be able to change the start date once it has passed.

   1. To set flight budgeting, enter a budget in the **Budget** field.

      This option is only available if you selected **Set budget on individual flights** when setting up the line item budget.

   1. Set the flight pacing.

      Pacing determines how much of your flight budget is spent per day. You can set the pacing by using a flight pacing percentage or a daily budget. For more information on flight pacing, see [Lifetime Pacing](lifetime-pacing.md) and [Adaptive Pacing](adaptive-pacing.md).

      | **Flight Pacing Option** | Description |
      |---|---|
      | **Pacing percent** | This setting dictates how your flight relatively distributes and spends its allocated budget. Pacing percent values may be 50%-150%.<br>If the pacing is set to 100%, the budget is split evenly over every day in the flight. If the pacing is higher than 100%, the flight spends more per day at the beginning of the flight and less at the end. The reverse occurs if the pacing is lower than 100%. |
      | **Daily budget** | The amount of budget spent per day.<br>The budget can be currency, imps, completes, or views, depending on the budget type and payment model you selected earlier. |

1. **Optional:** Click **+Add Subflight** to create one or more subflights that you can use to further customize flight pacing and spend.

    > [!NOTE]
    >  Budget subflights are an **Alpha** feature that allow you to set custom budget and pacing settings for specific days within a line item flight. If you'd like to gain access to them, please contact your Microsoft Advertising account representative.

   1. Enter a name for your subflight.
   1. Select a start and end date for your subflight.

      Alternatively, you can click **Copy from flight** to copy the start and end dates of the parent
        flight.

       > [!NOTE]
       > Line items can use no more than one subflight for any given date.

   1. Toggle **Recurring** to select certain days of the week for which your subflight will take effect.

   1. Set subflight pacing.

      Pacing determines how much of your subflight budget is spent per day. You can set the pacing by using a subflight pacing percentage or a daily budget. For more information on flight pacing, see [Lifetime Pacing](lifetime-pacing.md) and [Adaptive Pacing](adaptive-pacing.md).

      | Option | Description |
      |---|---|
      | **Pacing percent** | This setting dictates how your subflight relatively distributes and spends its allocated budget. Pacing percent values may be between 50%-150%.<br>If the pacing is set to 100%, the budget is split evenly over every day in the flight. If the pacing is higher than 100%, the flight spends more per day at the beginning of the flight and progressively less at the end. The reverse occurs if the pacing is lower than 100%. |
      | **Daily budget** | The amount of budget spent per day.<br>The budget can be currency, imps, completes, or views, depending on the budget type and payment model you selected earlier.<br>**Note**: If your line item is underspending when using subflights with daily budgets, underspend catch-up settings will take effect once those subflights have ended. |

1. Select one of the following **Underspend Catch-Up** settings to dictate how your line item distributes unspent budget throughout the remainder of a flight:

    > [!NOTE]
    > Underspend Catch-Up will not have any effect if **Daily budget** option is selected. It will only have an impact when **Pacing percent** is used.

    | Button | Description |
    |---|---|
    | **Evenly (default)** | Select this option if you want your unspent daily budget distributed evenly through the remainder of the flight. |
    | **ASAP** | Select this option if you want the unspent portion of your daily budget to be spent as quickly as possible. |

1. Set the necessary [Daypart Targeting](daypart-targeting.md) settings to target users based on the day and time when they see impressions.
1. Select one of the following **Daily Pacing Allocation** buttons to set the pace for how quickly the budget should be spent in one day:

    | Button | Description |
    |---|---|
    | **Evenly (default)** | Leave this button selected if you want the daily budget distributed evenly throughout the day based on the available impressions within a specific geographic area. |
    | **ASAP** | Select this button if you want to spend the budget as quickly as possible. This will allow the line item to spend as impressions become available rather than following a spend curve based on available impressions for a specific geographic area. This will also result in [Adaptive Pacing](adaptive-pacing.md) not bid shading impressions.<br>**Warning**: Overspend is more likely to occur when ASAP is selected. |

   1. **Optional:** If desired, click **+New** to activate **Hourly Pacing Overrides**.

      Activating **Hourly Pacing Overrides** lets you override your line item's default pacing behavior to manually set hour-to-hour pacing for specific dates or days of the week. Upon clicking **+New**, the **Create Custom Pacing Allocation Curve** dialog displays.

   1. Click **Select Dates** or **Select Days of Week** depending on whether you want to pace hourly for a particular date range or certain days of the week.
  
   1. Drag the line graph to allocate pacing percentages for certain hours, or enter percent values into hour slots' text fields.

      > [!NOTE]
      > Hourly pacing percent allocations must equal 100%.

   1. Click **Save**.

1. Use the **Budget Overview** graph to see how your lifetime budget will be distributed across the active dates in your flight.

## Related topics

- [Create an Augmented Line Item](create-an-augmented-line-item-ali.md)
- [Lifetime Pacing](lifetime-pacing.md)
- [Adaptive Pacing](adaptive-pacing.md)