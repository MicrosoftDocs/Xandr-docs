---
title: Trade Desk Buying Guide
description: This page is an overview about Trade Desk Buying Guide to help Xandr publishers communicate with their buyers. This page provides a step-by-step guide to create Deal workflow and Programmatic guaranteed (PG) workflow. Additionally, information on Deal troubleshooting tips & FAQs is given.  
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Trade desk buying guide

## Overview

Xandr, in partnership with Trade Desk, has created this buying guide to help Xandr publishers communicate with their buyers about accessing and targeting Xandr's publisher inventory using Trade Desk as their DSP. The information has been created in collaboration with and approved by the Trade Desk team. Note that platforms can and will change regularly, and as always with our documentation we will do our best to update this guide as needed. We recommend that if buyers are having issues or need help with using the Trade Desk platform their first point of outreach should be the Trade Desk team.

## Key definitions

| Terminology | Definitions |
|:-|:-|
| Ad Group | Belongs to a campaign, which belongs to an advertiser. This is where buyers start constructing the details and targeting for the strategy they are running. |
| Campaign | - Strategy for purchasing advertising inventory that is organized around a theme, product, or brand.<br>- Run for a set period of time (flight) and are given individual budgets with which to purchase inventory.<br>- The Campaign level is located under an Advertiser and above its corresponding Ad Groups. |
| Inventory Contracts | - First-Party Inventory Contracts: Established by a partner of The Trade Desk. Buyer contacts their account manager for assistance creating a first-party contract.<br>- Third-Party Inventory Contracts: Managed by The Trade Desk and available for all partners to use (“always-on” deals). |
| Programmatic Guaranteed (PG) | - A publisher reserves inventory for the buyer, and in turn, the buyer commits a certain amount of spend to the publisher.<br>- Fixed CPM<br>- The Trade Desk bids at a rate of ~96%+ and should win all the bids it presents.<br>- The supply-side partner (SSP)/publisher is expected to be able to pace the deal ID evenly over the course of the specified flight. |
| Publisher Management Platform (PMP) | - Displays the essential information about buyers’ private contracts.<br>- Navigate to the PMP dashboard by clicking **Libraries** in the platform header and selecting **Publisher Management Platform (PMP)**. |

## Trade desk’s deal workflow

:::image type="content" source="media/trade-desk-buying-guide-fig-a.png" alt-text="Screenshot of Trade Desk’s Deal workflow.":::

## Easy proposal activation - For GAM, Magnite, Freewheel, Bidswitch

:::image type="content" source="media/trade-desk-buying-guide-fig-b.png" alt-text="Screenshot of easy proposal activation for GAM, Magnite, Freewheel and Bidswitch.":::

## Deal workflow

### Step 1: Set up a campaign

Initiate the setting up of a campaign by clicking **+CAMPAIGN** button and enter the **Campaign Name**.

:::image type="content" source="media/trade-desk-buying-guide-fig-c.png" alt-text="Screenshot of setting up a campaign.":::

### Step 2: Upload a creative

1. Upload hosted and third party creatives within the **Add Creative** wizard in the **Basic Information** page. Creatives for all media types are uploaded here. Note that native creatives must be hosted to proceed further. Below screenshots depicts the uploading of a hosted display creative.

   :::image type="content" source="media/trade-desk-buying-guide-fig-d.png" alt-text="Screenshot of uploading a creative.":::

1. Next, in the **Details** page, enter the **Name** and the **Landing Page URL** for your creative.

   :::image type="content" source="media/trade-desk-buying-guide-fig-e.png" alt-text="Screenshot of entering the Landing Page URL.":::
  
1. Next, in **Tracking and Declarations** page, enter the necessary details as per of your requirements.
  
   > [!NOTE]
   > The **Clickthrough URL** field is mandatory in this page.

   :::image type="content" source="media/trade-desk-buying-guide-fig-f.png" alt-text="Screenshot of Tracking and Declarations page.":::

1. Next, in **Flight Dates** page, enter the start and end date of the creative flight along with the Time Zone.

   :::image type="content" source="media/trade-desk-buying-guide-fig-g.png" alt-text="Screenshot of Flight Dates page entering start and end date of the creative flight along with the Time Zone.":::
  
1. Next, in the Summary page, review the information entered and confirm the details.

### Step 3: Upload a deal to the trade desk platform via PMP

1. Click **Inventory Contract** to open the Inventory Contract Wizard. In **Description** page, enter the **Name** of the contract. Other details in the page is optional.

   :::image type="content" source="media/trade-desk-buying-guide-fig-h.png" alt-text="Screenshot of Uploading a deal to the Trade Desk platform via PMP.":::
  
1. In **Supply Vendor Deals** page, select the **Supply Vendor** and enter **Deal Code/ID** as well as CPM.

   :::image type="content" source="media/trade-desk-buying-guide-fig-i.png" alt-text="Screenshot of Supply Vendor Deals page to select Supply Vendor and enter Deal Code/ID.":::
  
1. In **Publishers page**, add the **Publisher Name** associated with the **Deal ID** and click **Next**.

   :::image type="content" source="media/trade-desk-buying-guide-fig-j.png" alt-text="Screenshot of Publishers page.":::
  
1. In **Category Targeting**, **Site Targeting** and **Location Targeting** pages, specify applicable category(s), site(s), and location(s) that you want to target and click **Next**.

   :::image type="content" source="media/trade-desk-buying-guide-fig-k.png" alt-text="Screenshot of  Category Targeting, Site Targeting and Location Targeting pages.":::

1. In **Creative Targeting** page, select the applicable Ad Sizes and click **Complete**. Once you click **Complete**, you will only see available impressions for the deal as long as the deal is activated in the SSP.

   :::image type="content" source="media/trade-desk-buying-guide-fig-l.png" alt-text="Screenshot of Creative Targeting page.":::
  
### Step 4: Create an real time bidding (RTB) Ad group

1. Click the **+Ad Group** button and enter a name to your Ad Group. It is recommended to choose a unique name which differs from your other Ad Groups. Select the **Media Types**, **Device Types**, **Ad Environments** and specify the **Goal** and **Target** in the page. Click **Next**.

   :::image type="content" source="media/trade-desk-buying-guide-fig-m.png" alt-text="Screenshot of clicking the +Ad Group button and entering a name to your Ad Group.":::

1. Select your **Pacing** and **Flight Dates** and specify your budget for the flights. Enter the amount for your **Base bid** and **Max bid** and click **Next**.

   :::image type="content" source="media/trade-desk-buying-guide-fig-n.png" alt-text="Screenshot of selecting your Pacing and Flight Dates and specifying your budget for the flights.":::

1. Select your **Audience Type**, **Frequency**, and **Geos** for targeting. Next, enable **Cross-Device** targeting and attribution.

   :::image type="content" source="media/trade-desk-buying-guide-fig-o.png" alt-text="Screenshot of selecting your Audience Type, Frequency, and Geos for targeting.":::
  
1. Complete your Ad Group creation set up by selecting **Creatives** from drop-down, adding **Sites/App** lists using **ADD LIST** button, and selecting the **Market type** under the **Private Contract** section that you uploaded previously.

   :::image type="content" source="media/trade-desk-buying-guide-fig-p.png" alt-text="Screenshot of selecting the Market type under the Private Contract section.":::

    > [!NOTE]
    > Below is the list of targeting options available when creating an Ad Group:
    >
    > - Language
    > - Site and SSP
    > - Device Types
    > - Browser/OS
    > - Time and Day of Week
    > - Video Size and Quality
    > - Device Make and Model
    > - Ad Format and Ad Size
    > - Viewability/Fold
    > - Geography/ Latitude & Longitude
    > - Frequency
    > - Mobile Carrier

### Step 5: Target and launch the deal

Find the deal by searching by deal ID or deal name. Once fetched, target the deal ID within the **Private Contract** rail at the Ad Group level. Note that, it is possible to target more than one private contract in a single Ad Group. Once the deal is trafficked in the SSP, your Ad Group will automatically start spending according to the requirements.

:::image type="content" source="media/trade-desk-buying-guide-fig-q.png" alt-text="Screenshot of Targeting and Launching the Deal.":::
  
## Programmatic guaranteed (PG) workflow

:::image type="content" source="media/trade-desk-buying-guide-fig-r.png" alt-text="Screenshot of Programatic Guaranteed (PG) Workflow.":::

## Tips and tricks for PG workflow

- For PG deals with **GAM**, **Magnite**, **Freewheel**, or **Bidswitch**, the client will utilize the Easy Proposal Activation workflow described above.
- If the SSP is not **GAM**, **Magnite**, **Freewheel**, or **Bidswitch**, the publisher will provide the client with the targetable deal ID so the client can create the PG contract in The Trade Desk platform.

 > [!NOTE]
 > A few best practices for clients:
 >
 > - Make sure to leverage the The Trade Desk’s PG workflow on the platform.
 > - Ensure that there are no daily spend caps on the Ad Group or Campaign level.
 > - Confirm that the Ad Groups are in active state.
 > - Make sure that the agreed ad sizes are trafficked at the Ad Group level.
 > - Make it certain that all parties are aligned on the budget. Ensure that the client’s creative meets the specs outline by the publisher and that the creative is uploaded 24-48 hours before the launch date.

## Deal troubleshooting tips & FAQs

### First party 1:1 deal troubleshooting guide

:::image type="content" source="media/trade-desk-buying-guide-fig-s.png" alt-text="Screenshot of  Deal Troubleshooting Guide.":::

### The trade desk troubleshooting tool

Go into the **Private Contract** rail in your Ad Group and click **Troubleshoot** to see the **ISSUE**, **DETAILS**, **POTENTIAL SOLUTION**, and **EXCLUDED PERCENTAGE** of bids for a specific contract.

:::image type="content" source="media/trade-desk-buying-guide-fig-t.png" alt-text="Screenshot of Private Contract rail in your Ad Group where you click Troubleshoot.":::

:::image type="content" source="media/trade-desk-buying-guide-fig-u.png" alt-text="Screenshot to see the ISSUE, DETAILS, POTENTIAL SOLUTION, and EXCLUDED PERCENTAGE of bids for a specific contract.":::

The **Bid Exclusions Reasons** dialog would appear. You can

|  |  |
|--|--|
| Contract Dropdown | Switch between contracts assigned to your Ad Group by selecting a different name from this dropdown. Select All Contracts to see reasons across all deals in your Ad Group. |
| Deal | Select a specific deal for the contract in question or choose **All** to see issues from all deals associated with the contract. |
| Date | Select a date range to filter issues. |
| View Contract Details | Click this link to be taken to the Settings page for the contract in question. |
| Percentage Indicator | Use this bar to compare the percentage of bids excluded to the percentage of bid served. |

### Common reasons for bid exclusions and their troubleshooting

| Common Reason for Bid Exclusion | The Trade Desk Definition | The Trade Desk Suggestion |
|--|--|--|
| Creative Not Eligible | An issue with the creative’s approval status, attributes, or settings prevented a bid response from being served. | Check if the creative is being blocked on the publisher’s end due to category or block advertiser restrictions. Have the publisher check with the supply vendor that the creative ID isn’t being excluded from the auction and has been approved by the supply vendor. Confirm that the necessary media types are included in the creative. |
| No Creatives of Correct Type Found | The Ad Group has no creatives of the correct type (display, video, native, audio) matching the bid request. | Ensure the creatives assigned to your Ad Group match the creative types coming through the contract details. For example, if you have video creatives assigned to your Ad Group, confirm that video inventory is coming through the deal and if the publisher accepts VAST or VPAID. |
| No Matching Ad Format Found | The Ad Group does not have a creative assigned with an ad format matching the bid request. | Make sure that all creatives assigned to your Ad Group match the creative sizes coming through the contract details. For example, if the publisher is sending 970x250 and 728x90 desktop display inventory, ensure that you have 970x250 and 728x90 creatives assigned to your Ad Group. |
| Referrer Data Missing | A pre-bid solution such as DoubleVerify, IAS or Peer39 blocked the request. | Consider loosening or lifting pre-bid solutions as they may be restricting the number of requests. |
| User Doesn’t Match Audience Targeting | The Ad Group is targeting an audience and there was no match found with the bid request. | Confirm with the publisher the avails for the audience in which you’re targeting. Consider expanding the audience targeting so scale is not limited. |

### Common questions asked while troubleshooting

| Questions | Response |
|--|--|
| Is the advertiser’s audience targeting too specific and therefore restricting bidding? | Remaining Addressable Market (RAM) shows how many imps are available to bid on after the Ad Group’s targets and rails have been applied. The lower the score, the more restrictive; the higher the score, the less restrictive. Common Targeting Parameters: Audience, Geo, Brand Safety & Measurement, Device. |
| Did the publisher increase the deal floor and you are now bidding below the floor? | Confirm the floor price listed in the deal. |
| Did the publisher shift the inventory to a different SSP? | Check if you are seeing avails come through the deal. If it’s a First Party 1:1 deal, reach out to the publisher directly; if it’s a Third Party PMP Library deal, reach out to your Account Manager. |
| Is there an issue if avails, and winning bids, are coming through a Third Party PMP Library deal ID but there’s not much spend? | Our buyers are self-service and will make the decision as to when/if they activate their campaigns against certain supply types.<br>We encourage the publishers’ sales team to share the deal private contract links with any clients you are contacting. The link will drive buyers with logins to our platform closer to the point of spend activation on the Third Party PMP Library deals. Please note that you will not be able to view the links, but our clients should have access.<br>You may see more adoption in client First Party 1:1 deals after setting up Third Party PMP Library deals. The 1:1 deals will likely drive more revenue, but we see value in the PMP Library deals since they allow newer and smaller agencies to access your inventory. |

> [!NOTE]
> The above troubleshooting steps are general in nature. Your Account Manager and The Trade Desk Knowledge Portal are the best resources for assistance with PMP deals and the Trade Desk platform.
