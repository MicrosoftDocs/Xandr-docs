---
title: Microsoft Invest - Sources of Planner Information
description: In this article, learn where Planner gets data from and what data providers are supported by Planner.
ms.date: 10/28/2023
---

# Microsoft Invest - Sources of planner information

Impression estimates are based on a seven-day sample of data, defined at the daily level. Planner stores seven days' worth of samples, resulting in a rolling weekly snapshot that is updated once per day.

The following table shows the scale of historical data underlying the estimates:

| Period | Scale of Data |
|---|---|
| **Daily** | 10 million auctions/users from the past day |
| **Weekly** | 20 million impressions/users from the past 7 days |

## Planner data providers

Planner supports real-time data provider segments from the Microsoft Advertising Real-Time Signals Service (RTSS) as well as the following brand safety/contextual data providers:

- comScore
- IAS
- DoubleVerify
- Peer39
- Adloox
- Factual
