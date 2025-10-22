---
title: Xandr Bidder Release Notes
description: Explore the product releases, updates, and deprecations, with a listed table that accommodates potential date shifts.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Xandr Bidder Release Notes

The following table lists Xandr product releases, updates, and deprecations. Dates may shift if necessary.  

| Release Date | Status | Feature | Product Theme | More Info |
|--|--|--|--|--|
| 2022-04-21 | Upcoming | Effective June 20, 2022, the Impression Bus API (along with the Digital Platform API) will only permit HTTPS (secured and encrypted) connections. After that date, **HTTP (unsecured and unencrypted) connections will not be accepted and will fail**. You must ensure that you are not using unsecured and unencrypted HTTP across your organization | Security | - [Breaking Change Notice - April 21, 2022 - HTTPS Required](breaking-changes.md) |
| 2022-01-27 | Released | Xandr has released support for OMID in Native 1.2 according to the [OpenRTB OM SDK Spec](https://github.com/InteractiveAdvertisingBureau/AdCOM/blob/main/OpenRTB%20support%20for%20OMSDK.md). Xandr now supports OMID for video, display, and Native 1.2 | OpenRTB, Native, Mobile | - [Outgoing Bid Request to Bidders](outgoing-bid-request-to-bidders.md) |
| 2021-11-04 | Released | Xandr has added support for video.linearity within the video object of bid requests in accordance with the OpenRTB specification.<br> - 1: Linear / In-Stream<br> - 2: Non-Linear / Overlay | OpenRTB | - [Outgoing Bid Request to Bidders#VideoObject](outgoing-bid-request-to-bidders.md#outgoing-bid-request-to-bidders) |
| 2021-10-14 | Released | Xandr now supports inventorypartnerdomain in ext objects of app and sit in accordance iab ads.txt specification 1.0.3<br> - App.ext.inventorypartnerdomain<br> - Site.ext.inventorypartnerdomain | OpenRTB | Iab spec including inventorypartnerdomain update: [https://iabtechlab.com/wp-content/uploads/2021/03/ads.txt-1.0.3.pdf](https://iabtechlab.com/wp-content/uploads/2021/03/ads.txt-1.0.3.pdf) |
| 2021-08-02 | Released | Native 1.2 - Viewability Measurement  <br>**What's changing**<br>On native 1.2 bid requests:<br> - The **ver** field is set to "1.2"<br> - The **eventtrackers** object will be included in bid requests, including fields **event** and **methods**<br>&nbsp; - event types 1-4  are supported<br> &nbsp; - methods 1 - "img" and 2 - "js" are supported<br>On the bid response:<br> - The **ver** field should be set to "1.2"<br> - For v1.2 responses: The **eventtrackers** object is supported, including fields **event**, **method**, and **url**<br>event types 1-4  are supported<br> - The **imptrackers** and **jstracker** fields are still supported, but we recommend using **eventtrackers** instead. These fields will be deprecated in future versions. | OpenRTB, Native | &nbsp; - [Outgoing Bid Request to Bidders](outgoing-bid-request-to-bidders.md)<br>&nbsp; - We support for Version 1.1 and 1.2 of the OpenRTB Native Ads API. Once your bidder has been enabled for Native 1.2, you will begin to receive version 1.2 bid requests and will be required to provide version 1.2 bid responses. Native v1.2 is available regardless of whether your bidder is enabled for [Native Ad Markup Bidding](native-ad-markup-bidding.md). |
| 021-06-17 | Released | The **video.mimes** array of the OpenRTB bid request from Xandr will no longer include the following values:<br> - application/x-shockwave-flash<br> - video/x-flv | OpenRTB |  |
| 2021-02-18 | Released | Synthetic CTV Device IDs | OpenRTB | - [Outgoing Bid Request to Bidders](outgoing-bid-request-to-bidders.md) |
| 2019-09-24 | Released | **Rebranded and Updated Bidder User Interface** | User Interface | - [Xandr Bidder UI](https://bidder.xandr.com/login)<br> - [Bidder Platform User Interface](bidder-platform-user-interface.md) |
| 2019-09-03 | Released | **Support Supplychain Fields in OpenRTB Bid Requests** | OpenRTB | - [IAB Supplychain Object Specs](https://github.com/InteractiveAdvertisingBureau/openrtb/blob/master/supplychainobject.md)<br> - [Outgoing Bid Request to Bidders](outgoing-bid-request-to-bidders.md) |
| 2019-03-21 | Released | **Support IFA Fields for CTV Impressions in OpenRTB Bid Requests** | OpenRTB, CTV | -  [IAB IFA OTT Guidelines](https://iabtechlab.com/wp-content/uploads/2018/12/OTT-IFA-guidelines.final_Dec2018.pdf)<br> - [Outgoing Bid Request to Bidders](outgoing-bid-request-to-bidders.md) |
| 2018-12-01 | Released | **Deprecate Xandr Bidding Protocol and Legacy OpenRTB** | OpenRTB | - [Bidding Protocol](bidding-protocol.md) |
| 2018-11-01 | Released | **Deprecate Bid Shading and Spend Protection Fields in OpenRTB Bid Requests** | OpenRTB | - [PublisherIntegrationObject](outgoing-bid-request-to-bidders.md)<br> - [BidRequestAppNexusObject](outgoing-bid-request-to-bidders.md) |
| 2018-10-29 | Released | **Native Ad Markup Bidding (Beta)** | Native, Creative, OpenRTB | - [Native Ad Markup Bidding](native-ad-markup-bidding.md) |
| 2018-09-24 | Released | **Support Video Placement Field in OpenRTB Bid Requests** | OpenRTB | - [VideoObject](outgoing-bid-request-to-bidders.md) |
| 2018-06-07 | Released | **New Google Ad Manager Bid Errors** | Creative, Troubleshooting | - [Bid Error Codes](bid-error-codes.md)<br> - [Bidder Bid Error Report API](bidder-bid-error-report-api.md)<br> - [Notify Request](notify-request.md) |
| 2018-04-30 | Released | **Expired Creative Inactivity Period Decreased** | Creative | - [Add a Creative](add-a-creative.md)<br> - [Creative - FAQ](creative---faq.md)<br> - [Object Limit Service](object-limit-service.md) |
| 2018-03-22 | Released | **Creative Unexpiration** | Creative |  |
| 2018-02-13 | Released | **Supply Type Detection** | Mobile, Targeting | - [Supply Type Detection - FAQ](supply-type-detection---faq.md) |
| 2018-02-08 | Released | **WiFi Carrier Renamed** | Mobile, Targeting | - [Carrier Service](carrier-service.md)<br> - [OpenRTB Bid Request](outgoing-bid-request-to-bidders.md) |
| 2018-02-06 | Released | **Split Bid Error 102 into Two Errors**<br>We are splitting bid error code 102 "Creative id was not found or inactive" into two errors. The new errors are:<br>Error 102: "Creative id was not found"<br>Error 137: "Creative id is inactive" | Creative, Reporting, Troubleshooting | - [Bid Error Codes](bid-error-codes.md) |
| 2017-11-06 | Released | **API Version 1.18 Release - Breaking Change** | Reporting, API | - [API Version 1.18 Breaking Change Communication](september-5--2017---api-version-1-18-release---breaking-changes.md) |
| 2017-10-13 | Released | **Support Privacy Link in OpenRTB Native** | Creative, OpenRTB | - [Creative Service](creative-service.md) |
| 2017-09-25 | Released | **Update Bcat Behavior to Include Brand Override** | OpenRTB |  |
| 2017-09-18 | Released | **Update device.os Field in OpenRTB** | OpenRTB | - [DeviceObject](outgoing-bid-request-to-bidders.md#outgoing-bid-request-to-bidders) |
| 2017-07-31 | Released | **Support ipv6 in OpenRTB Bid Request to Bidders** | OpenRTB | - [DeviceObject](outgoing-bid-request-to-bidders.md#outgoing-bid-request-to-bidders) |
| 2017-07-27 | Released | **Change in Bcat and Battr Behavior** | OpenRTB |  |
| 2017-07-27 | Released | **Remove Xandr Categories from OpenRTB Bid Requests** | OpenRTB |  |
| 2017-05-31 | Released | **Change in Click URL Behavior** | OpenRTB |  |
| 2017-05-15 | Released | **New Quick Start Buying Guide** | Documentation | - [Quick Start Creative Buying Guide](quick-start-creative-buying-guide.md) |
| 2017-05-11 | Released | **Support Multiple Media Types in a Single Bid Request from AST Supply** | OpenRTB |  |
| 2017-02-21 | Released | **Banner Sizes Extension Deprecated** | OpenRTB | - [Outgoing Bid Request to Bidders](outgoing-bid-request-to-bidders.md) |
| 2017-02-09 | Released | **Native 1.0 Bid Requests Deprecated** | OpenRTB | - [Outgoing Bid Request to Bidders](xandr-bidder-release-notes.md) |
