---
title: Integration with OpenRTB 2.6 Protocol For Supply Partners 
description: This page outlines how Xandr's supply partners integrate using the OpenRTB protocol. Xandr supports the OpenRTB 2.6 protocol for receiving impressions across all media types.
ms.custom: supply-partners
ms.date: 7/3/2025
---

# Integration with OpenRTB 2.6 protocol for supply partners

This page outlines how Xandr's supply partners integrate using the OpenRTB protocol. Xandr supports the OpenRTB 2.6 protocol for receiving impressions across all media types. This document highlights the top-level objects that have changes or updates, including new fields that are added or implemented. Additionally, it outlines the fields that have been transitioned from their previous location in OpenRTB 2.4/2.5 to their new location in OpenRTB 2.6.

## Implementation

To ensure seamless functionality and compatibility with the latest supply-side protocols, it is essential that all supply partners activate support for OpenRTB 2.6. This version introduces new fields and enhancements designed to improve auction efficiency, inventory transparency, and interoperability with demand partners.

<!-- ### Endpoint

To make OpenRTB 2.6 requests on the sell side, you must use the OpenRTB version header. The inclusion of this header is mandatory. If it is not included, the system will default to OpenRTB 2.4.

The header and version to use is:

```
x-openrtb-version : 2.6
```
-->

> [!NOTE]
>
> To use OpenRTB 2.6, supply partners must include the header value `x-openrtb-version: 2.6` in each request. Otherwise, the system defaults to version 2.4/2.5. No enablement is required to use the 2.6 header value.

## Top-level bid request object

The OpenRTB 2.6 protocol introduces several changes and updates to the top-level objects and their associated fields that were previously supported by OpenRTB 2.4. The following sections detail these changes and updates, outlining the specific objects and fields that have been modified or added as a part of the OpenRTB 2.6 implementation.

>[!NOTE]
> Any field(s) not listed here remains supported in its original location as documented in the [OpenRTB 2.4 protocol](incoming-bid-request-from-ssps.md).

| Field | Type | Description |
|:---|:---|:---|
|`imp`| array of objects | (Required). The impressions offered in this bid request. See [Impression Object](#impression-object) below. <br><br> **Note:** The `imp` is not a new field in the OpenRTB 2.6 protocol guide. It is included in this document solely as a reference to the `rwdd` field in the below [section](#impression-object). |

### Impression object

The `Imp` object defines an ad placement or impression being auctioned by the supply partner. A single bid request can include multiple `Imp` objects, which is useful for exchanges that support selling all ad positions on a given page. Each `Imp` object requires an ID, allowing bids to reference them individually.

>[!NOTE]
> Any field(s) not listed here remains supported in its original location as documented in the [OpenRTB 2.4 protocol](incoming-bid-request-from-ssps.md).

As a part of the OpenRTB 2.6 implementation, Xandr has added the following field(s) to the `Imp Object`. 

| Field | Type | Description |
|:---|:---|:---|
|`rwdd`| integer | This field indicates whether the user receives a reward for viewing the ad, with 0 representing "no" and 1 representing "yes." Typically, video ad implementations grant rewards such as access to an additional news article for free, an extra life in a game, or a sponsored ad-free music session. The reward is usually provided after the video ad is fully viewed. |
| `video` | object | This field is required if the impression is offered as a video ad. See [Video Object](#video-object) below. <br><br> **Note:** The `video` is not a new field in the OpenRTB 2.6 protocol guide. It is included in this document solely as a reference to the `plcmt` field in the below [section](#video-object). |

### Video object

The `Video` object represents a video impression. While many of its fields are non-essential for minimally viable transactions, they are included to provide fine control when necessary. Video in OpenRTB generally adheres to the VAST standard. Consequently, companion ads are supported by optionally including an array of `Banner` objects that define these companion ads. For more details, see [Banner object](https://github.com/InteractiveAdvertisingBureau/openrtb2.x/blob/main/2.6.md#326---object-banner-)

>[!NOTE]
> Any field(s) not listed here remains supported in its original location as documented in the [OpenRTB 2.4 protocol](incoming-bid-request-from-ssps.md).

As part of the OpenRTB 2.6 implementation, Xandr has added the following field(s) to the `Video` Object:

| Field | Type | Description |
|:---|:---|:---|
| `plcmt` | integer | The video placement type for the impression references the List: Plcmt Subtypes - Video in AdCOM 1.0. |

### Video ad pods

Starting in version 2.6, OpenRTB now supports "pod bidding" for video and audio content streams. An ad pod refers to an ad break, similar to those seen in TV or heard on radio, containing one or more in-stream creative assets that play sequentially within the content stream. OpenRTB 2.6 enhances previous versions' capabilities by allowing multiple ad requests within a single bid request, indicating they are related.

Pod bidding signals provide additional information about the pod and its impression opportunities, such as the sequence of ad impressions, total pod length, maximum number of ads per pod, multiple pod associations, and more.

#### Implementation caveat

We currently support all pod types on the sell side; however, on the buy side, all requests are converted to structured pods in bid requests sent to bidders. This is because our platform currently only processes structured pods.

As part of the OpenRTB 2.6 implementation, Xandr has added the following field(s) to the `Video` Object:

| Field | Type | Description |
|:---|:---|:---|
| `Video.podid` | string | Unique identifier indicating that an impression opportunity belongs to a video ad pod. If multiple impression opportunities within a bid request share the same `podid`, this indicates that those impression opportunities belong to the same video ad pod. |
| `Video.podseq` | integer <br> **Default**: `0` | The sequence (position) of the video ad pod within a content stream. For guidance on the use of this field, refer to in AdCOM 1.0. |
| `Video.rqddurs` | integer array | Precise acceptable durations for video creatives in seconds. This field specifically targets the Live TV use case where non-exact ad durations would result in undesirable 'dead air'. <br>This field is mutually exclusive with `minduration` and `maxduration`; if `rqddurs` is specified, `minduration` and `maxduration` must not be specified and vice versa. |
| `Video.slotinpod` | integer <br> **Default**: `0` | For video ad pods, this value indicates that the seller can guarantee delivery against the indicated slot position in the pod. For guidance on the use of this field, refer to List: Slot Position in Pod in AdCOM 1.0. |
| `plcmt` | integer | The video placement type for the impression references to the List: Plcmt Subtypes - Video in AdCOM 1.0. For further implementation guide, see [Use `Plcmt`, `Placement`, and `Context` fields together](#using-plcmt-placement-and-context-fields-together). |

### Using `Plcmt`, `Placement`, and `Context` fields together

The OpenRTB 2.6 specification replaces the `placement` field (`imp.video.placement`) from OpenRTB 2.4/2.5 with the `plcmt` field (`imp.video.plcmt`). However, some bidders may still use OpenRTB 2.4/2.5. To maximize demand sources, include both the `placement` and `plcmt` fields in your requests.

Refer to the table below to find the correct values. Start by comparing your OpenRTB 2.4/2.5 `placement` values with their corresponding "plcmt" fields in OpenRTB 2.6.

>[!NOTE]
> `Instream` placements are now divided into `Instream` and a new `Accompanying Content` value.

In addition to the `plcmt` and `placement` fields, include the `context` field in the AppNexus video extension object (`imp.video.ext.appnexus.context`) in your bid requests. This field provides crucial information about the video's position (e.g., pre-roll, mid-roll, or post-roll) that the `plcmt` or `placement` fields alone do not convey (see the "Xandr Extension" column below). Ensure your bid requests include all three fields.

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
| name | string | Network the content is on (e.g., a TV network like “ABC”). <br> **Note**: This field was previously supported through an extension of the **content object** in older OpenRTB versions. For more details, see [OpenRTB 2.4 documentation](../bidders/outgoing-bid-request-to-bidders.md).                 |
| domain| string | The primary domain of the network (e.g., “abc.com” for the network ABC). It is recommended to include the top private domain (PSL+1) for DSP targeting normalization purposes. |

## Object: Channel

This object describes the channel an ad will be displayed on. A Channel is defined as the entity that curates a content library or stream within a brand name for viewers. Examples are specific view-selectable "channels" within linear and streaming television (e.g., MTV, HGTV, CNN, BBC One) or a specific stream of audio content commonly called "stations."

The **name** is a human-readable field, while **domain** and **id** can be used for reporting and targeting purposes.

### Channel attributes

| **Attribute** | **Type** | **Description** |
|---------------|----------|-----------------|
| `id` | string   | A unique identifier assigned by the publisher. This may not be a unique identifier across all supply sources. |
| `name` | string   | Channel the content is on (e.g., a local channel like "WABC-TV"). |
| `domain`| string   | The primary domain of the channel (e.g., "abc7ny.com" in the case of the local channel WABC-TV). It is recommended to include the top private domain (PSL+1) for DSP targeting normalization purposes. |

## Object: UID

This object contains a single user identifier provided as part of extended identifiers.

| **Attribute** | **Type** | **Description** |
| --- | --- | --- |
| `id` | string | The identifier for the user. |
| `atype` | integer | Type of user agent the ID is from. It is highly recommended to set this, as many DSPs separate app-native IDs from browser-based IDs and require a type value for ID resolution. Refer to [List: Agent Types](https://github.com/InteractiveAdvertisingBureau/AdCOM/blob/master/AdCOM%20v1.0%20FINAL.md#list_agenttypes) in AdCOM 1.0 |


## Updated field locations

A number of fields have moved from the old location in OpenRTB 2.4/2.5 to the new location in OpenRTB 2.6.

>[!NOTE]
> Any field(s) not listed here remains supported in its original location as documented in the [OpenRTB 2.4 protocol] (incoming-bid-request-from-ssps.md).

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
| `user.ext.eids` | `user.eids` | object array | This section details the support of a standard protocol for multiple third-party identity providers. See [Object EID](https://github.com/InteractiveAdvertisingBureau/openrtb2.x/blob/main/2.6.md#objecteid) for more details. |
| `user.ext.eids.source` | `EID.source` | string | The source or technology provider responsible for the set of included IDs is represented as a top-level domain. |
| `user.ext.eids.uids` | `EID.uids` | object array | It consists of an array of extended ID UID objects sourced from the specified origin. [Object UID](https://github.com/InteractiveAdvertisingBureau/openrtb2.x/blob/main/2.6.md#3228---object-uid-) for more details. |
| `user.ext.eids.uids.id` | `UID.id` | string | This represents the user's identifier. |
