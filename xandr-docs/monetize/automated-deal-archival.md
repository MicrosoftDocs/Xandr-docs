---
title: Microsoft Monetize - Automated Deal Archival  
description: Automatic deal archival in Microsoft Monetize ensures auctions are running efficiently on the Microsoft Advertising platform.
ms.date: 07/28/2025
ms.author: shsrinivasan
---

# Microsoft Monetize - Automated Deal Archival 

> [!NOTE]
> This feature is currently in pilot and may change without notice. A notification appears in the UI when the feature is enabled for an account. For more information, contact your Microsoft Advertising account representative. 

## Overview
Automatic deal archival ensures auctions are running efficiently on the Microsoft Advertising platform. The platform archives deals that buyers have not been using for an extended period of time. Archived deals remain visible in monitoring tools and reports but do not participate in auctions or generate bid requests. This page outlines the archival criteria and provides guidance on how to monitor and manage archived deals. 

## Deal lifecycle  

A deal progresses through several stages during its lifecycle. The table below describes deal behavior at each stage and outlines the available actions:

| **Stage** | **Auctions** | **Monitoring (UI)** | **Reporting** |
|---|---|---|---|
| Active deal | Generates bid requests | Available to view and edit | Included |
| Inactive deal | Does not generate bid requests | Available to view and edit | Included |
| Archived deal | Does not generate bid requests | Available to view and edit | Included |
| Deleted deal | Does not generate bid requests | Not available to view or edit | Included |

## Deal archival policy  
 
The Microsoft Advertising platform automatically archives deals by default that are over a year old and have had no spend in the past 12 months. The system evaluates deals daily against this criteria. Archiving is automatic, but the platform does not delete deals.


## Monitoring archived deals  

You can view archived deals in the Deals Monitoring screen, but they don’t appear by default. For more information on navigating the monitoring screen, see  [Create a Custom Deal](create-a-custom-deal.md) or [Microsoft Monetize - Monitor Line Items](monitor-line-items.md)
To view archived deals: 
- Select the Advanced Filters button, then choose Show Archived Deals and select Apply. The monitoring screen updates to display only archived deals. 
- To view the archived date for a deal, select the Modify Columns button and select the Last Archived Date column option. To see recently archived deals, click the column header to sort the monitoring screen. 
> [!NOTE]
> Archived deals continue to be included in reporting.  

## Managing archived deals  

You can archive deals by selecting the deals in the monitoring screen and clicking the Archive button in the action bar at the top. For more information on how to navigate to the monitoring screen, see  [Create a Custom Deal](create-a-custom-deal.md) or [Microsoft Monetize - Monitor Line Items](monitor-line-items.md)
 
To ensure a deal’s lifecycle on the Microsoft Advertising platform aligns with lifecycles used by DSPs, an archived deal cannot be unarchived. However, you can easily create a new deal with the same settings by selecting the archived deal and choosing either the Use as Template or Duplicate options. 

 

## Related topics
- [Create a Custom Deal](create-a-custom-deal.md) 
- [Microsoft Monetize - Monitor Line Items](monitor-line-items.md)
