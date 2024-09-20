---
title: DFP sales managers Yield Analytics extension
description: Learn how to install the Yield Analytics Sales Manager Extension and how it automatically updates.
ms.date: 10/28/2023
ms.custom: yield-analytics-ui
---

# DFP sales managers Yield Analytics extension

## Background

You can access Yield Analytics derived forecast and contention information directly in the DFP Sales Management interface using our Chrome browser extension. This method of accessing our data is particularly convenient for users who do not normally work in the Yield Analytics user interface, but have a regular need to respond to proposal requests and enter/update orders in the Sales Management product.

## Installation instructions

Users who access Sales Manager using the Chrome browser are able to take advantage of this functionality by following the installation and setup instructions:

1. Open the Chrome application.
1. Navigate to the following link: [Yieldex Analytics Sales Manager Extension Overview](https://chrome.google.com/webstore/detail/yieldex-analytics-sales-m/ingnfjfbgglccomoildaalnppeifljlk).
1. Select **Add to Chrome** to install the plugin.
1. On the dialog that appears, select **Add extension** to confirm the installation.
1. View the Yield Analytics Sales Manager Extension in Chrome.
1. Select on the Customize and control Google Chrome link in the menu bar. (<b>Note:</b> This is the three vertical dots link.)
1. Select **More Tools**, and select **Extensions**.
    1. Select on the Details link of the Yield Analytics Sales Manager Extension to view the configuration options.
    1. If you intend to use the extension in incognito mode, you must enable the incognito control on the details page.
        1. select on the Extension options link to set up your account.
        1. Enter the same Username and Password that are used for accessing the Yield Analytics user interface.
        1. Enter the full Customer URL that is used for accessing your customer instance of the Yield Analytics user interface. This should be entered without the https:// portion of the URL.
        1. Once entered, login changes are saved automatically.
1. After installing the Google Sales Manager Plugin, you will need to log out and back into Sales Manager in order to see the Yield Analytics capacity and availability results appear on the pages that are listed below.

## Update instructions

The Yield Analytics Sales Manager Extension should update automatically when a new version is pushed to the Chrome Web Store.  In the case where you want the plugin to update on demand, the following steps can be taken to manually control the process.

1. View installed Chrome Extensions.
1. Select on the Customize and control Google Chrome link in the menu bar. (<b>Note:</b> This is the three vertical dots link.)

    Select **More Tools**, and select **Extensions**.
    1. Enable Developer Mode by selecting on the configuration option in the upper right-hand corner of the extension page.
    1. A new series of options will appear on the Extension page including an UPDATE option. Selecting this link will force all installed extensions to update to their latest versions.

If you are unable to force an update to your list of extensions you can choose to remove the Yield Analytics Sales Manager Extension by selecting on the Remove link on the extension and following the Installation Instructions process.

## Where can you find Yield Analytics results?

After logging into your DFP account, navigate to the **Sales** tab. Access any of the following screens:

**Catalog** — The results are in the product name column, under each product’s name, with a dedicated forecast request/refresh button. The forecast is controlled by the date-range filter for this screen.

**Proposal Detail** — The results are in the proposal line item name column, under each line item’s name, with a dedicated forecast request/refresh button. All line items can be checked concurrently by utilizing the request/refresh button in the column header. The forecast is controlled by the date-range set up and targeting defined for each line item row in this table.

**Proposal Line-item Detail** — The results are in a dedicated container that appears between the product and line item name, with a Yield Analytics Availability label. The forecast is controlled by targeting and date-range information according to the most recent saved state. If settings are changed, the line item must be saved prior to requesting a new forecast. A dedicated Order Line Contention button is available to understand which line items will be in competition with the one that you have in focus, according to our proprietary understanding of inventory consumption.
