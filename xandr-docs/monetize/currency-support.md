---
title: Microsoft Monetize - Currency Support
description: This page gives an overview on currency. Learn what are the prerequisite concepts that you need to know and what all currencies Microsoft Advertising supports. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Currency support

Support for multiple currencies allows buyers and sellers to transact with one another globally on the Microsoft Advertising platform. However, it is important for all parties to understand how spending and payment in different currencies flows from buyers to sellers and partners on the platform. This page provides an explanation of all relevant concepts, processes and settings. In addition, Microsoft Advertising is expanding its support for non-USD currencies (as part of a larger multi-year platform-wide localization effort). As a result, this page will be updated periodically to explain how these changes affect the currencies supported on the platform, reporting and invoicing and what customization options you have. If you have questions about currency support please contact your Account Manager.

## Prerequisite concepts

Ensure you understand these basics before proceeding (each of these concepts is discussed in greater detail in dedicated sections below):

1. **Base currency:** Microsoft Advertising' default currency is USD.
    - Although USD is the default currency, Microsoft Advertising supports the **buying and selling ("transacting")** of impressions as well as **billing** in a number of different non-USD currencies.
    - Microsoft Advertising performs all calculations in USD. To support non-USD use cases, we convert in and out of USD (as needed) using the latest exchange rates from our [API Currency Service](../digital-platform-api/currency-service.md).
1. **Supported local currencies and exchange rates:** Our [API Currency Service](../digital-platform-api/currency-service.md) updates exchange rates platform-wide on a daily basis based on the most current [Refinitiv](https://www.lseg.com/en/fx) rates.  
1. **Transaction and billing currency and account setup:**
    Microsoft Advertising distinguishes between the currencies you transact in (currencies you select in the Digital Platform UI/API for buying/selling) and the currency you are billed in (currency in which you are invoiced or paid). Generally, Microsoft Advertising bills clients for fees/charges based on the daily conversion rate logged at the time the relevant auction took place. However, in the following scenarios, we use the month-end rate to bill (for a full list, see [Media cost and related fees conversion for billing](#media-cost-and-related-fees-conversion-for-billing) below):
    - The transaction currency differs from the billing currency
    - We can't easily associate a fee back to an auction (e.g., Ad Serving Fees, Minimums, Log Level Data Fees, etc.)

## Base currency (USD)

Microsoft Advertising uses USD as the default currency (also referred to as "base" or "primary" currency). However, we support transacting in a wide range of currencies. When we need to compare values across the platform, we use a common unit of measure; our base currency of USD (which we convert into). This conversion practice is used across the platform when evaluating bids, running auctions, managing budgets or optimizing performance across the currencies we support. However, none of these conversions will change the local currency amount since we convert in and out of the local currency using the same rate.

## Supported currencies

If you have signed a contract with Microsoft Advertising, the following non-USD currencies are supported.

| Currency | Transaction | Billing |
|--|--|--|
| Argentine Peso (ARS) | X | X |
| Australian Dollar (AUD) | X | X |
| Brazilian Real (BRL) | X | X |
| British Pound (GBP) | X | X |
| Canadian Dollar (CAD) | X | X |
| Chilean Peso (CLP) | X |  |
| Chinese Yuan (CNY) | X |  |
| Colombian Peso (COP) | X |  |
| Czech Koruna (CZK) | X | |
| Danish Krone (DKK) | X | X |
| Egyptian Pound (EGP) | X |  |
| Euro (EUR) | X | X |
| Hong Kong Dollar (HKD) | X | X |
| Hungarian Forint (HUF) | X | |
| Indian Rupee (INR) | X | X |
| Indonesian Rupiah (IDR) | X | X |
| Israeli Shekel (ILS) | X |  |
| Japanese Yen (JPY) | X | X |
| Kazakhstani Tenge (KZT) | X |  |
| Malaysian Ringgit (MYR) | X | X |
| Mexican Peso (MXN) | X | X |
| New Zealand Dollar (NZD) | X | X |
| Nigerian Naira (NGN) | X | X |
| Norwegian Krone (NOK) | X | X |
| Pakistani Rupee (PKR) | X |  |
| Peruvian Nuevo Sol (PEN) | X |  |
| Philippine Peso (PHP) | X | X |
| Polish Złoty (PLN) | X | X |
| Qatari Riyal (QAR) | X |  |
| Romanian Leu (RON) | X |  |
| Saudi Riyal (SAR) | X |  |
| Serbian Dinar (RSD) | X |  |
| Singapore Dollar (SGD) | X | X |
| South African Rand (ZAR) | X | X |
| South Korean Won (KRW) | X |  |
| Swedish Krona (SEK) | X | X |
| Swiss Franc (CHF) | X | X |
| Taiwan Dollar (TWD) | X | |
| Thai Baht (THB) | X | X |
| Tunisian Dinar (TND) | X |  |
| Turkish Lira (TRY) | X | X |
| Ukrainian Hryvnia (UAH) | X |  |
| United Arab Emirates Dirham (AED) | X | X |
| United States Dollar (USD) | X | X |
| Vietnamese Dong (VND) | X | |

- **Transaction Currency** is the currency used to buy or sell inventory on the platform.
  - For Buyers, this is set at the Line Item level (or inherited from the network/member or Insertion Order level if not explicitly set at the Line Item).
  - For Sellers, this is set at the Publisher level.
  - Users can manually set a transaction currency on most objects (e.g., Insertion Orders, Line Items).
  - A given member/network might have multiple transaction currencies if they set up objects in different currencies (i.e., Advertiser A = EUR, Advertiser B = USD, Publisher C = GBP, etc.)
- **Billing Currency** is the currency in which you are invoiced and/or paid by Microsoft Advertising. Each member has only one billing currency (specified in your contract). If you would like to change your billing currency, contact your Account Manager.

> [!NOTE]
> Not all currencies available for **transacting** are available for **billing** (invoicing). If you set your transaction currency to anything other than your billing currency, the amount you are billed at month-end may not exactly match the totaled sum of all transaction amounts. This is because the transaction values are calculated after each auction and billing is totaled monthly using the conversion rate at the end of the month.

## Exchange rates

Exchange Rates are sourced once daily from [Refinitiv](https://www.lseg.com/en/fx) at approximately 3:00 a.m. UTC. All Microsoft Advertising applications (bidder, budgeting, billing, etc.) use the [API Currency Service](../digital-platform-api/currency-service.md) (also available to clients) to access the latest rates. This service provides centralized, consistent and uniform exchange rates across the entire platform. The API Currency Service is available to clients solely to reconcile amounts paid or received by them resulting from their transactions through the Microsoft Advertising Platform and may not be used by clients for any other purpose.

> [!NOTE]
> Due to the distributed nature of our systems, new rates will not be populated across all of our servers simultaneously.

## Account setup

Users can set the transaction currency for certain buy and sell side objects (listed below under Currency Settings per Object) under their member. The buy/sell side object currency settings control one or both of the following:

1. The default currency for any child objects created under the parent (e.g., Insertion Order determines the currency of its Line Items). The user can override the default currency set at the parent object.
1. Transacting (buying or selling inventory). This is the currency of record for the object since it's what is actually logged for each auction.

See "Currency Settings per Object" below for more details on the objects that have currency setting and what those settings affect.

> [!NOTE]
> While you are able to set currency on many objects, the only two which are actually used to buy and sell are those set on the **Line Item** (for the buy side) and **Publisher** (for the sell side). The currencies set on these two objects are what is actually logged by and used for transacting on the platform.

## Currency settings per object

The table below explains when you can set currencies and the effects of those settings.

| Currency Setting | Default/Settable? | Controls/Affects |
|--|--|--|
| **Advertiser** | **Default**: USD<br>**Settable?**: Users can update. Since there is no budget set at this level, you can always change the advertiser currency.<br>**Where set**:<br> - API: via the `default_currency` field in the [Advertiser Service](../digital-platform-api/advertiser-service.md)<br> - UI: via the **Currency** field (under **Default Settings**) of the **Advertiser** screen | This setting controls the default currency for any new child objects you create (i.e., you set it once on the Advertiser and all Insertion Orders and Line Items inherit that currency).<br> - Only used for buying or selling inventory if you don't set a different currency on the Insertion Order or Line Item.<br> - Only used in reporting if you don't set a different currency on the Insertion Order or Line Item. |
| **BUY SIDE** |  |  |
| BUY/SELL SIDE |  |  |
| **Campaign** | **Default**: Inherits the value of the Line Item level currency setting.<br>**Settable?**: User can't update. |  |
| **Insertion Order (IO)** | **Default**: Inherits the currency setting of the IO's Advertiser.<br>**Settable?**: User can set up IOs with any of the supported transaction currencies when creating a new IO.<br>**Note**: Once an IO is saved, the currency cannot be changed as any changes will have budget implications. This includes both active and inactive IOs. If you need to change the currency of an existing IO, clone it and set the second IO to your desired currency. Then set the original IO to inactive. However, the new IO will not have any of the cloned IO's buying history.<br>**Where set**:<br> - API: via the `currency` field in the [Insertion Order Service](../digital-platform-api/insertion-order-service.md)<br> - UI: via the **Currency** field of the **Insertion Order** screen | The IO's currency setting is only used to manage its budget, not to actually buy inventory.<br> - Only used for buying or selling inventory if you don't set a different currency on the line item.<br> - This is not logged for reporting. |
| **Line Item** | **Default**: Inherits the currency setting of the Line Item's Advertiser.<br>**Note**: If you are using IOs, the Line Item's currency must match that of its parent IO.<br>**Settable?**: Can be set to any supported transaction currencies (unless you are using IOs). Once a Line Item is saved, the currency cannot be changed as any changes will have budget implications. This includes active and inactive Line Items.<br>**Where set**:<br> - API: via the `currency` field in the [Line Item Service](../digital-platform-api/line-item-service.md)<br> - UI: via the **Currency** field of the **Line Item** screen | - **This is the Transaction Currency if you are buying inventory**<br> - This currency and its USD exchange rate at the time of the auction are logged when the auction occurs. |
| **Member/Network** | **Default**: USD<br>**Settable?**: User can’t update (contact Account Manager to change). Since there is no budget set at this level, your account manager can always change the member currency at your request. | This setting controls the default currency for child objects you create. This is only used for buying or selling inventory (and reporting) if you don't set a (different) currency on the Advertiser, Insertion Order or Line Item. |
| **Placement Groups** | **Default**: Inherits the value from the Network or Publisher setting.<br>**Settable?**: User can't update the currency for Placement Groups (refer to the Publisher to view the currency). |  |
| **Placements** | **Default**: Inherits the value from the Network or Publisher setting.<br>**Settable?**: User can't update the currency for placements (refer to the Publisher to view the currency). |  |
| **Publisher** | **Default**: Inherits the currency setting of the Publisher's Network.<br>**Settable?**: User can set any of the supported transaction currencies when creating a Publisher. Once a Publisher is saved (including inactive publishers), the currency cannot be changed.<br>The exception to this rule is that clients can change the publisher currency using the Publisher API service.<br>**Note**: Changing the currency can result in issues with reporting. It is recommended to change the currency on the **first day of the month**. This will minimize these issues.<br>**Where set**:<br> - API: via the `currency` field in the [Publisher Service](../digital-platform-api/publisher-service.md) | - This is the **Transaction Currency** if you are selling inventory.<br> - This currency and its USD exchange rate at the time of the auction are logged when the auction occurs. |
| **SELL SIDE** |  |  |

## Start transacting using multiple currencies

Once you've set the currency for your member and any objects (e.g., Insertion Orders, Line Items, Campaigns) for which you want to have a different currency, you can start buying and selling inventory.

### Buying

1. Set your budget(s) at the Insertion Order and Line Item levels (in your Transaction Currency).
1. Once your Line Items and Campaigns have been set to active and are within their flight dates/billing periods, the system will place bids in the currency you selected until your budget has been spent.

### Selling

1. When you set a Publisher to active and begin selling, buyers will begin submitting their bids for that Publisher's inventory. Although these bids may be submitted in multiple currencies (depending on each buyer's settings), Microsoft Advertising will convert all bids received to USD in order to evaluate the auction using a single currency.
1. To enforce any Publisher floors, Microsoft Advertising converts the local currency floor price to USD, then compares the floor to the net bids (already converted to USD) to eliminate unwanted bids.
1. The auction is run and all results are logged in USD. In addition, Microsoft Advertising logs the Transaction Currency (Publisher currency) and the applicable exchange rate at the time of auction.

### Conversions made during the auction

We convert all non-USD bids (e.g., if Line Item has been set to a currency other than USD) into USD (Base Currency) so we can compare bids in the same unit of measurement. All these converted bids are sent through our auction logic and the winning bid is priced appropriately in USD. Finally, after the auction is complete, we log all results in USD, along with your Transaction Currency and the applicable exchange rate that was used to initially convert the bid into USD.

When viewing your auction activity via reporting or log level data feeds, you have the option to view monetary fields in either USD or the Transaction Currency (labeled Buying Currency in reports). To display reports in the Transaction Currency(ies), we convert the USD values to the Transaction Currency using the rates logged for each auction. This provides you with the most accurate local currency values which you can then use for forecasting and billing reconciliation.

## Reporting and analytics

Once an auction has been completed, you can review the details related to it in your Transaction Currency using reporting, log level data or within specific locations in the UI (e.g., Quick Stats, Grids, etc.).

### Reports

| Report Name | What it contains |
|--|--|
| **Buying Billing Report** | - Monetary fields are displayed in local currency by default.<br> - "Buying Currency" is a default dimension. All monetary fields are displayed in the Transaction Currency (Line Item currency) logged at auction time.<br> - Deselecting "Buying Currency" as a dimension will display all monetary fields in USD. |
| **Network Analytics Report** | - Monetary fields are displayed in USD by default.<br> - Selecting "Buying Currency" as a dimension will display all monetary fields in the Transaction Currency (Line Item currency) logged at auction time.<br> - Selecting "Selling Currency" as a dimension will display all monetary fields in the Transaction Currency (Publisher currency) logged at auction time. |
| **Selling Billing Report** | - Monetary fields are displayed in local currency by default.<br> - "Selling Currency" is a default dimension. All monetary fields are displayed in the Transaction Currency (Publisher currency) logged at auction time.<br> - Deselecting "Selling Currency" as a dimension will display all monetary fields in USD. |

### UI/Analytics

Line Item and Campaign revenue metrics can be displayed in Transaction Currency, however all other grids and monetary metrics are displayed in USD only. Be sure to note which currency your data is being displayed in and if it's not in your Transaction Currency, use the reports (listed above) to view auction details in the your Transaction Currency.

## Media cost and related fees conversion for billing

The conversion of media cost and fees to the billing currency will be based on either daily conversion rates or a month-end conversion rate. To determine which will be used and which fees will be affected, refer to the table below.

| Daily conversions (depends) | Month-end conversion (depends) | Month-end conversion (always) |
|--|--|--|
| **When Used?** If the Transaction Currency (currency logged at auction time) is the same as the Billing Currency.<br>**How Applied?** When these criteria are met, we convert from USD to the Billing Currency using the rates logged for each auction. This provides our clients with the most accurate local currency billing and reconciles with our reporting and data feeds which support local currency. | **When Used?** If the Transaction Currency (currency logged at auction time) is different from the Billing Currency.<br>**How Applied?** We calculate the fee in USD and convert from USD to the desired Billing Currency using the month end rate. You can access this rate by asking our API Currency Service for the rate on the last day of a given month. | **When Used?** Always (only for the fees listed in this column)<br>**How Applied?** We calculate the fee in USD and convert from USD to the desired billing currency using the month end rate. You can access this rate by asking our API Currency Service for the rate on the last day of a given month. |
| **Which Fees/charges?**<br> - Buy side costs and charges<br>&nbsp; - Media Cost<br>&nbsp; - BASC Deductions<br>&nbsp; - BASC Fees<br>&nbsp; - Direct Clear Fees<br>&nbsp; - Creative Overage Fees<br> &nbsp; - Data Costs<br> &nbsp; - Sell side revenue and charges<br>&nbsp;&nbsp;&nbsp; - Seller Revenue<br>&nbsp;&nbsp;&nbsp; -SASC Deduction<br>&nbsp;&nbsp;&nbsp; -SASC Fee<br> - Managed Ad Serving Fee<br> - Buyer Serving Fee<br> - Seller Serving Fee<br> - Imp Tracker Fee<br> - Click Tracker Fee | **Which Fees/charges?**<br><br> - Buy side costs and charges<br>&nbsp; - Media Cost<br>&nbsp;&nbsp; - BASC Deductions<br>&nbsp;&nbsp; - BASC Fees<br>&nbsp;&nbsp; - Direct Clear Fees<br> &nbsp;&nbsp; - Creative Overage Fees<br> &nbsp;&nbsp; - Data Costs<br>&nbsp;&nbsp; - Sell side revenue and charges<br>&nbsp;&nbsp;&nbsp; - Seller Revenue<br>&nbsp;&nbsp;&nbsp; - SASC Deduction<br> &nbsp;&nbsp;&nbsp; - SASC Fee<br>- Managed Ad Serving Fee<br> - Buyer Serving Fee<br>  - Seller Serving Fee<br> - Imp Tracker Fee<br> - Click Tracker Fee | **Which Fees/charges?**<br> - Creative Audit Fee<br> - Priority Creative Audit Fee<br> - Log Level Data Fee<br> - Seller Revshare Min<br> - Other Mins<br> - Onboarding Fee<br> - Microsoft Advertising Service Fee<br> - Other Flat Fees<br> - Other CPM Fees |
|  |  |  |
