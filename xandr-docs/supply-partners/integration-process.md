---
title: Integration Process
description: This article provides information for supply partners to implement OpenRTB integration or migrate from a custom SSP protocol integration.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: supply-partners
ms.author: shsrinivasan
---

# Integration process

This document includes the necessary information for supply partners to review, plan, and execute a new OpenRTB integration, or migrate from a custom SSP protocol integration to [OpenRTB standard](https://www.iab.com/guidelines/real-time-bidding-rtb-project/), in a self-paced fashion.

> [!NOTE]
> The Integration Process page is for external supply partners only.

## Prerequisite checklist

> [!NOTE]
> If you do not already have a customer support portal account, visit the [Login](https://support.ads.microsoft.com) page, proceed as a Guest and request a new user registration.

1. Contact your account manager (or open a ticket with our support team) to confirm the following information:  
    - [Member seat ID](./understanding-the-sell-side-object-hierarchy.md) and if not requested yet, new member seat creation and API login credentials for Xandr's API.
    - [Endpoints for incoming bid requests](./incoming-bid-request-from-ssps.md), and if not requested yet, new endpoint creation on Xandr.
1. Review the documentation outlined below and discuss any open questions:
    - [OpenRTB Specs](./openrtb-specs.md)
    - [FAQ - Integration Process](./faq-integration-process.md)
    - [Object Hierarchy](./understanding-the-sell-side-object-hierarchy.md)
    - [Inventory Mapping](./synchronize-your-inventory-structure.md)
    - [User Sync](./user-id-mapping.md)
    - [Ads.txt/App-Ads.txt](../industry-reference/xandr-support-for-ads-txt-and-app-ads-txt.md)
    - [Deals](./selling-deals-on-xandr.md) (If applicable)

> [!NOTE]
> Prerequisite checks are only complete after the contract is signed and member ID is created. Prior to that, only point `1a.` can be processed. However, until the contract is countersigned, we'd still love to kick off the conversation with your integration team so that you can get familiar with the process and get your technical questions addressed right away!

- Engagement is expected to take 3-4 weeks.
- The client must fully review the Prerequisite Checklist (this document) - and gather all the information prior to following the steps below.

## Step 1: Self-guided API/UI training and creation of publisher and placement objects (estimated time: 7 - 10 days)

1.  Review Xandr [Object Hierarchy](./understanding-the-sell-side-object-hierarchy.md) and API/UI
  documentation.
2. Provision the objects that you will need for initial testing, either via  or the [API](../digital-platform-api/api-getting-started.md). See [API Documentation](./api-documentation.md) for more details.
3. Create sell-side objects to synchronize inventories (at least the ones are needed for initial functional testing) via UI/API
   - Review Xandr Object Hierarchy: Member → Publisher → Placement Group → Placement
   - Create a publisher and a placement for the test
     - Within each object, the code value must be populated with the external identifier the SSP will pass in the [bid request](./incoming-bid-request-from-ssps.md).
   - Related API documentation
     - [Member Service](../digital-platform-api/member-service.md)
     - [Publisher Service](../digital-platform-api/publisher-service.md)
     - [Placement Group Service (Site Service)](../digital-platform-api/site-service.md)
     - [Placement Service](../digital-platform-api/placement-service.md)
1. Setup a Default placement on the publisher and member level. (in case we cannot identify inventory from the bid request, the impression will be logged into that default placement.)
1. Use the `code` field to map your bid requests to your publishers and placements. For more details and examples, read the [Integration FAQ](./faq-integration-process.md).  

   > [!NOTE]
   > In order to provide transparency to our buyers and improve our optimization, we require our partners to break out their inventory by publisher. For more information regarding our inventory structure standards please visit our wiki page [Use the API to Synchronize Your Inventory Structure](./use-the-api-to-synchronize-your-inventory-structure.md).
  
1. Use the [Publisher Service](../digital-platform-api/publisher-service.md) to create publishers that are mapped to your inventory.

   > [!NOTE]
   >
   > - The `code` field is required for all external sellers at both the publisher and placement levels and is highly recommended for all other sellers to ensure that your inventory is as granular as possible so
   > that it can be investigated accurately for quality issues, and specifically for domain detectability. This step will help you to split your inventory into highly detectable and less detectable tags, allowing you to isolate the impacts of non-detectable domains on the rest of your inventory's viability.
   > - In order to create or edit publishers in  or the [API](../digital-platform-api/api-getting-started.md), you have to declare the [Inventory Relationship](./inventory-relationship-faq.md). The requested information is basic business information about how the inventory is accessed and will be used to support Xandr's inventory quality efforts. For a complete list of fields and their usage requirements, refer to the [Publisher Service](../digital-platform-api/publisher-service.md) documentation.

1. User Sync Setup
   <br>Store the user mapping table between Xandr's and yours by using the getUID service. Learn details from [User ID Mapping](./user-id-mapping.md).

## Step 2: OpenRTB bid request endpoint testing (estimated time: 3 - 4 days)

Xandr supports the [OpenRTB 2.4 protocol](https://www.iab.com/wp-content/uploads/2016/03/OpenRTB-API-Specification-Version-2-4-FINAL.pdf)for receiving all media type impressions. Follow the OpenRTB 2.4 specification from [IAB](https://www.iab.com/guidelines/real-time-bidding-rtb-project/).

Use the endpoints below to send server-to-server OpenRTB bid requests to Xandr:

- `http://MEMBER_ALIAS-useast..com/openrtb2member_id=MEMBER_ID&test=1`
- `http://MEMBER_ALIAS-uswest..com/openrtb2member_id=MEMBER_ID&test=1`
- `http://MEMBER_ALIAS-emea..com/openrtb2?member_id=MEMBER_ID&test=1`
- `http://MEMBER_ALIAS-apac..com/openrtb2?member_id=MEMBER_ID&test=1`

> [!NOTE]
> `MEMBER_ID` and `MEMBER_ALIAS` should be substituted with your individual partner member ID and alias.

Feel free to use the bid request examples from the page Incoming Bid Request from SSPs and adjust the code fields accordingly to match your publisher and placement inventory mapping.

You must use the `"test=1"` query string parameter on your calls to identify a test impression. It will not be logged in reporting.

## Step 3: Manual tests

1. Provide a bid request sample to Xandr.
1. Setup a **test** placement on Xandr platform and make sure the inventory is mapped correctly.
1. Provide a sample creative that meets all the requirements of the test placement.
1. Setup Ad Quality rule that only allows Xandr Test Buyer to buy Impressions on the Test Placement.
1. Remove `"&test=1"` from the endpoint query string when the test starts.
  
   > [!NOTE]
   > If you do not remove `"&test=1"`, imps will **not** be logged on Xandr side.

1. Fire the traffic manually from the test placement to confirm the receipt of a bid response, the creative served, and impressions logged on your side.
1. Xandr will run a delivery test from a dedicated buy-side member seat and notify you of any discrepancies before scaling your inventory further.
1. Xandr will validate your OpenRTB bid requests and notify you in case the format needs to be corrected.  

## Step 4: Programmatic functional test (live traffic)

1. Open up a small but substantial portion of traffic to Xandr on the established **endpoint** (at a minimum of several thousand imps per day).
   Xandr will confirm the volume of traffic being sent in and verify that impressions are flowing in through our reporting and they align with your internal reporting.
1. Run the test for a day or so and compare numbers to ensure the discrepancy between your reporting and Xandr reporting is acceptable.

## Step 5: Go live

1. Map all your inventories on Xandr platform before going live with 100% traffic.
1. After finishing the inventory mapping, ramp up traffic and remove filters that may be imposed during testing such as country pre-targeting, device pre-targeting and bid volume throttling.

## Step 6: Completion/Follow up (estimated time: 2 - 3 days)

We encourage a gradual traffic ramp-up where distinct portions of your inventory are being sent to Xandr. General recommendation is to start with a small chunk of traffic (100-200 QPS).

Notify your Xandr contact about the completion of the self-paced integration/migration; your contact will initiate the final OpenRTB requirement validation tests and provide you with final results and feedback.
