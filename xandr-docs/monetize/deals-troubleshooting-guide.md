---
title: Deals Troubleshooting Guide
description: Use deal configuration and delivery metrics to troubleshoot Microsoft Monetize deals that aren't delivering as expected.
ms.date: 09/01/2026
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: v-garittar
ROBOTS: NOINDEX, NOFOLLOW
---

# Deals troubleshooting guide

## Summary

1. [Introduction](#1-introduction)
1. [Confirm deal eligibility](#2-confirm-deal-eligibility)
1. [Deal delivery: Key metrics to review](#3-deal-delivery-key-metrics-to-review)
1. [Interpreting key metrics and common delivery issues](#4-interpreting-key-metrics-and-common-delivery-issues)
1. [Technical Support escalation path](#5-technical-support-escalation-path)
1. [Appendix A: Buyer line item configurations](#appendix-a-buyer-line-item-configurations)
1. [Appendix B: External DSPs troubleshooting tools](#appendix-b-external-dsps-troubleshooting-tools)
1. [Appendix C: Deal sync with DV360 and TTD](#appendix-c-deal-sync-with-dv360-and-ttd)

## 1. Introduction

This document is intended to help evaluate deals and identify potential issues. It covers key metrics throughout the deal process, providing a comprehensive guide to pinpoint where problems might arise.

## 2. Confirm deal eligibility

Before reviewing delivery or spend, confirm the deal is eligible to transact end-to-end. The checks in this section validate that the deal and the associated line item is active, successfully synced (where applicable), accepted by the buyer, currently within the active date range/flight dates, and the budget is not met (where applicable).

### 2.1 Objects status

- Confirm that all relevant objects in the hierarchy (Advertiser, Insertion Order, Line Item, and deal) are set to “Active.”
- Verify that all the relevant objects in the hierarchy have not been “Deleted”.
- Verify that both the deal and deal line item have not been “Archived”.

> [!TIP]
> Find here more details about Deal Archival [Microsoft Monetize - Automated Deal Archival](automated-deal-archival.md).

### 2.2 Sync status (where applicable)

Confirm that the deal has been synced with the buyer platform.

> [!TIP]
> Microsoft provides automated deal synchronization only for DV360 and The Trade Desk (TTD). These integrations use Microsoft's deal sync services to automatically synchronize deals between platforms.

For more information, refer to the following guides:

- DV360: [Bidders - Deal Sync with DV360 - Publisher Guide](deal-sync-with-dv360-publisher-guide.md)
- The Trade Desk (TTD): [Bidders - Deal Sync with Trade Desk - Publisher Guide](deal-sync-with-trade-desk-publisher-guide.md)

For all other DSPs, partners are responsible for syncing deals using the [Deal API Service](../digital-platform-api/deal-service.md) or managing the sync process within their own platforms and interfaces.

Remember that some DSPs might still require manual creation of the deal from the buyer.

### 2.3 Acceptance status

Confirm that the deal acceptance status is “Accepted” or “Activated.” A “Pending” status indicates the deal is awaiting buyer acceptance.

> [!TIP]
> The acceptance status is only relevant for the DSPs Microsoft is syncing the deals with, for all the other DSPs the Acceptance Status is automatically set to “Accepted”.

### 2.4 Date range & flight dates

- Verify the deal start date has passed (the deal is within its active date range).
- Verify the deal end date has not passed.
- Check the time zone settings, ensure dates are evaluated in the correct time zone.
- For deals with multiple flights, verify the current date falls within an active flight.

## 3. Deal delivery: Key metrics to review

When evaluating deal delivery, the following deal metrics should be reviewed. Five key deal metrics are used to identify the source of a deal issue. This section is critical for pinpointing where a breakdown may be occurring in the deal metrics lifecycle. The goal is to determine which of the five steps in the deal process is impacted. After gathering the relevant background information, this assessment should be the first step when troubleshooting a deal.

### Relevant metrics from Deal Metrics Report

#### 01. Imps Matched

The number impressions eligible for the deal. This is calculated by looking at the available imps from the seller that match the targeting profile of the deal. This does not mean that these available impressions are sent to the buyer. Also called: available imps, avails, imps seen.

- **Are there imps matched on the deal? (Yes / No / Low)**

#### 02. Bid Requests

Imps Matched that are sent to the buyer. Bid requests are controlled by the settings the bidder has on their bidder profile, which determines what supply they've instructed Microsoft/Xandr to send them. Also called: requests, imp requests, ad requests.

- **Are there bid requests on the deal? (Yes / No / Low)**

#### 03. Bids

The number of bids the buyer sends in response to bid requests. Buyers only send bid responses if the bid request matches the targeting on their line item / campaign, whether on our platform or through a bidder. Also called: Bid responses.

- **Are there bids on the deal? (Yes / No / Low)**

#### 04. Imps Won (Sold)

The number of bids that the buyer won the auction for. Buyers might not always win the impression because of external factors at play in the auction such as a competing bid (by price or priority), ad quality, or bidding below the auction floor. Also called: imps, imps sold.

- **Are there imps won (sold) on the deal? Yes or No? Low?**

#### 05. Ineligible Bids

The bids that were rejected from participating in the deal.

Review the [Bid Error Report](seller-bid-error-report.md) to identify bids that were filtered or rejected due to:

- Bid price below the deal floor
- Microsoft policy enforcement
- Seller ad quality restrictions
- Invalid or expired creatives
- Other errors

Refer to the [Bid Error Codes](../bidders/bid-error-codes.md) for additional guidance.

- **Are there ineligible bids on the deal? (Yes / No / Low)**

Answering these questions in sequence will help you determine the starting point for identifying the root cause of the issue: whether it lies with the seller object, the curator object, or the buyer object. It's crucial to pinpoint which of these steps is causing your deal to be stopped.

> [!TIP]
> To verify this, review the relevant columns in the [Monetize Deal Screen](deals-screen-in-microsoft-monetize.md) or access the [Seller Deal Metrics report](seller-deal-metrics.md) in Reporting.

## 4. Interpreting key metrics and common delivery issues

Review the following metrics to understand where delivery stops:

- Imps Matched: eligible impressions for the deal
- Bid Requests: bid requests sent to buyers
- Bids: buyer bid responses
- Imps Won (Sold): the count of bids that successfully won
- Ineligible Bids: rejected bids

### 4.1 If the deal has no impressions matched

- Confirm that the deal, the deal line item, and all associated parent objects are active.
- Verify with the buyer that they have accepted or approved the deal. Rejected or Cancelled deals will result in no impressions matched.
- Review whether seller inventory matches the deal targeting.
- Verify with the Technical Support team that the buyer and seller are GDPR compliant, confirm the buyer’s contractual status, eligibility, and ability to receive traffic, and determine whether the buyer has successfully transacted through other deals or via OpenRTB.

### 4.2 If deal has impressions matched but no bid requests

Verify with the Technical Support team whether bidder profile restrictions, QPS limits, or supply throttling constraints are impacting traffic delivery.

> [!TIP]
> Check the following documents for more details:
>
> - [Supply Stream Efficiency](../bidders/supply-stream-efficiency.md)
> - [Bidder Profile - FAQ](../bidders/bidder-profile---faq.md)
> - [QPS FAQ](../bidders/qps-faq.md)
> - [Optimized Bid Stream FAQ](../bidders/optimized-bid-stream-faq.md)

### 4.3 If bid requests are sent but no bids are received

The absence of bids from external DSPs cannot be diagnosed from the Microsoft side alone. Effective troubleshooting requires direct engagement with the buyer contact. If the buyer contact is unavailable, investigation and resolution capabilities are significantly limited.

- Confirm that the buyer seat ID targeted in the deal matches the buyer DSP partner ID.
- Verify with the buyer that the deal exists and is approved in their DSP.
- Verify with the buyer that the deal is targeted to an active line item with sufficient budget, that line item targeting aligns with the deal settings, and that an audited creative is associated with the line item and eligible to receive traffic.
- Verify with the buyer that creatives attached to the buying line item are approved, compatible, and not expired (External bidder creatives are automatically considered expired when they have not served impressions and have not been modified within a 15-day period. [Microsoft Monetize - Troubleshoot Third-party Creatives across Microsoft Advertising Inventory](troubleshoot-third-party-creatives.md)).
- Verify with the buyer whether buying line item targeting is overly restrictive.

> [!TIP]
> Reference [Appendix A: Buyer line item configuration](#appendix-a-buyer-line-item-configurations).

### 4.4 If bids are present but impressions sold are low or zero

Even when valid bids are submitted, impressions sold may remain low or fail to transact due to auction dynamics, inventory competition, policy restrictions, or downstream publisher-side decisioning. Review the following areas:

#### Buyer Eligibility and Pricing

- Confirm the buyer bid price meets or exceeds the deal floor price.
- Verify the buyer is eligible to participate in the deal and meets any contractual requirements.

#### Creative and Policy Validation

- Verify creatives are eligible and compatible with the deal's media type.
- Confirm creatives are active, approved, and not expired.
- Review brand safety, viewability, quality, and Microsoft policy requirements.
- Check for any seller- or inventory-level restrictions applied through OpenRTB requests or publisher controls.

#### Auction Competition and Seller Prioritization

- Determine whether competing buyers are submitting higher bids for the same inventory.
- Review seller-side competition, including:
  - Higher-priority direct or guaranteed deals
  - Preferred or priority line items
  - Other auction participants bidding on the same inventory

#### Secondary Publisher-Side Auctions

In OpenRTB or Prebid integrations, a bid win within Microsoft Advertising does not guarantee the impression will be served.

Publishers may run a secondary auction in their ad server, where competing line items can receive priority based on pricing or delivery rules.

In these scenarios, bids are successfully returned but do not convert into impressions.

#### Bids Sent but No Response (BSNR) Scenarios

Investigate cases where bids are returned but no response is received from the publisher. Potential causes include:

- Seller-side rejection after the bid is submitted.
- Publisher ad server prioritization preventing the bid from serving.
- Technical factors such as lazy loading, player behavior, or impression tracking failures.

> [!NOTE]
> If bids are successfully returned by Microsoft but do not result in impressions, the root cause is often outside of the Microsoft platform. Coordination with the seller or publisher may be required to determine why bids are not winning or converting in the final auction.

## 5. Technical Support escalation path

If all sections above have been reviewed and the issue remains unresolved, follow the escalation steps outlined below.

### 5.1 Helpful information for escalation

To enable efficient investigation, ensure the following details are documented before raising an escalation. When submitting the request, include as much of the information below as possible:

- Deal ID and deal type (PG, Standard)
- Buyer member/seat ID and seller member ID
- Deal start date and the date the issue was first observed
- Observed symptoms, such as: No delivery, Under-delivery, or Delivery stopped after initial spend
- Troubleshooting steps already completed from this guide
- Any error messages, warnings, or system indicators encountered
- Screenshots of deal configuration (if available), including Buyer side and Seller side
- Relevant reports supporting the observed behaviour

Providing comprehensive information upfront helps reduce back-and-forth and accelerates root-cause identification.

### 5.2 Customer Support Portal

For platform support and escalations, use the [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com).

## Appendix A: Buyer line item configurations

Microsoft does not have access to the buyer line item configurations within external DSP platforms. While we encourage buyers to share screenshots or console views to support collaborative troubleshooting, this approach is often limited in effectiveness. The limited visibility into the external buyer's configurations makes it challenging to diagnose issues; however, we are aware of the following major buyer settings that can act as blockers:

### 1. Seat ID / Partner ID misconfiguration

Using the wrong seat ID (e.g. generic Microsoft member ID instead of the DSP’s actual Partner/Advertiser ID) will prevent the deal from syncing and appearing in the buyer’s DSP.

### 2. Deal not approved in DSP

Even if the deal syncs, the buyer must approve/accept it in their DSP UI (e.g., DV360 Negotiations tab, TTD Deals screen). If not approved, the deal will not deliver.

### 3. Line item targeting

The deal must be attached to an active line item with budget. If the buyer forgets to target the deal, or the line item is paused or not yet live, no spend will occur.

### 4. Creative technical attributes / category / media type / size and approval

The buyer must use compatible creatives (e.g. display for display inventory, video for video inventory). Creatives must be approved in the DSP; unaudited or pending creatives will block delivery.

Creative technical attributes or category issues (e.g. running a pharma creative on publishers that don’t accept pharma).

### 5. Targeting restrictions

Overly narrow targeting (geo, device, audience, day parting, frequency caps) can block or throttle delivery. For example:

- Geographical targeting mismatch between the deal and the buyer’s line item.
- Device/platform mismatch (e.g. targeting web only when the deal includes only app inventory).
- Segment targeting is too restrictive: broaden the segment targeting or expand size of segments by adding in third-party audiences. Using Google Audiences in DV360 will block delivery on Microsoft supply, as Microsoft is not opted into Google’s data co-op.

### 6. Blocklists and allowlists

Buyer-applied blocklists (URLs, apps) at any level (agency, seat, advertiser, IO, line item) can inadvertently block sellers. Allowlists are equally important; if seller domains aren’t included, delivery may be blocked.

### 7. Floor price and bid rate

If the buyer’s bid is below the deal’s floor CPM, they will not win impressions. Miscommunication around floor pricing or overly aggressive optimization targets that reduce bid prices are common blockers.

### 8. Manual deal registration

For DSPs without auto-sync (e.g., Yahoo, Amazon, other DSPs), buyers must manually register the deal using the Deal ID. If this step is missed or the Deal ID is entered incorrectly, the deal will not deliver.

### 9. Brand safety and verification settings

Brand safety exclusions or viewability thresholds set too high can block bid responses if the seller doesn’t meet those criteria.

### 10. Viewability incompatibilities

DSPs use proprietary technologies to estimate whether an ad is likely to be viewed. This functionality depends on impressions being measurable, something that can be technically challenging on third-party exchanges such as Microsoft Monetize. Due to these incompatibilities, when impressions are not measurable, DSPs are unable to place bids.

### 11. Technical/platform-specific issues

Bugs or integration issues (e.g. sync failures, incorrect mapping) may require escalation to support teams on both sides.

> [!TIP]
> **Bid Request Sampler**
>
> Alternatively, where possible, provide a sample bid request to the DSP buyer contact for further analysis. Supplying a sample bid request can assist the DSP’s technical support team in identifying why the buyer line item is unable to bid. The bid request can be captured in Monetize or Curate UI.
>
> The Bid Request Sampler provides sample bid request data under certain time frames and conditions. You can download results as a text file.
>
> Find more details here: [Microsoft Monetize - Sample Bid Requests](sample-bid-requests.md) / [Microsoft Curate - Sample Bid Requests](../curate/curate-sample-bid-requests.md).

## Appendix B: External DSPs troubleshooting tools

Microsoft does not have visibility into buyer line item configurations within external DSP platforms. While buyers are encouraged to share screenshots or console views to support collaborative troubleshooting, this approach may provide limited insight and may not fully ho the root cause of bidding issues.

Some DSPs offer dedicated troubleshooting tools that buyers can leverage to diagnose why a line item is not bidding:

- Display & Video 360 (DV360) provides a built-in Deal Troubleshooter, which offers detailed diagnostics explaining why a buyer line item may not be bidding on a deal. This tool surfaces specific blocking conditions and setup issues affecting bid activity. Refer to **Troubleshoot your deals and line items - Display & Video 360 Help**.
- Amazon buyers can refer to the Missed Opportunities section to identify reasons why bids or impressions may not be occurring. Refer to **Missed opportunities | Amazon Ads Support Center**.

Tooling and diagnostic capabilities vary by platform. Buyers are encouraged to use any available DSP-specific troubleshooting resources to investigate deal and line-item behaviour.

For other DSPs, there is no confirmed availability of a dedicated deal troubleshooting tool. In these cases, investigation relies primarily on buyer-side reporting, configuration review, and direct engagement with the DSP.

## Appendix C: Deal sync with DV360 and TTD

This section describes the most common reasons a deal may fail to sync with a demand-side platform (DSP), such as DV360 or The Trade Desk. Because Microsoft manages the deal synchronization process with these DSPs, we can provide visibility into the sync status and help identify potential issues that may prevent successful delivery.

A deal is eligible to sync when all of the following conditions are met:

### 1. Deal and associated line item are active

The deal and associated line item are active in the platform. Inactive or paused status are filtered out before any sync attempt.

### 2. Deal has not expired

The deal’s end date has not passed. Deals with an end date in the past are excluded from sync.

### 3. Deal and associated line item are not archived or deleted

The deal and associated line item that have been archived or deleted are not eligible to sync to DSPs.

### 4. Buyer / DSP configuration is valid

The buyer seat / partner ID must be valid and recognized by the DSP, otherwise the sync will fail or be rejected.

### 5. DSP API service is available

Deal sync depends on the DSP’s API service being available. Temporary DV360 or TTD API outages can delay or block syncing even when the deal itself is correctly configured.

For more details on the deal sync process, please refer to the following resources:

- [Microsoft Monetize - Publisher Guide for Deal Sync with Trade Desk](deal-sync-with-trade-desk-publisher-guide.md)
- [Microsoft Monetize - Publisher Guide for Deal Sync with DV360](deal-sync-with-dv360-publisher-guide.md)
- [Microsoft Monetize - Deal Sync with Trade Desk (FAQ)](deal-sync-with-trade-desk-faq.md)
- [Microsoft Monetize - FAQs on Deal Sync with DV360](deal-sync-with-dv360-faq.md)
- [Microsoft Monetize (March 6, 2026) Deal sync status visibility and filtering](release-notes-03-06.md)

> [!TIP]
> Even after a deal syncs successfully, the buyer must accept and have buying line item targeting the deal in their DSP before it can transact.
