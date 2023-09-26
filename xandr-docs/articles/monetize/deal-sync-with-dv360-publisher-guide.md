---
Title : Deal Sync with DV360 - Publisher Guide
Description : Note: This feature is in **Closed
Beta**. It is only available to select clients. Please consult your
---


# Deal Sync with DV360 - Publisher Guide







Note: This feature is in **Closed
Beta**. It is only available to select clients. Please consult your
Account Manager if you'd like to be added to the beta test.







## Overview

Xandr's integration with the Display Video 360
(DV360) Seller API automatically synchronizes the deals created in
Microsoft Monetize with the Google DV360 system.
This enables a more seamless deal transaction between
Microsoft Monetize publishers and DV360 buyers.





Important: You can manually set up
deals with DV360, but this requires buyers to manually register
publisher deals in the DV360 user interface. (Details of the manual
process can be found in <a
href="https://docs.xandr.com/bundle/xandr-bidders/page/dv360-buying-guide.html"
class="xref" target="_blank">DV360 Buying Guide</a>.) The manual process
of setting up deals can result in delays and issues due to human error.





The key benefits of using an automatic synchronization process are:

- Seamless deal set up process with DV360 buyers.
- Elimination of requirement for buyers to manually register deals in
  the DV360 UI.
- Automatic deal synchronization of deals and deal updates from
  Microsoft Monetize to DV360 (with some
  restrictions, which are explained below).





## Process

**New Deal Creation**

New seat ID deals created in the Microsoft Monetize
UI automatically get uploaded to DV360 systems for buyer acceptance, as
shown here:

<div id="ID-00007677__p-80cb9dc2-41f7-4ff9-95cb-0fb6376b3276" >

  

<div class="imagecenter">

<img src="../images/dv360/P1.png"
id="ID-00007677__image-8b2f83a5-c417-4294-974d-8beb38ee6696"
class="image imagecenter" />



  



**Deal Update**

Updates to newly created deals (post deal sync enablement) automatically
get uploaded to DV360 systems for buyer acceptance:

<div id="ID-00007677__p-54e23713-55cc-4929-9c4c-f9f253ee3eec" >

  

<div class="imagecenter">

<img src="../images/dv360/P2.png"
id="ID-00007677__image-722ad74a-9cb9-4828-9d88-81884ab1524e"
class="image imagecenter" />



  



**Frequency of Deal Sync**



- We synchronize deals every hour.
- New deals are uploaded up to 1 hour after being created.
- Updates to existing deals are uploaded up to 1 hour after it is
  created (depending on when the last sync script ran).
- Buyer acceptance statuses are synchronized every hour.







## What Is Changing

While there are no changes to how a publisher create deals in
Microsoft Monetize UI, publishers should be aware of
which type of deals are automatically synchronized and which deals still
continue to follow the manual workflow.



- All new deals created in the alpha are synchronized with DV360, with
  the exceptions of:
  - Multi-Buyer Deals that are created at the Bidder level.
  - Deals created with a DV360 Buyer Member ID instead of a Bidder Seat
    ID DV360 Partner ID.
- In a later phase, we plan to begin synchronizing older deals that
  match the above criteria.







## Best Practices For Deal Set Up

**1:1 Deals and Exchange Curated Deals (ECDs)**



- Deals must be set up with DV360 partner IDs. This deal synchronizing
  process does not support member ID deals.
- Once a partner ID is selected for a deal, it cannot be changed in
  subsequent updates.
- Always have active communication with the buyer during the deal
  negotiation and setup process to ensure the buyer knows to approve the
  deal in the DV360 UI.



**Programmatic Guaranteed (PG) Deals**



- Deals must be set up with DV360 partner IDs. This deal sync process
  does not support member ID deals.
- You cannot change the DV360 partner ID once the deal is created.
- The deal must have only **ONE** declared media type (video, banner,
  native, audio).
- Always have active communication with the buyer during the deal
  negotiation and setup process to ensure the buyer knows to approve the
  deal in the DV360 UI.
- Only update deal details when necessary and **always** notify the
  buyer to approve the changes. The DV360 buyer continues to bid using
  previous PG deal details until new deal updates are approved.
- PG deals must include allowed creative sizes for banner and display .



**Multi-Buyer Deals**



- Deals set up with multiple DV360 seat IDs automatically get
  synchronized.

- Bidder level deals (set up with ALL DV360 buyers) are not supported in
  automatic deal synchronizing.

- The buyer that accepts a Multi-Buyer Deal in the DV360 UI must have
  access to accounts for **all** seat IDs included in the deal. If that
  is not possible, the buyer should reach out to Google support to
  accept the deal.

- Once a DV360 seat ID is added to a deal, it cannot be removed.








