---
title: Data Science Toolkit - Incrementality
description: Learn what is Incrementality and why advertisers need to measure incrementality. This page also explains how Xandr helps customers to plan their incrementality strategies and testing.     
ms.custom: data-science
ms.date: 10/28/2023
---


# Data Science Toolkit - Incrementality

## Overview

Advertisers want to ensure the effectiveness of their advertising campaigns and that they are getting the best return on their advertising spend. The Return on Advertising Spend model (ROAS), with its simplified Revenue/Cost equation, provides a generalized view of the success of a campaign. However, the ROAS model misses the complexity of modern advertising and quantifies every user and inventory platform equally. Attribution models such as Last-touch and Multi-touch can provide a more detailed means to measure the impact of a campaign, but they do not prove causality and fail to answer the question: *"Is my campaign driving people to spend money on my product, or would they have converted anyway?”*

To answer this question advertisers need to measure incrementality.

Incrementality is the measurement of incremental lift, the percentage of conversions that can be attributed to an advertisement or advertising campaign. Measuring incrementality moves performance measurement towards answering the question of causality.

## Incrementality and Xandr

Xandr provides a [Log-Level Incrementality Feed](log-level-incrementality-feed.md) which provides data on impressions shown to an audience randomly split between a test group (the group exposed to ads) and a control group (the group not exposed to ads). Additionally, we have provided a [best practices document](incrementality-and-xandr.md) to help our customers plan their incrementality strategies and testing.
