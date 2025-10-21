---
title: Microsoft Monetize - Valuation
description: In this page, learn what is valuation and how it can be used to determine bid amount. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Microsoft Monetize - Valuation

Valuation is the process by which our system determines a bid amount. Our valuation algorithms determine the appropriate price for an auction based on the likelihood that an event that the advertiser values (a click, a view, a video complete, or a conversion) will occur. Through research and testing, the Microsoft Advertising Data Science team has determined the features and signals that have the most significant impact for accurately calculating the likelihood of an event. We use different mathematical methods, such as logistic regression, to leverage our platform's extensive datasets in creating valuation solutions for each type of advertiser goal. Our system builds a unique data model for each line item to determine the optimal bid for impressions.

The final bid submitted in an auction is further modified based on multiple additional factors, including:

- [Adaptive Pacing](adaptive-pacing.md)
- Goal priority (performance, delivery, or margin)
- Payment type
- Booked revenue
- Partner fees
- Margin

## Predicting clicks

CPC and CTR goals optimize to clicks. The features and signals used to predict the likelihood of clicks are:

- Tag
- Device type
- Browser
- URL
- Geo region
- Creative size
- Segment
- How frequently the user has been served impressions from this advertiser
- How recently the user has been served impressions from this advertiser

## Predicting only post-click conversions

CPA goals can be set to optimize only to post-click conversions. In that case, the features and signals used to predict the likelihood of post-click conversions are:

- Tag
- Device type
- Browser
- URL
- Geo region
- Creative size
- Segment
- How frequently the user has been served impressions from this advertiser
- How recently the user has been served impressions from this advertiser

## Predicting post-click and post-view conversions

You can set a CPA goal that optimizes to both post-click and post-view conversions for both retargeting line items (line items that target customers who have already shown an interest in the advertiser) and prospecting line items (line items that target a broader spread of potential customers who may become interested in the brand). The different types of line items use different features and signals to predict the likelihood of conversion events.

For retargeting line items, the features and signals used to predict these events are:

- Your proprietary segments (that is, segments that are not in the Data Marketplace)
- How recently the user was added to this segment
- How frequently the user has been served impressions from this advertiser
- How recently the user has been served impressions from this advertiser

For prospecting line items, the features and signals used to predict these events are:

- Inventory URL
- Geo region
- How frequently the user has been served impressions from this advertiser
- How recently the user has been served impressions from this advertiser

## Predicting views

vCPM goals optimize to views. The features used to predict the likelihood of views are:

- Tag
- Inventory URL
- Operating system

## Predicting video completes

CPCV and VCR goals optimize to video completes, which occur when a video is played for its entire duration. The features and signals used to predict the likelihood of video completes are:

- Tag
- Inventory URL
- Operating system
- Video Context, for example pre-roll, mid-roll, or post-roll

## Related topics

- [Optimization Guide - ALI](optimization-guide-ali.md)
- [Adaptive Pacing](adaptive-pacing.md)
- [discovery](discovery.md)