---
title: Working with Channel Metrics
description: Use the Channels tab to view high-level metrics for integrated supply-side platform along with the adserver data.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: yield-analytics-ui
ms.author: shsrinivasan
---

# Work with channel metrics

The **Channels** tab provides high-level metrics for integrated Supply-Side Platform (SSPs) along with adserver data. It is a useful tool to contrast guaranteed verses pre-emptible volumes and pricing, in addition to comparing multiple SSP's effectiveness.

Since the **Channels** tab is powered by the **reporting** tab, custom reports can be built within Yield Analytics using data captured from the SSP. In reports, information can be bucketed into four types of channels:

| Channel Type | Definition | Data Source |
|:---|:---|:---|
| SSP (Xandr, AdX, etc.) | Any order line that is associated with a given SSP will be included in that SSP's channel. | SSP |
| Direct Sales | Any guaranteed, non-SSP, in-network order line. | Ad Server |
| N/A | Any pre-emptible, non-SSP, in-network or out-of-network order line. | Channel-specific metrics not provided. |
| Non-Analyzed | Any guaranteed, non-SSP, out-of-network order line. | Ad Server <br> (Contracted values are distributed in a straight-line fashion. Values are not affected by out-of-network data). |

## Channel metric definitions

| Channel Metric | Definition |
|:---|:---|
| Channel Consumed Impressions | The number of impressions that were filled or consumed by the channel. In the case of secondary channels, these are the impressions filled by the channel. |
| Channel Received Impressions | The number of impressions that the channel received as recorded by the channel. In the case of the Direct Sales channel, the Channel Received Impressions will equal Capacity Impressions. |
| Channel Earned Revenue | The total revenue earned by the channel. |
| Channel eCPM | - The computed eCPM for the channel.<br> - Formula: Channel Earned Revenue / (Channel Consumed Impressions/1000) |
| Channel rCPM | - Channel "real" CPM. This is a measure of how well a channel is monetizing the opportunity that it is presented with. It is useful for comparing the value brought by various partners. rCPM uses the "Channel Received Impressions" instead of Channel Consumed Impressions when determining value. <br><br> - Formula: Channel Earned Revenue / (Channel Received Impressions/1000) |
| Channel Fill % | - A measure of the utilization rate of the channel. In the case of the Direct Sales Channel, the Channel Fill % will equal the Sell Through %. This is calculated based on the consumed impressions associated to the Direct channel.<br><br> - Formula: Channel Consumed Impressions/Channel Received Impressions * 100 |
| Channel Advertiser | - Guaranteed, Non-SSP Order Lines – Populates from the order line in ad server <br> - Preemptible, SSP Order Lines – Populates from SSP <br>  - Preemptible, Non-SSP Order Lines – Shows as “N/A” |
| Channel Received Impressions | Impressions that are received by the SSP, as recorded by the SSP. In the case of the Direct Sales Channel, the Channel Received Impressions will equal Capacity Impressions. This is only available in product and targeting reports. |

## SSP specific dimensions

| Xandr Dimension |  Definition |
|:---|:---|
| Buyer Member (Xandr) | The Xandr Buyer Member |
| Placement ID (Xandr) | The Xandr Placement |
| Publisher ID (Xandr) | The Xandr Publisher |
| Site ID (Xandr) | The Xandr Site |

| Google AdX Dimension | Definition |
|:---|:---|
| AdUnit ID (AdX) | The AdX Ad Unit |

| PubMatic Dimension | Definition |
|:---|:---|
| Ad Tag ID (PubMatic) | The ad tag ID from PubMatic. |
| Demand Source (PubMatic) | The demand partner name field from PubMatic (typically, this is always null). |
| Demand Type (PubMatic) | The demand type field from PubMatic. This is not yet available in the PubMatic API, so it will always be null at this point in time. |
| Network (PubMatic) | The Network name field from PubMatic. |
| Site (PubMatic) | The site name field from PubMatic. |

| Rubicon Dimension | Definition |
|:---|:---|
| Site (Rubicon) | The site field from Rubicon. |
| Zone (Rubicon) | The zone field from Rubicon. |
| Size (Rubicon) | The size field from Rubicon. |
| Tag ID (Rubicon) | The tag ID field from Rubicon. |

## Related topic

[Channel Management](./channel-management.md)
