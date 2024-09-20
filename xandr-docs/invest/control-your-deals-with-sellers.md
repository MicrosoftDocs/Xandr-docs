---
title: Microsoft Invest - Control Your Deals with Sellers
description: On the Deals screen, learn how to set deal review preferences, accept or decline deals, manage status and assign deal alias.   
ms.date: 10/28/2023
---

# Microsoft Invest - Control your deals with sellers

You can control deals received from sellers on the **Deals** screen. You can:

- Set deal review preferences to require a review or allow any new deals received from a seller to be set to Active status automatically
- Accept or decline deals upon review
- Manage the status of deals at any time by accepting, deactivating, or declining them
- Assign a deal alias (internal name) to any seller deal for easier management within your organization

> [!NOTE]
> For more information on managing deals with sellers including viewing basic and advanced deal metrics, monitoring each deal's health, and running detailed reports, see [Manage Your Deals with Sellers](manage-your-deals-with-sellers.md).

## Locate the deals screen

To reach the **Deals with Sellers** screen, select **Partners** \> **Deals** and select the **Sellers** tab.

## Set deal review preferences

Buyers can configure the default manner in which they process new seller deals by selecting one of the following settings:

- **Default Active**: new seller deals will be set to **Active** status by default when received. Deals can be declined or changed to **Inactive** status later if necessary (see [Manage Deal Status](#manage-deal-status)).
- **Require Review**: new seller deals will be set to **Pending** status by default when received until the deals are reviewed by the buyer and accepted or declined (see [Accept or Decline Deals](#accept-or-decline-deals)).

> [!NOTE]
>
> - **Default Active** is the default setting if no deal review preference is set.
> - Changing the review preference only affects new deals. It does not change the status of existing deals.

To set the deal review preference for new seller deals, do the following:

1. Select **Partners \> Deals** and select the **Sellers** tab.
1. On the top right of the **Deals** screen, select the edit icon on **New Deals Do Not Require Approval** (or **New Deals Require Approval** if it’s been changed previously) to open **Review Preferences**.
1. On the **Review Preferences** page, select either:
    - **Default Active** – to accept all new deals and set their status to **Active**
    - **Require Review** – to require review of all new deals before accepting or declining them
1. Select **Save**.

## Accept or decline deals

If you have set your buyer review preference to **Require Review** see [Set Deal Review Preferences](#set-deal-review-preferences), you can then review new deals and accept or decline them. You can also accept or decline deals that are in any status (i.e., **Pending**, **Active**, **Inactive**, or **Declined**). Accepting deals changes the deal status to **Active** and declining deals changes the deal status to **Declined**.

## Accepted deals

When you select **Accept**, the deal is:

- Added to your list of **Active** deals
- Eligible for targeting
- Passed to the bidstream

> [!NOTE]
> Accepted deals can be set to **Inactive** status see [Manage Deal Status](#manage-deal-status) if you want to remove them from the list of **Active** deals.

## Declined deals

When you select **Decline**, the deal is:

- Added to your list of **Declined** deals
- Not eligible for targeting
- Not passed to the bidstream

> [!NOTE]
> You can change **Declined** deals to **Active** at any time (see [Manage Deal Status](#manage-deal-status)).

To accept or decline one or more new deals:

1. Select **Partners \> Deals** and select the **Sellers** tab.
1. Check the box next to any deals you want to accept or decline (you can search by **Deal Name**, **Deal Alias**, **Deal ID**, or **Code**).
1. In the **Select** drop-down, select **Accept** or **Decline**.

## Manage deal status

You can manage the status of deals so you can control when each deal is available for targeting. A deal can have a status of **Pending**, **Active**, **Declined**, or **Inactive**. The following table provides a description of each status, when the status occurs, and available actions you can perform given the status of the deal:

| Buyer Deal Status | Description | Status Occurs When: | Available Actions |
|:-|:-|:-|:-|
| **Pending** | - Deal not passed in bidstream<br> - Not available for targeting <br> - Not included in **Target All Deals** | **Review Preferences** set to **Require Review**. | **Accept** or **Decline** deal. |
| **Active** | - Deal passed in bidstream <br> - Available for targeting, and included in **Target All Deals**. | - **Review Preferences** set to **Default Active** <br>  - **Pending** deal is accepted.<br>- **Inactive** or **Declined** deal set to **Active**. | Set status to **Inactive** or **Declined** |
| **Declined** | - Deal not passed in bidstream<br> -Not available for targeting<br> - Not included in **Target All Deals** | - **Pending** deal is declined.<br> - **Active** deal set to **Declined** | Set status to **Active** or **Inactive** |
| **Inactive** | - Deal not passed in bidstream <br> - Not available for targeting <br> - Not included in **Target All Deals** | **Active** deal set to **Inactive**. | Set status to **Active** or **Declined**. |

## Change deal status

To change the status of deals you receive from sellers to **Active**, **Inactive**, or **Declined**, do the following:

- When you set a deal to **Active** status, it will only be active if the seller has activated the deal.
- You cannot change the status of a deal to **Pending**. This status is only set if a new deal is received when **Review Preferences** is set to **Require Review**.

1. Select **Partners \> Deals** and select the **Sellers** tab
1. Select anywhere in the row of the deal you want to change the status of (you can search by **Deal Name**, **Deal Alias**, **Deal ID**, or **Code** to find a specific deal).
1. In the **Deal Controls** section, select the edit icon and select a status from the **Acceptance Status** drop-down.
1. Select **Save**.

## Set groups of deals to Active or Declined status

While you can change the status of each deal to **Active** or **Declined** using the **Deal Controls** of each deal, you can only make these changes one deal at a time. If you have a group of deals that you’d like to set to **Active** or **Declined** status, you can check the box next to these deals and select **Accept** in the **Select** drop-down to set them to **Active** status, or **Decline** to set them to **Declined** status (see [Accept or Decline Deals](#accept-or-decline-deals)).

## Assign a deal alias

You can assign a **Deal Alias** to use as a buyer internal name for seller deals so you can manage these deals by a name you provide for it. The alias you assign to a deal appears in the **Deal Alias** column of the **Deals with Sellers** page along with the **Deal Name** that the seller provided for the deal.

> [!NOTE]
> The Deal Alias you assign to a deal is not viewable by the seller of the deal.

To assign a **Deal Alias** to a deal, do the following:

> [!NOTE]
> The **Deal Alias** field is limited to 254 characters.

1. Select **Partners** \> **Deals** and **select** the **Sellers** tab.
1. Select anywhere in the row of the deal you want to assign a **Deal Alias** to (you can search by **Deal Name**, **Deal Alias**, **Deal ID**, or **Code** to find a specific deal).
1. In the **Deal Controls** section, select the edit icon and enter the internal name in the **Deal Alias** field.
1. Select **Save**.

## Related topics

- [Manage Your Deals with Sellers](manage-your-deals-with-sellers.md)
- [Partnership Details Screen](partnership-details-screen-buyer-view.md)
<!-- [Get Deals from Seller Packages](get-deals-from-seller-packages.md)-->
- [Buy-Side Reporting on Deals](buy-side-reporting-on-deals.md)
