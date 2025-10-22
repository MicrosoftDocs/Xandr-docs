---
title: Changelog for Buyer Seat ID
description: This page explains Legacy Member ID Integration Behavior and Buyer Seat ID Integration Behavior in tabular form.  
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Changelog for buyer seat ID

This documents all of the changes between member id integration and buyer seat id integration.

## Changes in Bidder integration

| Category | Legacy Member ID Integration Behavior | Buyer Seat ID Integration Behavior | More Information |
|--|--|--|--|
| Bidder Object | Existing Settings Managed in bidder Object:<br>-21+ fields that manage bidder settings | Additional New Fields added:<br>- max_seats<br>- default_member_id | [Bidder Service](./bidder-service.md) |
| Creative Registration | Creatives must be uploaded to the Xandr Member ID that will be used to bid with the creative | All creatives can be registered with the bidder's default_member_id set on the bidder object<br>Any bidder seat can bid using creatives registered with the default member id.<br>Existing creatives will continue to be associated with the member ids. | [Creative Service](./creative-service.md) |
| Seat Object | Not applicable to member id integration | New API Service created to register bidder seat ids into Xandr Systems | [Seat Service](./seat-service.md) |
| Reporting | All Bidder reports can break out a bidder spend by the member ID entity. This includes transaction reporting as well as bid error reporting | Bidders can access reporting on a buyer member id level and buyer seat id level | [Bidder UI](./bidder-platform-user-interface.md) <br><br> [Report Screen](./reporting-screen.md)<br><br>[Report Service](./report-service.md) |
| Bid Request | Eligible buyers for an impression are indicated in the request.wseat field of the bid request<br>deal.wseat field will include the Xandr member ID eligible to bid on the deal | request.wseat field will not be included in the bid request<br>deal.wseat field will include the Xandr member ID on legacy deals<br>deal.wseat field will include the buyer seat id on new seat id deals | [Outgoing Bid Request to Bidders](outgoing-bid-request-to-bidders.md) |
| Bid Response | seatbid.seat field should include the Xandr member id bidding on the impression | seatbid.seat field should include the buyer seat id | [Incoming Bid Response from Bidders](incoming-bid-response-from-bidders.md) |
| Deals | Xandr publishers can set up deals with bidder buyer members | Xandr publishers can set up deals with bidder buyer seats | [Deal Buyer Access Service](./deal-buyer-access-service.md) |
| Virtual Marketplace <br> - Transparency Feed | Bidder requests a new member id for virtual marketplace buyer and set up user access for data from this member. | Bidder shares seat ID(s) to be used by virtual marketplace buyers. Xandr will create member IDs that will correspond to these seats and set up mappings. | N/A |
