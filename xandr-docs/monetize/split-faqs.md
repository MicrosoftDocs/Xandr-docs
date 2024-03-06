---
title: Microsoft Monetize - Split FAQ
description: Explore FAQs on split objects, covering spend allocation, limitations, and optimize line items with prior max bids using CSV export/import.
ms.date: 10/28/2023
---

# Microsoft Monetize - Split FAQ

## How do I prevent any spend from being allocated to the line item default split?

> [!WARNING]
> Preventing spend from being allocated to the line item default split may result in underdelivery.

If you're using spend allocation, allocate 0% of budget to the line item default split. If you're not using spend allocation, set the line item default status to inactive.

## What are the limitations on split objects?

The limitations per split object are as follows:

- Maximum number of splits per line item: 100
- Maximum number of segments per split: 100
- Maximum number of creatives per split: 100
- Maximum number of items per feature: 200 (For example, you can specify
  200 domains per split or 200 postal codes per split)

## I'd like to enable optimization on a line item where I've previously disabled optimization and used max bids in splits

Currently, the **Optimization** toggle is disabled once you've set max bids for splits. If you'd like to enable optimization and stop using the max bid in splits, it's not possible to do that through editing the individual splits. Instead, you need to download the splits as a CSV, delete the EV information from the CSV, turn on optimization, and import the edited CSV. This creates disjointed reporting (the optimized splits will have different split IDs than the nonoptimized splits), but preserves all of your setup data.

1. Go to **Line Item** \> **Programmable Splits** and click **Export CSV** under **Actions**.
1. Click **Save** to save the CSV file.
1. Go to **Line Item** \> **Optimization** and toggle **Optimization Method** to **Optimization enabled**.
1. Click **Review and Save** to save your changes to the line item.
1. Make a copy of the CSV file you downloaded.
1. In the copied file, delete the columns named **ID** and **Max Bid** and save your changes.
1. Go to **Line Item** \> **Programmable Splits** and click **Import CSV** under **Actions**.
1. Select the CSV you amended and click **Open**.

This creates a new set of splits identical to the old splits except for ID and max bid.
