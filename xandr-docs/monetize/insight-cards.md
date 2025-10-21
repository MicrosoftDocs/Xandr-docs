---
title: Insight Cards 
description: Learn about Monetize Insights, which identifies issues and opportunities to help sellers monitor and optimize revenue on the platform.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Insight cards

Monetize Insights automatically identifies issues and opportunities on a periodic basis across a wide range of objects and settings that affect seller monetization. These help Monetize sellers simplify monitoring and optimizing their potential revenue from using the platform.

## Unblock brands

Monetize Insights automatically scans bid rejection data to find brands that are bidding at higher prices on impressions than the transacted revenue but are blocked due to the brand's parent category. These brands are surfaced directly to sellers for review.

This is particularly helpful when Ad Quality rules apply broad category blocks, but specific brands could be considered for exceptions. Sellers can review these insights by previewing the creative to assess its quality against their policy. If acceptable, they can set the brand to **eligible** with a single click in the relevant Ad Quality rule.

- By explicitly setting the brand to **eligible**, the unblocked brand can serve while the general category block remains in place.  
- If the insight is not relevant, the card can be **dismissed**, preventing it from appearing for a period.  
- If the brand should always be hidden from Insights, sellers can **archive** it after dismissal to ensure it never appears again.  
- Sellers can filter insights to view only newly detected brands.  

### FAQ - Unblock brands

**Why do I see more blocked brands due to their category in the Seller Bid Error report?**

The **Seller Bid Error report** provides visibility into all bid rejections, which can help with troubleshooting. However, many bid rejections do not impact revenue because the impression did not transact or the bid was below the transacted revenue.  

Insights focus on **incremental blocked bid value above transacted revenue**, providing a clearer view of bid errors likely to impact revenue.  

**When does the data analysis run?**

Insights are generated **weekly** and are typically available by **9 AM UTC on Mondays**.  

**What is the number of creatives I can preview?**

The insight displays **one** example creative from the brand.  

## Ads.txt

Monetize Insights analyzes **auction filtration logs** to identify impressions filtered due to **ads.txt** and **app-ads.txt**. Insights cards display:  

- The **domain or app**  
- The **operating system family** where the issue is detected  
- The **number of ad requests impacted**  

Clicking on the card title links to the **ads.txt file** or the **app store page**, where available. Sellers can copy the **code snippet** required for ads.txt or app-ads.txt updates.  

> [!NOTE]  
> The code should be updated as **DIRECT** or **RESELLER**, depending on the seller's relationship to the inventory.  

**Insight card generation:**  

- **Frequency**: Weekly  
- **Availability**: Before **9 AM UTC on Mondays**  
- **Data range**: Last **7 days**  

## PSP demand partner issues

Monetize Insights periodically checks enabled **PSP Demand Partners** against revenue data and highlights partners that are configured but receiving no spend.  

Insights also perform **initial troubleshooting** to indicate a root cause, such as: 

- The demand partner **responding with bids** but timing out consistently.  

**Insight card generation:**  

- **Frequency**: Weekly  
- **Availability**: Before **9 AM UTC on Mondays**  
- **Data range**: Last **7 days**  

Clicking **Investigate** loads the latest reporting data and provides options to:  

- Download a **bid request from the sampler**.  
- Access reporting for **granular analysis**.  

> [!NOTE]  
> This insight card is available only for users with the **Prebid Server Premium** role.  

## PSP config issues

Monetize Insights periodically checks for active **PSP configurations** with **no revenue reported** in the last **7 days**. Issues are assigned a **status** based on detection data, helping sellers understand where in the bid request funnel the issue occurs.  

For example:  

- A config **receiving bids** but **none are transacting**.  
- Identifying **key blockers** such as **Floors** or **Ad Quality**.  

**Insight card generation:**  

- **Frequency**: Weekly  
- **Availability**: Before **9 AM UTC on Mondays**  
- **Data range**: Last **7 days**  

Clicking **Investigate** loads the latest reporting data and offers further options for:  

- Downloading a **bid request from the sampler**.  
- Accessing reporting for **granular analysis**.  

> [!NOTE]
> This insight card is available only for users with the **Prebid Server Premium** role.  

## Placement issues

Monetize Insights automatically detects **placements** that:  

- Are sending Ad Requests but receiving no responses 
- Are sending Ad Requests, and receiving responses with no impressions sold
- Have low win rates 

Automatic triaging is applied examining the bid rejections that occured on the placement to indicate if there is significant blocked demand and if so, which category of rejections are most prevalent.
Clicking on **Investigate** button loads the most recent reporting for last 24 hours data showing the impression funnel and blocked bid metrics.

**Insight card generation:**

- **Frequency**: Weekly  
- **Availability**: Before **9 AM UTC on Mondays**  
- **Data range**: Last **7 days**  

### FAQ - Placement issues

**Are all placements evaluated for this insight?**

To reduce noise, only placements that are sending over 10k ad requests in a week are analysed. 

**What is the threshold for low win rate?**

Low win rate is a defined as impressions sold / ad requests being less than 1%. 

## GDPR - TCF Signals

To help publishers operating under General Data Protection Regulation (GDPR) verify whether their integrated Consent Management Platform (CMP) is correctly passing user consent signals in line with the IAB’s Transparency and Consent Framework (TCF), Microsoft Monetize Insight detects or flags publisher domains that meet any of the following criteria:

- Over 25% of ad requests that are blank or missing user consent
- Over 25% of ad requests that have bad or invalid user consent
- Less than 5% of ad requests that include extremely low rate of user consent

#### Insight card details:

- Frequency: Weekly
- Availability: Before 9 AM UTC on Mondays
- Data range: Past 7 days

Click the TCF String Insight card to view the latest publisher-level reporting. To see domain-specific metrics, generate the Seller CMP Analytics report. For more information, see [Seller CMP Analytics report](seller-cmp-analytics-report.md).

## Deals not spending

Monetize Insights automatically flags active deals that have unexpectedly stopped spending, enabling quick identification and follow-up. Detection runs daily, and newly identified deals are labeled "New" in the UI. A deal will be flagged if:

- The end date has not passed, or there is no end date
- The deal is active and not deleted
- No revenue was recorded in the past 24 hours, but revenue was recorded in at least one of the preceding 7 days


Deals are triaged based on bid funnel metrics data to identify if:
- The deal does not send bid requests
- The deal is sending bid requests but not receiving bids
- The deal is receiving bids but not transacting

To investigate the issue, click a flagged deal to see other deals with the same issue in the bid funnel such as "Deals receiving bids, but no impressions sold". Each deal listed displays the following::

- Last revenue date
- Total revenue transacted in the deal over the past 7 days
- Pressing Investigate to pull 24-hour data from the [Seller Deal Metrics](seller-deal-metrics.md) report, to identify:
    - Most recent impressions matched
    - Bid requests sent
    - Bid rate
    - Ineligible bid rate
    - Net win rate

For deeper analysis:
- Navigate directly into reporting
- Download a bid request (if the deal is with an external DSP) and share with buyers to troubleshoot bid submission issues.
