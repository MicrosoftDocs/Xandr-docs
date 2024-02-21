---
title: Integrate with PSP
description: In this article, find information about how to integrate publisher inventory with Prebid Server Premium (PSP).
ms.date: 10/28/2023
---

# Integrate with PSP

Integrating publisher inventory with Prebid Server Premium (PSP) begins with a connection to the publisher's ad server. If a customer uses the Microsoft Monetize Ad Server as their ad server, they are classified as a Microsoft Monetize Ad Server publisher. If a customer is on an external ad server, such as Google Ad Manager, they are considered a direct supply or SSP publisher. See below for guidance for each type of customer.

## Microsoft Monetize ad server customer integration

Monetize Ad Server customers can maintain their current integration type from page/app/server to Microsoft Advertising, then follow the guidance on the pages below:

1. [Add or Edit PSP Global Settings](add-or-edit-psp-global-settings.md).
1. [Add or Edit a Demand Partner](add-or-edit-a-demand-partner.md).
1. [Add, Edit, or Delete a PSP Configuration](add-edit-or-delete-a-psp-configuration.md).

There is an exception for accelerated mobile pages (AMP) inventory. Microsoft Monetize Ad Server Customers must follow the instructions mentioned in the [Integrate Accelerated Mobile Pages with PSP](integrate-accelerated-mobile-pages-with-psp.md) page to integrate their AMP inventory with PSP.

## Direct Supply (SSP) customer integration

SSP customers an integrate with Microsoft Advertising, and in turn, PSP, across the following types of inventory:

- [Integrate Web/Mobile Web with PSP](integrate-web-mobile-web-with-psp.md)
- [Integrate Apps with PSP](integrate-apps-with-psp.md)
- [Integrate Accelerated Mobile Pages with PSP](integrate-accelerated-mobile-pages-with-psp.md)
- [Non-prebid Integrations with PSP](non-prebid-integrations-with-psp.md)
- [Long Form Video Service](../digital-platform-api/long-form-video-service.md)
