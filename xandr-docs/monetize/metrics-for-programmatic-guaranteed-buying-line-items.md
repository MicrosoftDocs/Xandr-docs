---
title: Microsoft Monetize - Metrics for PG Buying Line Items
description: Learn analyzing the line item's performance in bidding and delivering toward a targeted PG deal using Programmatic guaranteed (PG) buying line items. This page covers PG buying line item metrics and their descriptions. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Metrics for PG buying line items

Programmatic guaranteed (PG) buying line items bring with them a unique set of metrics for analyzing the line item's performance in bidding and delivering toward a targeted PG deal. You can find these metrics being monitored for any PG buying line item within the **Line Item Details** pane's **Analytics** tab.

Below are categorized PG buying line item metrics and their descriptions. As a PG buyer, some of these metrics may or may not apply to your specific PG buying scenario and needs, but they serve as an exhaustive list of PG metrics that you may encounter.

| Metric | Description |
|--|--|
| **Percent Delivered** | The percentage of the total PG deal budget delivered to date<br> - **Percent Delivered = (The Number of Impressions Delivered to Date ÷ The PG Deal's Impression Budget) × 100** |

| Metric | Description |
|--|--|
| **Booked Revenue** | The revenue that a network receives from its managed advertisers. The network receives this revenue when a revenue event occurs (**example**: a conversion, click, or bought impression). |
| **Cost Per Acquisition (CPA)** | A payment model in which advertisers pay for every action, such as a sale or registration, completed as a result of a visitor clicking on their creative. An "acquisition" is also referred to as a "conversion." |
| **Cost Per Click (CPC)** | A payment model in which advertisers pay each time a user clicks on their creative |
| **Cost Per Completed View (CPCV)** | The price an advertiser pays every time a video ad runs through to completion. Rather than paying for all impressions, some of which may have been stopped before completion, an advertiser only pays for ads that finished.<br> - **CPCV = Cost ÷ Completed Views** |
| **Cost Per Mille (CPM)** | The standard basic pricing model for online advertising in which advertisers pay for every 1,000 impressions of their served creative |
| **Margin** | The designated currency amount paid to a network as compensation for managed-advertising services<br> - **Margin = Booked Revenue - Media Cost** |
| **Total Media Cost** | The total currency amount that a network pays a publisher for ad space |

| Metric | Description |
|--|--|
| **Click-Through Rate** | The rate or frequency at which users click on a digital creative and arrive at its landing page<br> - **Click-Through Rate = The Number of Clicks to Date ÷ The Number of Impressions Delivered to Date** |
| **Video Completion Rate** | The percentage of an advertiser's video creatives that are played from start to finish. This is also known as a View Through Rate (VTR) or Video Completion Rate (VCR).<br> - **Video Completion Rate = The Number of Completed Video Creatives to Date ÷ The Number of Video Creative Impressions to Date** |

| Metric | Description |
|--|--|
| **Google AdX Impressions** | The total number of impressions recorded for a PG deal using Google Ad Manager's classification for an impression |
| **Measurable Impressions (Imps)** | Impressions classified as when the measurement script fires a pixel to the Microsoft Advertising platform. When the user leaves the page containing the creative before the Microsoft Advertising script actually launched, the impression is counted as served, not measured. |
| **Viewability Rate** | The percentage of creative impressions that are deemed viewable as defined by the Interactive Advertising Bureau (IAB)<br> - **IAB's Definition of a "Viewable" Impression**: For at least one second, 50% of a creative's pixels (or 30% for a creative with at least 242,500 pixels) must be viewable to a viewer on their screen.<br> - **Viewability Rate = (Viewed Impressions ÷ View Measured Impressions) × 100** |
| **Viewable Impressions (Imps)** | Impressions considered viewable based upon Media Rating Council (MRC) and Interactive Advertising Bureau (IAB) viewability guidelines |
| **Microsoft Advertising Impressions** | The total number of impressions recorded for a PG deal using Microsoft Advertising's classification for an impression |

## Related topics

- [Programmatic Guaranteed Buying Line Items](programmatic-guaranteed-buying-line-items.md)
- [Create a Programmatic Guaranteed Buying Line Item](create-a-programmatic-guaranteed-buying-line-item.md)