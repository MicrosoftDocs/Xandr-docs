---
title: Integration with OpenRTB 2.6 Protocol for Bidders
description: Explore this article to learn how Xandr's demand partners integrate using the OpenRTB protocol. Xandr supports the OpenRTB 2.6 protocol for receiving impressions across all media types.
ms.date: 09/22/2026
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Integration with OpenRTB 2.6 protocol for bidders

This page outlines how Xandr's demand partners integrate using the OpenRTB protocol. Xandr supports the OpenRTB 2.6 protocol for sending and receiving impressions across all media types. This document highlights the top-level objects that have changes or updates, including new fields that are added or implemented. Additionally, it outlines the fields that have been transitioned from their previous location in OpenRTB 2.4/2.5 to their new location in OpenRTB 2.6.

## Implementation

To ensure seamless functionality and compatibility with the latest bidding protocols, it is essential that all bidders activate support for OpenRTB 2.6. This version introduces new fields and enhancements designed to improve bidding performance and transparency.

<!-- ### Endpoint

To make OpenRTB 2.6 requests on the sell side, you must use the OpenRTB version header. The inclusion of this header is mandatory. If it is not included, the system will default to OpenRTB 2.4.

The header and version to use is:

```
x-openrtb-version : 2.6
``` -->

> [!NOTE]
> Bidders must be enabled for OpenRTB 2.6 to start receiving the OpenRTB 2.6 fields listed below. Otherwise, the system will default to version 2.4 or 2.5. To update this setting, contact your account representative or submit a ticket through the support portal.

## Top-level bid request object

The OpenRTB 2.6 protocol introduces several changes and updates to the top-level objects and their associated fields that were previously supported by OpenRTB 2.4. The following sections detail these changes and updates, outlining the specific objects and fields that have been modified or added as a part of the OpenRTB 2.6 implementation.

> [!NOTE]
> Any field(s) not listed here remains supported in its original location as documented in the [OpenRTB 2.4 protocol](outgoing-bid-request-to-bidders.md).

| Field | Type | Description |
|:---|:---|:---|
|`imp`| array of objects | (Required). The impressions offered in this bid request. See [Impression Object](#impression-object) below. <br><br> **Note:** The `imp` is not a new field in the OpenRTB 2.6 protocol guide. It is included in this document solely as a reference to the `rwdd` field in the below [section](#impression-object). |

## Impression object

The `Imp` object defines an ad placement or impression being auctioned. A single bid request can include multiple `Imp` objects, which is useful for exchanges that support selling all ad positions on a given page. Each Imp object requires an ID, allowing bids to reference them individually.

> [!NOTE]
> Any field(s) not listed here remains supported in its original location as documented in the [OpenRTB 2.4 protocol](outgoing-bid-request-to-bidders.md).

As a part of the OpenRTB 2.6 implementation, Xandr has added the following field(s) to the `Imp Object`.

| Field | Type | Description |
|:---|:---|:---|
|`rwdd`| integer | This field indicates whether the user receives a reward for viewing the ad, with `0` representing "no" and `1` representing "yes." Typically, video ad implementations grant rewards such as access to an additional news article for free, an extra life in a game, or a sponsored ad-free music session. The reward is usually provided after the video ad is fully viewed. |
| `video` | object | This field is required if the impression is offered as a video ad. See [Video Object](#video-object) below. <br><br> **Note:** The `video` is not a new field in the OpenRTB 2.6 protocol guide. It is included in this document solely as a reference to the `plcmt` field in the below [section](#video-object). |

## Video object

The `Video` object represents a video impression. While many of its fields are non-essential for minimally viable transactions, they are included to provide fine control when necessary. Video in OpenRTB generally adheres to the VAST standard. Consequently, companion ads are supported by optionally including an array of `Banner` objects that define these companion ads. For more details, see [Banner object](https://github.com/InteractiveAdvertisingBureau/openrtb2.x/blob/main/2.6.md#326---object-banner-)

> [!NOTE]
> Any field(s) not listed here remains supported in its original location as documented in the [OpenRTB 2.4 protocol](outgoing-bid-request-to-bidders.md).

### Video ad pods

Starting in version 2.6, OpenRTB supports pod bidding for video and audio content streams. An ad pod is an ad break containing one or more in-stream creatives that play sequentially. For an introduction to structured and dynamic pods, see [Video ad pods](../monetize/video-ad-pods.md).

A structured pod defines its slots in advance. A dynamic pod defines the total fillable duration in `video.poddur` and the maximum number of ads in `video.maxseq`; the winning bids determine the number and duration of ads in the final sequence. The presence of `podid` alone does not make a pod dynamic.

> [!IMPORTANT]
> Bidders must be enabled for OpenRTB 2.6 to receive dynamic pod fields. For enabled bidders, Microsoft Monetize passes dynamic pod requests without converting them to structured pods. Bidders that aren't enabled receive the version 2.4 or 2.5 representation instead. Enablement doesn't guarantee podded traffic; the seller must also send a dynamic pod. Contact your account representative or submit a ticket through the support portal to request enablement.

The following fields can appear in the request. These definitions align with the September 2026 release of the [IAB Tech Lab OpenRTB 2.6 specification](https://github.com/InteractiveAdvertisingBureau/openrtb2.x/blob/main/2.6.md).

#### Bid request fields

| Field | Type | Description |
| --- | --- | --- |
| `video.podid` | string | Unique identifier marking an impression opportunity as belonging to a video ad pod. Opportunities within a bid request that share a `podid` belong to the same pod. |
| `video.podseq` | integer; default `0` | The sequence, or position, of the ad pod within the content stream. Refer to AdCOM 1.0 for guidance on use. |
| `video.poddur` | integer; recommended | The total number of seconds advertisers may fill in a dynamic video ad pod, or in the dynamic portion of a hybrid pod. Required only for the dynamic portion. It describes the length of the entire break, whereas `minduration`, `maxduration`, and `rqddurs` constrain the individual slots. |
| `video.maxseq` | integer; recommended | The maximum number of ads that may be served into a dynamic video ad pod, where the seller has not predetermined the precise number. |
| `video.rqddurs` | integer array | Precise acceptable creative durations in seconds. Aimed at the live TV case, where inexact durations leave dead air. Mutually exclusive with `minduration` and `maxduration`. |
| `video.slotinpod` | integer; default `0` | Indicates a slot position the seller can guarantee delivery against. Refer to [List: Slot Position in Pod](https://github.com/InteractiveAdvertisingBureau/AdCOM/blob/main/AdCOM%20v1.0%20FINAL.md) in AdCOM 1.0, where `-1` is the last ad in the pod, `0` any ad, `1` the first ad, and `2` the first or last ad. |
| `imp.video.plcmt` | integer | The video placement subtype for the impression. Refer to [List: Plcmt Subtypes - Video](https://github.com/InteractiveAdvertisingBureau/AdCOM/blob/main/AdCOM%20v1.0%20FINAL.md) in AdCOM 1.0. For implementation guidance, see [Use `Plcmt`, `Placement`, and `Context` fields together](#use-plcmt-placement-and-context-fields-together). |

#### Transaction IDs

The following transaction ID fields can accompany a pod request. One impression-level transaction ID corresponds to one logical ad break.

| Field | Type | Description |
| --- | --- | --- |
| `source.tid` | string; recommended | Transaction ID that must be common across all participants in this bid request, including any other exchanges involved. |
| `imp[].ext.tid` | string | Impression-level transaction ID, carried as an extension. Buyer guidance for long-form video is that one transaction ID corresponds to one logical ad break. |
| `source.ext.tidt` and `imp[].ext.tidt` | integer | Transaction ID type, carried as an extension alongside the ID itself. |

The transaction ID type tells you how far the identity can be trusted across the supply chain and whether it can be used to deduplicate an opportunity that arrives by more than one path.

| Value | Meaning | When a bidder sees it |
| --- | --- | --- |
| `1` | Publisher or globally unique | The transaction ID is unique to the ad break across the supply chain, so it can be used to deduplicate the opportunity. Transaction IDs that Microsoft Monetize generates for first-party supply carry this value. |
| `2` | Non-unique, or unique only per demand source | The same ad break may appear under different IDs on different paths, so the ID must not be used for cross-path deduplication. Transaction IDs that Microsoft Monetize generates for third-party supply carry this value. |

The following request describes a dynamic pod that can contain at most three ads totaling no more than 60 seconds:

```json
{
  "source": {
    "tid": "break-123",
    "ext": { "tidt": 1 }
  },
  "imp": [{
    "id": "pod-imp-1",
    "video": {
      "podid": "pod-123",
      "poddur": 60,
      "maxseq": 3,
      "minduration": 15,
      "maxduration": 30
    },
    "ext": {
      "tid": "break-123",
      "tidt": 1
    }
  }]
}
```

#### Bid response fields

Return multiple `bid` objects against the same pod impression to offer more than one creative. Microsoft Monetize uses each bid's `dur` value to assemble an ordered sequence that fits within `video.poddur` and doesn't exceed `video.maxseq`. The sequence can contain fewer ads or less total duration than the seller allows.

| Field | Type | Description |
| --- | --- | --- |
| `bid.dur` | integer | Duration of the video or audio creative in seconds. The platform uses it to assemble a sequence that fits within the pod duration. See [Object: Bid](#object-bid). |
| `bid.slotinpod` | integer | The slot position the bid is intended to fill, using the same AdCOM values as the request side. Return it only where the seller offered a guaranteed position. |

```json
{
  "seatbid": [{
    "bid": [
      { "id": "bid-1", "impid": "pod-imp-1", "price": 8.50, "dur": 30 },
      { "id": "bid-2", "impid": "pod-imp-1", "price": 5.25, "dur": 15 }
    ]
  }]
}
```

## Use `Plcmt`, `Placement`, and `Context` fields together

The OpenRTB 2.6 specification replaces the `placement` field (`imp.video.placement`) from OpenRTB 2.4/2.5 with the `plcmt` field (`imp.video.plcmt`). However, some sellers might still use OpenRTB 2.4/2.5.
<!-- To maximize demand sources, include both the `placement` and `plcmt` fields in your requests. -->

Refer to the table below to find the correct values. Start by comparing your OpenRTB 2.4/2.5 `placement` values with their corresponding `plcmt` fields in OpenRTB 2.6.

> [!NOTE]
> `Instream` placements are now divided into `Instream` and a new `Accompanying Content` value.

<!-- In addition to the `plcmt` and `placement` fields, include the `context` field in the AppNexus video extension object (`imp.video.ext.appnexus.context`) in your bid requests. This field provides crucial information about the video's position (e.g., pre-roll, mid-roll, or post-roll) that the `plcmt` or `placement` fields alone do not convey (see the "Xandr Extension" column below). Ensure your bid requests include all three fields. -->

| Video Ad type | Description | OpenRTB 2.4/2.5 | OpenRTB 2.6 | Xandr extensions |
|:---|:---|:---|:---|:---|
| `Instream` | Pre-roll, mid-roll, and post-roll ads play before, during, or after the streaming video content requested by the consumer. The instream video must start with “sound on” by default or have clear user intent to view the video content explicitly. While additional content may surround the player, the video content should be the primary focus of the user's visit. It must remain the main content on the page and the sole video player visible with audio capabilities during playback. If the player transitions to floating or sticky mode, subsequent ad calls should accurately reflect the updated player size. <br> <br> **NOTE:** The start delay determines the appropriate context (pre-roll, mid-roll, or post-roll) when placement = 1 and plcmt = 1. | `imp.video.placement = 1` | `imp.video.plcmt = 1` | imp.video.ext.appnexus.context = 1 (pre-roll), imp.video.ext.appnexus.context = 2 (mid-roll), imp.video.ext.appnexus.context = 3 (post-roll) |
| `In-Article (formerly known as Appnexus Outstream format)` | Video ads played independently of streaming video content, appearing in placements such as slideshows, native feeds, within content, or as sticky/floating elements. These ads dynamically load and play between paragraphs of editorial content, presenting as distinct branded messages. | `imp.video.placement = 3` | `imp.video.plcmt = 4` | imp.video.ext.appnexus.context = 4 (outstream) |
| `In Banner` | This format resides within a web banner that utilizes the banner space to provide a video experience instead of a static or rich media format. It depends on the availability of display ad inventory on the page for delivery. | `imp.video.placement = 2` | `imp.video.plcmt = 4` | imp.video.ext.appnexus.context = 5 (bannerstream) |
| `In Feed` | This ad format appears in content, social, or product feeds. | `imp.video.placement = 4` | `imp.video.plcmt = 2` | imp.video.ext.appnexus.context = 6 (in-feed) |
| `Interstitial` | This ad format plays video without accompanying video content. During playback, it must maintain primary focus on the page, occupy the majority of the viewport, and remain fixed without scrolling out of view. This can occur in placements such as in-app video or slideshows. | `imp.instl = 1 ,imp.video.placement = 5` | `imp.video.plcmt = 3` | imp.video.ext.appnexus.context = 7 (interstitial) |
| `Accompanying Content`| Pre-roll, mid-roll, and post-roll ads that are played before, during, or after streaming video content. The video player loads and plays before, between, or after paragraphs of text or graphical content, and starts playing only when it enters the viewport. Accompanying content should only start playback upon entering the viewport. It may convert to a Pre-roll, mid-roll, and post-roll ads play before, during, or after streaming video content. The video player loads and initiates playback before, between, or after paragraphs of text or graphical content, beginning only when it comes into view. Accompanying content starts playback when it enters the viewport. The player may convert to a floating or sticky position as it scrolls off the page. <br> <br> **NOTE:** The start delay determines the context (pre-roll, mid-roll, or post-roll) to use when placement = 1 and plcmt = 2. | `imp.video.placement = 1` | `imp.video.plcmt = 2` | imp.video.ext.appnexus.context = 8  (pre-roll) , imp.video.ext.appnexus.context = 9  (mid-roll), imp.video.ext.appnexus.context = 10 (post-roll) |

## Object: Network

This object describes the network an ad will be displayed on. A **network** is defined as the parent entity of the **Channel** object’s entity for the purposes of organizing Channels. Examples are companies that own and/or license a collection of content channels (e.g., Viacom, Discovery, CBS, WarnerMedia, Turner, and others) or studios that create such content and self-distribute content.

The **name** is a human-readable field, while **domain** and **id** can be used for reporting and targeting purposes.

### Network attributes

| Attribute | Type   | Description                                                                 |
|-----------|--------|-----------------------------------------------------------------------------|
| id | string | A unique identifier assigned by the publisher. This may not be unique across all supply sources. |
| name | string | Network the content is on (e.g., a TV network like “ABC”). <br> **Note**: This field was previously supported through an extension of the **content object** in older OpenRTB versions. For more details, see [OpenRTB 2.4 documentation](outgoing-bid-request-to-bidders.md). <br> **NOTE:** Beginning on or after June 30th, 2025, Monetize sends both the standardized mapped values as well as the unstandardized raw values that we receive from partners in a unified comma-delimited list for this field. This will be formatted as [mapped value], [raw value].|
| domain| string | The primary domain of the network (e.g., “abc.com” for the network ABC). It is recommended to include the top private domain (PSL+1) for DSP targeting normalization purposes. |

## Object: Channel

This object describes the channel an ad will be displayed on. A Channel is defined as the entity that curates a content library or stream within a brand name for viewers. Examples are specific view-selectable "channels" within linear and streaming television (e.g., MTV, HGTV, CNN, BBC One) or a specific stream of audio content commonly called "stations."

The **name** is a human-readable field, while **domain** and **id** can be used for reporting and targeting purposes.

#### Channel attributes

| **Attribute** | **Type** | **Description** |
|---------------|----------|-----------------|
| `id` | string   | A unique identifier assigned by the publisher. This may not be a unique identifier across all supply sources. |
| `name` | string   | Channel the content is on (e.g., a local channel like "WABC-TV"). |
| `domain`| string   | The primary domain of the channel (e.g., "abc7ny.com" in the case of the local channel WABC-TV). It is recommended to include the top private domain (PSL+1) for DSP targeting normalization purposes. |

## Object: User

We support the following fields in the `user` object:

| **Field** | **Type** | **Description** |
| --- | --- | --- |
| `user.consent` | string | When GDPR regulations are in effect, this attribute holds the Transparency and Consent Framework's Consent String data structure. |
| `user.eids` | object array | This section details the support of a standard protocol for multiple third-party identity providers. See [Object: EID](#object-eid) for more details. |

## Object: EID

The `EID` object contains extended identifiers from a source or technology provider. We support the following fields in the `EID` object:

| **Attribute** | **Type** | **Description** |
| --- | --- | --- |
| `inserter` | string | The canonical domain name of the entity that added the ID array element. For ad tech intermediaries, use the domain listed in ads.txt. For publishers, use the domain in the `site` or `app` object. |
| `source` | string | Canonical domain of the ID. |
| `matcher` | string | Technology provider responsible for the match method specified in `mm`. When omitted, `matcher` is assumed to equal `source`. This field may be omitted when `mm` is `0`, `1`, or `2`. |
| `mm` | integer | Match method used by the `matcher`. Refer to *List: ID Match Methods* in AdCOM 1.0. |
| `uids` | object array | Array of extended ID `UID` objects from the given source. See [Object: UID](#object-uid) for more details. |

> [!NOTE]
> Microsoft Monetize supports sending the `inserter`, `matcher`, and `mm` fields in all OpenRTB bid requests, across all versions. For bidders using OpenRTB versions earlier than 2.6, enablement is required to receive these fields. Contact your Microsoft account representative or submit a support ticket to request access.

## Object: UID

This object contains a single user identifier provided as part of extended identifiers.

| **Attribute** | **Type** | **Description** |
| --- | --- | --- |
| `id` | string | The identifier for the user. |
| `atype` | integer | Type of user agent the ID is from. It is highly recommended to set this, as many DSPs separate app-native IDs from browser-based IDs and require a type value for ID resolution. Refer to [List: Agent Types](https://github.com/InteractiveAdvertisingBureau/AdCOM/blob/master/AdCOM%20v1.0%20FINAL.md#list_agenttypes) in AdCOM 1.0. |

> [!NOTE]
> Microsoft Monetize supports sending the `atype` field in all OpenRTB bid requests, across all versions. For bidders using OpenRTB versions earlier than 2.6, enablement is required to receive this field. Contact your Microsoft account representative or submit a support ticket to request access.

## Object: Deal

The `Deal` object defines a deal that applies to an impression.

| **Field** | **Type** | **Description** |
|:---|:---|:---|
| `guar` | integer; default `0` | Indicates whether the deal is guaranteed and the bidder must bid on the deal. A value of `0` indicates a non-guaranteed deal, and `1` indicates a guaranteed deal. |

> [!NOTE]
> Microsoft Monetize supports sending the `deal.guar` field in all OpenRTB bid requests, across all versions. For bidders using OpenRTB versions earlier than 2.6, enablement is required to receive this field. Contact your Microsoft account representative or submit a support ticket to request access.

## Object: Bid
OpenRTB 2.6 includes the additional capability to declare the taxonomy in use.

| **Field** | **Type** | **Description** |
|:---|:---|:---|
| `cattax` | integer; default 1 | **NOTE:** Available September 2025. If your ad is political, you need to declare. See [Monetize Creative Standards](../monetize/creative-standards.md) for more details regarding required EU declaration beginning Fall 2025. <br> The taxonomy in use. <br> **NOTE** IAB Content Taxonomy v1.0 is assumed if the `cat` field is present without `cattax`. Otherwise, the mapping is as such: <br> - 1 - IAB Content Taxonomy v1.0 <br> - 2 - IAB Content Taxonomy v2.0 <br> - 3 - IAB Ad Product Taxonomy v1.0 <br> - 5 - IAB Content Taxonomy v2.1 <br> - 6 - IAB Content Taxonomy v2.2 <br> - 7 - IAB Content Taxonomy v3.0 <br> - 8 - IAB Ad Product Taxonomy v2.0 <br> - 9 - IAB Content Taxonomy v3.1|
| `dur` | integer | Duration of the video or audio creative in seconds. |


## Updated field locations

A number of fields have moved from the old location in OpenRTB 2.4/2.5 to the new location in OpenRTB 2.6.

> [!NOTE]
> Any field(s) not listed here remains supported in its original location as documented in the [OpenRTB 2.4 protocol](outgoing-bid-request-to-bidders.md).

| Old location (OpenRTB 2.4/2.5) | New location (OpenRTB 2.6) | Type | Description |
|:---|:---|:---|:---|
| `regs.ext.gdpr` | `regs.gdpr` | integer | The flag indicating GDPR regulation applicability is set as follows: <br> - **0** signifies No <br> -  **1** signifies Yes <br> - **omission** denotes Unknown <br> See [Regs Resources](https://github.com/InteractiveAdvertisingBureau/openrtb2.x/blob/main/implementation.md#regsresources) for detailed information.|
| `regs.ext.us_privacy` |  `regs.us_privacy` | string | Communicate consumer privacy signals under US privacy regulation. See [Regs Resources](https://github.com/InteractiveAdvertisingBureau/openrtb2.x/blob/main/implementation.md#regsresources) for detailed information.|
| `ext.schain`| `source.schain` | object | This object represents the links in the supply chain and indicates whether the supply chain is complete. See [Supply chain](https://github.com/InteractiveAdvertisingBureau/openrtb2.x/blob/main/2.6.md#objectsupplychain) for detailed information. |
| `ext.schain.complete` | `schain.complete` | integer | Indicates whether the chain includes all nodes involved in the transaction, tracing back to the owner of the site, app, or other inventory medium. A value of **0** means no, and **1** means yes. |
| `ext.schain.nodes` | `source.schain.nodes` | object array | Represents an array of SupplyChainNode objects in the order of the chain. In a complete supply chain, the first node is the initial advertising system and seller ID involved in the transaction, such as the site, app, or other medium owner. In an incomplete supply chain, it represents the first known node. The last node represents the entity sending this bid request. |
| `ext.schain.ver` | `source.schain.ver` | string | Indicates the version of the supply chain specification in use, formatted as “major.minor.” For example, use the string “1.0” for version 1.0 of the specification. |
| `ext.schain.nodes.asi` | `source.schain.nodes.asi` | string | Indicates the canonical domain name of the SSP, Exchange, Header Wrapper, or other system that bidders connect to. This domain may be the operational domain of the system, if different from the parent corporate domain, to facilitate WHOIS and reverse IP lookups for establishing clear ownership of the delegate system. This should be the same value as used to identify sellers in an ads.txt file if one exists. |
| `ext.schain.nodes.sid` | `source.schain.nodes.sid` | string | The identifier associated with the seller or reseller account within the advertising system. This value must match the one used in transactions (e.g., OpenRTB bid requests) in the field specified by the SSP/exchange. Typically, this is publisher.id in OpenRTB and the publisher's organization ID in OpenDirect. Limit this value to 64 characters in length. |
| `ext.schain.nodes.rid` | `source.schain.nodes.rid` | string | The OpenRTB RequestId issued by this seller for the request. |
| `ext.schain.nodes.hp` | `source.schain.nodes.hp` | integer | Indicates whether this node participates in the payment flow for the inventory. When set to 1, the advertising system in the asi field pays the seller in the sid field, who is then responsible for paying the previous node in the chain. When set to 0, this node does not participate in the payment flow for the inventory. For SupplyChain version 1.0, this property should always be 1. Implementers must ensure they propagate this field when constructing SupplyChain objects in bid requests sent to downstream advertising systems. |
| `device.ext.sua` | `device.sua` | UserAgent object | The bid request includes structured user agent information defined by the UserAgent object. If both ua and sua are provided, sua should be prioritized as it offers a more accurate representation of the device attributes. This preference is due to the possibility that ua may contain a frozen or truncated UserAgent string. |
| `device.ext.user_agent_data.browsers` | `UserAgent.browsers` | array of BrandVersion objects | Each BrandVersion object identifies a browser or similar software component. Implementers must transmit brands and versions obtained from the Sec-CH-UA-Full-Version-List header. See [BrandVersion](https://github.com/InteractiveAdvertisingBureau/openrtb2.x/blob/main/2.6.md#objectbrandversion) for detailed information.|
| `device.ext.user_agent_data.platform` | `UserAgent.platform` | BrandVersion object | The BrandVersion object, outlined in [BrandVersion](https://github.com/InteractiveAdvertisingBureau/openrtb2.x/blob/main/2.6.md#objectbrandversion), serves to identify the execution platform or operating system (OS) of the user agent. To ensure accurate transmission of this information, implementers are advised to follow specific guidelines when handling headers related to user agent platform details. <br> **Identifying the Brand and Version:** <br> - **Brand (Platform):** Extract the brand information from the Sec-CH-UA-Platform header. This header typically contains data that specifies the platform or OS type. <br> - **Version (Platform Version):** Extract the version information from the Sec-CH-UA-Platform-Version header. This header provides the specific version number associated with the platform or OS. |
| `device.ext.user_agent_data.mobile` | `UserAgent.mobile` | integer | The value indicating whether the agent prefers a "mobile" version of the content, if available, optimized for small screens or touch input, should be derived from the Sec-CH-UA-Mobile header. |
| `device.ext.user_agent_data.architecture` | `UserAgent.architecture` | string | Retrieve the device's major binary architecture, such as "x86" or "arm", from the Sec-CH-UA-Arch header. Implementers must extract this value to identify the primary architecture of the user agent's device |
|`device.ext.user_agent_data.bitness` | `UserAgent.bitness` | string | Retrieve the device's bitness, such as "64" for 64-bit architecture, from the Sec-CH-UA-Bitness header. Implementers must extract this value to determine the bitness of the user agent's device. |
| `device.ext.user_agent_data.model` | `UserAgent.model` | string | Retrieve the device model from the Sec-CH-UA-Model header. Implementers must extract this value to identify the specific model of the user agent's device. |
| `device.ext.user_agent_data.browsers.brand` |  `BrandVersion.brand` | string | The brand identifier, such as "Chrome" or "Windows", originates from the User-Agent Client Hints headers. It represents either the user agent brand, extracted from the Sec-CH-UA-Full-Version header, or the platform brand, derived from the Sec-CH-UA-Platform header. |
| `device.ext.user_agent_data.browsers.version` | `BrandVersion.version` | array of string | It comprises a sequence of version components arranged in descending hierarchical order: major, minor, micro, and so forth. |
| `user.ext.consent` | `user.consent` | string | When GDPR regulations are in effect, this attribute holds the Transparency and Consent Framework's Consent String data structure. |
| `user.ext.eids` | `user.eids` | object array | This section details the support of a standard protocol for multiple third-party identity providers. See [Object: EID](#object-eid) for more details. |
| `user.ext.eids.source` | `EID.source` | string | The source or technology provider responsible for the set of included IDs is represented as a top-level domain. |
| `user.ext.eids.uids` | `EID.uids` | object array | It consists of an array of extended ID UID objects sourced from the specified origin. [Object UID](https://github.com/InteractiveAdvertisingBureau/openrtb2.x/blob/main/2.6.md#3228---object-uid-) for more details. |
| `user.ext.eids.uids.id` | `UID.id` | string | This represents the user's identifier. |
