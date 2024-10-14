---
title: Microsoft Invest - Traffic Quality
description: In this article, learn how to investigate and report suspicious traffic, along with answers to frequently asked questions about regulating unusual activity.
ms.date: 10/28/2023
---

# Microsoft Invest - Traffic quality

Microsoft Advertising makes every effort to search for sellers, publishers, placements, or domains that are seeing illegitimate conversion or click rates. We continue to improve the automated and manual processes of analysis by which we patrol the inventory that runs through our platform. If you have specific questions on how our Traffic Quality team operates, reach out to your Microsoft Advertising representative.

This page describes what to do if you discover suspicious traffic affecting your business and answers some frequently asked questions about traffic quality.

> [!NOTE]
> A campaign should have at least 10,000 impressions on a given slice of inventory in order for the CTR or conversion rate numbers to be considered significant. For more information on these terms, see [Online Advertising and Ad Tech Glossary](../industry-reference/online-advertising-and-ad-tech-glossary.md). We define a "slice of inventory" for this purpose as any given combination of publisher, placement, domain, etc.

## Investigate and report suspicious traffic

If you believe that you are serving on inventory with artificially inflated performance rates, our [support team](https://help.xandr.com/) is happy to investigate. Before submitting a support request, confirm the issue and narrow down the scope as much as possible by following the steps below.

### Step 1: Provide a high-level description of the issue

What is the issue and what objects does it affect? For example, which advertisers or campaigns are affected?

### Step 2: Determine the time range of the incident

- Include when the observed behavior began and if it is still happening.
- Note that historical changes in performance are far more difficult to diagnose as the behavior can no longer be observed live.

### Step 3: Run an Analytics report, breaking results out by various dimensions

For details, see [Member Analytics Report](network-analytics-report.md).

- Is the inflated performance specific to a member, publisher, or placement?
- Is it specific to a creative or creative size?
- Is it specific to a geographic area?

### Step 4: Check the setup of your creatives

- Is click tracking set up properly? For instructions on checking your setup, see [Click Tracking](click-tracking.md).
- Did your advertiser set up their pixels correctly? Are there duplicate pixels on an advertiser's page?

### Step 5: Run a Site Domain Performance report and note the sites where the behavior is happening

For details, see [Site Domain Performance](site-domain-performance.md).

If the behavior is specific to a limited set of domains, inspect the domains to see if there is an explanation.

### Step 6: Send support your findings

After completing the above steps, if you believe you have isolated a specific case, send your findings to [support](https://help.xandr.com).

This should include the following:

- Demand-side object data from your line items and campaigns, grouped by day over the affected time range.
- Remember to include relevant performance metrics (clicks & CTR, conv rate & total conversions).

## Frequently asked questions

This section is intended to help you understand our monitoring and security systems, and any general questions you have about how we respond or regulate unusual activity on the Microsoft Advertising Platform.

### Does Microsoft Advertising allow bidders/advertisers to bid on ad requests where IP addresses are owned by cloud providers such as Amazon Web Services or Rackspace?

We block some cloud providers but not all because some international customers use various cloud providers as a proxy. This is temporary until they fully migrate to our platform.

### Does Microsoft Advertising allow bidder/advertisers to bid on ad requests where IP addresses are listed on the IAB's spider list?

No. We subscribe to the [IAB bots and spiders list](https://www.iab.net/1418/spiders), so bots that are declared in their user agents will not be bid on.

### Does Microsoft Advertising allow bidders/advertisers to bid on ad requests where the UserAgent is not a known standard browser?

We have a list of banned user agents. However, due to the rapid pace of change for many user agents, we can't guarantee we're blocking all unsuitable agents. If you see a suspect user agent, let us know.

### Does Microsoft Advertising have any detection for 'duplicate' clicks?

We de-duplicate clicks on a particular ad impression in our data pipeline.

### Can I get Microsoft Advertising to place on my blocklist a specific IP address or domain?

We're happy to investigate but can't guarantee that action will be taken. Abnormal performance you report may not be reflected across the broader platform.
