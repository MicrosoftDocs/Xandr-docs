---
title: Bid Landscape Feed
description: In this article, find information about the Bid landscape feed and details about the columns associated with this data feed.
ms.custom: log-level-data
ms.date: 10/28/2023
---

# Bid landscape feed

> [!IMPORTANT]
> This feed is not available to Microsoft Invest clients.

The Log-Level Bid Landscape Feed helps you gain insight into the demand for your inventory based on auctions involving a randomly selected set of 1% of the users on our platform. This feed contains the top fifteen bids, with one row per bid. This includes the winning bid. Please note that the winning bid may or may not have been the highest bid due to your ad quality or yield management settings.

> [!NOTE]
> Each user is randomly and evenly assigned to one of the 1000 separate user groups; once assigned to a group, a user stays in that group. This log covers auctions for users with a `user_group_id` that is less than or equal to 10. We track the timestamp and auction ID for each.

The Xandr internal name for this feed is `bid_landscape_feed`.

## Scope

Both eligible and ineligible bids from external bidders are covered by this feed, but only eligible bids from Xandr's bidder are covered. This is because bids from external bidders are checked against the seller's ad quality settings after the bids are sent, whereas bids from Xandr's bidder (`bidder_id` 2) are checked against the seller's ad quality settings before the bids are sent. Therefore, bids reported for `bidder_id` 2 will always have been eligible and will usually be shown with `bid_reject_reason` 0.

## Sequence

The columns below are listed in the same order in which they appear in the log-level feed file (top to bottom here, left to right in the file).

## Integer key

- tinyint = 1 byte (8 bit)
- smallint = 2 byte (16 bit)
- int = 4 byte (32 bit)
- bigint = 8 byte (64 bit)

## Columns

> [!NOTE]
> Microsoft Advertising may need to remove values for certain log level data (LLD) fields in order to comply with current data sharing restrictions.

| Column Index | Column Name | Type | Description |
|---|---|---|---|
| 01 | date_time | UNIX Epoch time | The date and time of the bid (e.g., `1526057561` which would need to be translated to *Friday, May 11, 2018 4:52:41 PM (UTC)*). |
| 02 | auction_id_64 | bigint | The ID of the Xandr auction that included the bid. |
| 03 | user_id_64 | bigint | The ID of the user associated with the bid. |
| 04 | brand_id | int | The ID of the brand for the creative that was bid. |
| 05 | creative_id | int | The ID of the creative that was bid. |
| 06 | actual_bid_price | numeric | The actual price of the bid (in USD), net of Xandr fees.<br> For fixed price deals, this field will contain the value that was used for price ranking in the auction. Buyer bid price will be in `raw_net_bid_price`. |
| 07 | biased_bid_price | numeric | The biased price of the bid (in USD), if yield management biases were applied to the buyer. |
| 08 | bid_reject_reason | tinyint | The reason that the bid was rejected. See [Bid Reject Codes](#bid-reject-codes) below. |
| 09 | ym_floor_id | int | The ID of the yield management floor that was applied to the buyer, if any. |
| 10 | ym_bias_id | int | The ID of the yield management bias that was applied to the buyer, if any. |
| 11 | bidder_id | int | The ID of the bidder. |
| 12 | buyer_member_id | int | The ID of the buying member. |
| 13 | seller_member_id | int | The ID of the selling member. |
| 14 | total_bid_modifier | numeric | The total amount added to or deducted from the bid due to yield management biases and/or modifiers, if any. |
| 15 | exclusivity_level | tinyint | When the impbus determines the winning bid for the auction, bids with higher values get precedence over bids with lower values. Sellers can use this information to run auction simulations. Allowed values: <br> - `0` = Learn bid on a non-prefer learn impression or give up bid <br> - `1` = Non exclusive <br> - `2` = Exclusive <br> - `3` = Learn bid on a prefer-learn impression |
| 16 | ym_auction_tier_id | int | If applicable, the ID of the Yield Management Auction Tier into which this bid was categorized. Tiers have a priority, and bids in tiers of higher priority get preference over bids in tiers of lower priority. Sellers can use this information to run auction simulations. For more information, see the [Yield Management Auction Tier Service](../digital-platform-api/yield-management-auction-tier-service.md). |
| 17 | hard_floor | numeric | The hard floor specified in the seller's [Yield Management Profile](../digital-platform-api/yield-management-profile-service.md), in the currency set by the publisher. Defaults to `0` if there was no hard floor on the Yield Management profile. |
| 18 | modified_hard_floor | numeric | The floor actually applied in the auction in USD. This can differ from the value of `hard_floor` due to floor optimization and floor modifiers. Defaults to `0` if there was no hard floor applied in the auction. |
| 19 | soft_floor | numeric | The soft floor (in the seller's local currency) specified in the seller's [Yield Management Profile](../digital-platform-api/yield-management-profile-service.md). Defaults to `0` if there was no soft floor on the Yield Management profile. |
| 20 | modified_soft_floor | numeric | The soft floor (in USD) that is actually supplied in the auction. This can differ from the value in `soft_floor` due to floor optimization and floor modifiers. Defaults to `0` if there was no soft floor applied in the auction. |
| 21 | bid_payment_type | tinyint | How the buyer was to have paid for the impression:<br> - `0` = CPM <br> - `1` = CPC or CPA <br> Defaults to `0`. |
| 22 | is_winning_bid | tinyint | Whether this bid won the impression: <br> - `0` = no <br> - `1` = yes |
| 23 | deal_id | int | The ID of the [deal](../digital-platform-api/deal-service.md) that was used to coordinate this bid on your inventory. Defaults to `0` if no deal was used. |
| 24 | ad_profile_id | int | The publisher-level [ad profile ID](../digital-platform-api/ad-profile-service.md) that was applied to this impression. This is used during bid rejection analysis to let the seller know which ad profile allowed or blocked the creative. Defaults to `0` if no publisher-level ad profile was used. Note that this value will never be the global ad profile. |
| 25 | is_mediated_bid | tinyint | Whether this bid is coming from mediated demand: <br> - `0` = standard <br> - `1` = mediation |
| 26 | raw_net_bid_price | numeric | The buyer's bid converted to USD less the buyer and seller deductions. <br> This value will be identical to the `actual_bid_price` value unless fixed price deals are in place. For a fixed price deal, the `raw_net_bid_price` is the actual bid from the buyer. |
| 27 | external_request_id | string (100) | Specifies the seller's own auction ID that ties the impression back to their own data feeds. (See `external_request_id` under [Standard Feed](standard-feed.md).) |
| 28 | bid_price_type | int | The type of bid price that was used to bid on this impression: <br> - `0 - BID_RESPONSE_TYPE_CPM`: A standard or "regular" CPM bid price. <br> - `1 - BID_RESPONSE_TYPE_PCPM`: A bid price from a Guaranteed Delivery line item with an impression goal. For more information about the available goal types for these line items, see [Guaranteed Delivery](../monetize/guaranteed-delivery.md). <br> - `2 - BID_RESPONSE_TYPE_LEARN`: A "learn" bid price from a buy-side object that was trying to optimize. For more information about learn bids from a buy-side perspective, see [Targeted Learn](../monetize/targeted-learn.md). <br> - `3 - BID_RESPONSE_TYPE_CPVM`: A bid price where buyers pay only for impressions that are measured “viewable”. See [vCPM Payment Type](../monetize/vcpm-payment-type.md) for more information. |
| 29 | hashed_user_id_64 | bytes | The hashed version of the Xandr 64-bit User ID which will we provided as a proxy in certain cases where Xandr is unable to provide the real `user_id_64`. You will not be able to target users via their hashed user ID. However you can use this identifier to calculate unique users, user frequency, and user recency. An example is provided below: <br> `user_id_64:` <br> `XXXXXX304391387YYYY` <br> `hashed_user_id_64:` <br> `0000f47b074866470613d9397f0bd7efa78c7adec992aac5e117cbe2d55993a94767` <br><br> **Note**: If you receive the `user_id_64` version of this field, you will not received the hashed version. |
| 30 | partition_time_millis | UNIX Epoch time | The hourly partition any record row falls into, represented as a UNIX Epoch timestamp value (in milliseconds). Useful for defining hourly partitions when loading into a database or data warehouse. For the Avro format, this field is given the timestamp-millis logical type for native timestamp detection. For example, `1568077200000` can also be represented as *Tuesday, September 10, 2019 1 AM (UTC)*. |

## Bid reject codes

The following codes appear in the `bid_reject_reason` column to indicate why a bid was rejected.

| Code | NEC (Notify Error Code) | Code | BRR (Bid Reject Reason) | Description |
|--|--|--|--|--|
| `0` | NEC_UNKNOWN | `900` | BRR_OTHER | Unknown error |
| `10` | NEC_REQUEST_TIMEOUT | `202` | BRR_REQUEST_TIMEOUT | Request timed out |
| `11` | NEC_REQUEST_THROTTLED_ABORTED | `203` | BRR_REQUEST_THROTTLED_ABORTED | Request throttled or aborted |
| `12` | NEC_CONNECTION_ERROR | `204` | BRR_CONNECTION_ERROR | Connection error |
| `13` | NEC_INV_HTTP_CODE | `205` | BRR_INV_HTTP_CODE | Invalid HTTP response code |
| `14` | NEC_JSON_PARSING_ERROR | `206` | BRR_JSON_PARSING_ERROR | JSON parsing error |
| `15` | NEC_XML_PARSING_ERROR | `207` | BRR_XML_PARSING_ERROR | XML parsing error |
| `16` | NEC_BID_RESPONSE_PARSING_ERROR | `208` | BRR_BID_RESPONSE_PARSING_ERROR | Bid response parsing error |
| `50` | NEC_NO_AD_TAG_IN_RESP | `209` | BRR_NO_AD_TAG_IN_RESP | No ad tag in response |
| `51` | NEC_NO_ACTIONS_TAG_IN_RESP | `210` | BRR_NO_ACTIONS_TAG_IN_RESP | No actions tag in response |
| `52` | NEC_NO_IMPURL_TAG_IN_RESP | `211` | BRR_NO_IMPURL_TAG_IN_RESP | No impurl tag in response |
| `53` | NEC_NO_CLICK_ACTION_IN_RESP | `212` | BRR_NO_CLICK_ACTION_IN_RESP | No click action in response |
| `54` | NEC_NO_ASSETS_TAG_IN_RESP | `213` | BRR_NO_ASSETS_TAG_IN_RESP | No assets tag in response |
| `55` | NEC_BAD_CR_FORMAT_IN_RESP | `214` | BRR_BAD_CR_FORMAT_IN_RESP | Incorrect creative format in response |
| `60` | NEC_RESP_TOO_LONG | `215` | BRR_RESP_TOO_LONG | Response too long |
| `61` | NEC_NO_PRICE | `216` | BRR_NO_PRICE | No price received from bidder |
| `62` | NEC_NO_CREATIVE_ID | `217` | BRR_NO_CREATIVE_ID | No creative id received from bidder |
| `63` | NEC_BAD_LANDING_PAGE | `218` | BRR_BAD_LANDING_PAGE | Invalid creative landing page received from bidder |
| `64` | NEC_NO_DROP_LOG_URL | `219` | BRR_NO_DROP_LOG_URL | No drop log url received from bidder |
| `102` | NEC_CREATIVE_NOT_FOUND | `503` | BRR_CREATIVE_NOT_FOUND | Creative was not found |
| `103` | NEC_CREATIVE_MALICIOUS | `504` | BRR_CREATIVE_MALICIOUS | Creative is malicious |
| `104` | NEC_CREATIVE_NOT_SSL | `501` | BRR_CREATIVE_NOT_SSL | Creative is not ssl_approved for a secure auction |
| `105` | NEC_CREATIVE_NOT_OWNED | `505` | BRR_CREATIVE_NOT_OWNED | Creative does not belong to response member |
| `106` | NEC_CREATIVE_WRONG_SIZE | `506` | BRR_CREATIVE_WRONG_SIZE | Creative size doesn't match tag sizes |
| `107` | NEC_CREATIVE_NOT_VAST | `507` | BRR_CREATIVE_NOT_VAST | Creative not in VAST format |
| `108` | NEC_CREATIVE_HASNT_VAST_SUBTYPE | `508` | BRR_CREATIVE_HASNT_VAST_SUBTYPE | Creative does not have VAST media subtype for VAST tag |
| `109` | NEC_CREATIVE_HAS_VAST_SUBTYPE | `509` | BRR_CREATIVE_HAS_VAST_SUBTYPE | Creative has VAST media_subtype for non-VAST tag |
| `110` | NEC_CREATIVE_HAS_FLASH | `510` | BRR_CREATIVE_HAS_FLASH | Flash creative returned for user that doesn't have flash |
| `111` | NEC_CREATIVE_BAD_FORMAT | `511` | BRR_CREATIVE_BAD_FORMAT | Creative format is not allowed by site |
| `112` | NEC_CREATIVE_BAD_CLICK_ACTION | `512` | BRR_CREATIVE_BAD_CLICK_ACTION | Creative click action is not allowed by site |
| `113` | NEC_CREATIVE_BAD_MEDIA_TYPE | `513` | BRR_CREATIVE_BAD_MEDIA_TYPE | Creative has an invalid media type |
| `114` | NEC_CREATIVE_INITIATES_POP | `514` | BRR_CREATIVE_INITIATES_POP | Creative initiates pop |
| `115` | NEC_CREATIVE_MISSING_CLICK | `515` | BRR_CREATIVE_MISSING_CLICK | Creative has no click url |
| `116` | NEC_CREATIVE_NO_LANDING_PAGE | `516` | BRR_CREATIVE_NO_LANDING_PAGE | Creative has no landing page url |
| `117` | NEC_CREATIVE_BANNED | `517` | BRR_CREATIVE_BANNED | Creative is banned by bid_request |
| `118` | NEC_CREATIVE_BAD_CCRT | `518` | BRR_CREATIVE_BAD_CCRT | Creative has an inactive or non-existent CCRT |
| `119` | NEC_CREATIVE_TEMPLATE_HAS_NO_CONTENT_JS | `519` | BRR_CREATIVE_TEMPLATE_HAS_NO_CONTENT_JS | Creative has no content js in template for JS tag |
| `120` | NEC_CREATIVE_TEMPLATE_HAS_NO_CONTENT_JS_OR_HTML | `520` | BRR_CREATIVE_TEMPLATE_HAS_NO_CONTENT_JS_OR_HTML | Creative has no content js or html in template for IFRAME tag |
| `121` | NEC_CREATIVE_TEMPLATE_HAS_NO_CONTENT_XML | `521` | BRR_CREATIVE_TEMPLATE_HAS_NO_CONTENT_XML | Creative has no content xml in template for VAST tag |
| `122` | NEC_CREATIVE_NOT_ALLOWED_BY_SELLER | `522` | BRR_CREATIVE_NOT_ALLOWED_BY_SELLER | Creative with format is not allowed by seller |
| `123` | NEC_CREATIVE_FAIL_ADVERTISER_EXCLUSION | `902` | BRR_OTHER_ADVERTISER_EXCLUSION | Creative fails advertiser exclusion |
| `124` | NEC_CREATIVE_BAD_MIMES | `523` | BRR_CREATIVE_BAD_MIMES | Creative does not have valid MIME type |
| `125` | NEC_CREATIVE_SUSPICIOUS | `524` | BRR_CREATIVE_SUSPICIOUS | Creative is suspicious |
| `126` | NEC_CREATIVE_MEDIATION_NOT_SUPPORTED | `525` | BRR_CREATIVE_MEDIATION_NOT_SUPPORTED | Mediated creative is not supported |
| `127` | NEC_CREATIVE_LEGACY_VAST_NOT_SUPPORTED | `526` | BRR_CREATIVE_LEGACY_VAST_NOT_SUPPORTED | Legacy vast creative is not supported |
| `128` | NEC_CREATIVE_BAD_VIDEO_PROTOCOL | `527` | BRR_CREATIVE_BAD_VIDEO_PROTOCOL | Creative requires a vast version that is not supported by the placement |
| `129` | NEC_NATIVE_WRONG_CREATIVE_ID | `528` | BRR_NATIVE_WRONG_CREATIVE_ID | Native assets point to wrong creative instead of creative |
| `130` | NEC_NATIVE_MISSING_ASSET_DATA | `529` | BRR_NATIVE_MISSING_ASSET_DATA | Native creative does not match title or data asset requirements |
| `131` | NEC_NATIVE_MISSING_ASSET_IMAGE | `530` | BRR_NATIVE_MISSING_ASSET_IMAGE | Native creative does not match image asset requirements |
| `132` | NEC_NATIVE_NO_VALID_ASSET | `531` | BRR_NATIVE_NO_VALID_ASSET | Native creative has no valid data for any assets |
| `133` | NEC_NATIVE_NOT_RENDERABLE | `532` | BRR_NATIVE_NOT_RENDERABLE | Native creative is not renderable |
| `134` | NEC_CREATIVE_BAD_CONTENT_SOURCE | `533` | BRR_CREATIVE_BAD_CONTENT_SOURCE | Creative comes from bad source |
| `135` | NEC_NATIVE_MISSING_ASSET_VIDEO | `534` | BRR_NATIVE_MISSING_ASSET_VIDEO | Native creative does not match video asset requirements |
| `136` | NEC_CREATIVE_MISSING_ELEMENT | `535` | BRR_CREATIVE_MISSING_ELEMENT | Creative missing element(s) |
| `137` | NEC_CREATIVE_INACTIVE | `536` | BRR_CREATIVE_INACTIVE | Creative is inactive |
| `138` | NEC_CREATIVE_GDPR_MISSING_VENDOR | `556` | BRR_CREATIVE_GDPR_MISSING_VENDOR | Creative has one or more unrecognized vendor(s) |
| `139` | NEC_CREATIVE_GDPR_UNAPPROVED_VENDOR | `557` | BRR_CREATIVE_GDPR_UNAPPROVED_VENDOR | Creative has one or more vendor(s) lacking user consent |
| `158` | NEC_CREATIVE_IGNORE_BY_DEBUG_SETTING | `579` | BRR_CREATIVE_IGNORE_BY_DEBUG_SETTING | Creative is ignored from the rtp_debug_settings |
| `171` | NEC_CURATED_DEAL_BRAND_BANNED | `356` | BRR_BLOCKED_BY_CURATED_DEAL_BRAND | Creative brand banned on curated deal |
| `172` | NEC_CURATED_DEAL_CATEGORY_BANNED | `357` | BRR_BLOCKED_BY_CURATED_DEAL_CATEGORY | Creative category banned on curated deal |
| `173` | NEC_CURATED_DEAL_ADSERVER_BANNED | `358` | BRR_BLOCKED_BY_CURATED_DEAL_ADSERVER | Creative adserver banned on curated deal |
| `174` | NEC_CURATED_DEAL_LANGUAGE_BANNED | `359` | BRR_BLOCKED_BY_CURATED_DEAL_LANGUAGE | Creative language banned on curated deal |
| `175` | NEC_CURATED_MEMBER_BRAND_BANNED | `360` | BRR_BLOCKED_BY_CURATED_MEMBER_BRAND | Creative brand banned on curator member |
| `176` | NEC_CURATED_MEMBER_CATEGORY_BANNED | `361` | BRR_BLOCKED_BY_CURATED_MEMBER_CATEGORY | Creative category banned on curator member |
| `177` | NEC_CURATED_MEMBER_ADSERVER_BANNED | `362` | BRR_BLOCKED_BY_CURATED_MEMBER_ADSERVER | Creative adserver banned on curator member |
| `178` | NEC_CURATED_MEMBER_LANGUAGE_BANNED | `363` | BRR_BLOCKED_BY_CURATED_MEMBER_LANGUAGE | Creative language banned on curator member |
| `179` | NEC_BID_DSA_TRANSPARENCY_FAIL | `422` | BRR_BID_DSA_TRANSPARENCY_FAIL | Bid rejected due to failing transparency check |
| `201` | NEC_RESP_WRONG_AUCTION_ID | `220` | BRR_RESP_WRONG_AUCTION_ID | Auction ID does not match request |
| `202` | NEC_MEMBER_MISSING | `221` | BRR_MEMBER_MISSING | No member ID sent in response |
| `203` | NEC_MEMBER_INACTIVE | `222` | BRR_MEMBER_INACTIVE | Inactive member |
| `204` | NEC_MEMBER_NO_CONTRACT | `223` | BRR_MEMBER_NO_CONTRACT | Member has no contract |
| `205` | NEC_MEMBER_NO_BUDGET | `224` | BRR_MEMBER_NO_BUDGET | Member safety budget |
| `207` | NEC_BIDDER_NON_OWNING | `225` | BRR_BIDDER_NON_OWNING | Exclusive bid from non-owning bidder |
| `208` | NEC_MEMBER_NOT_IN_BIDDER | `226` | BRR_MEMBER_NOT_IN_BIDDER | Bid from member not associated to bidder |
| `209` | NEC_INVALID_ROADBLOCK | `227` | BRR_INVALID_ROADBLOCK | Roadblock bid from non-owning member |
| `210` | NEC_MEMBER_NOT_ELIGIBLE | `228` | BRR_MEMBER_NOT_ELIGIBLE | Member is not eligible to bid |
| `211` | NEC_DEAL_MISSING | `229` | BRR_DEAL_MISSING | Member is not eligible to bid without deals |
| `301` | NEC_NO_PRICE_NONEXCLUSIVE | `230` | BRR_NO_PRICE_NONEXCLUSIVE | No price set on non-exclusive bid response |
| `302` | NEC_INVALID_CURRENCY | `231` | BRR_INVALID_CURRENCY | Bid from member specifies an invalid currency |
| `304` | NEC_NEGATIVE_BID | `400` | BRR_BELOW_FLOOR | Effective revenue share less than 0 |
| `306` | NEC_BID_BELOW_RESERVE | `400` | BRR_BELOW_FLOOR | Net bid was lower than reserve price |
| `347` | NEC_BELOW_FLOOR_YM | `401` | BRR_BELOW_FLOOR_YM | Bid is below yield management floor price. |
| `307` | NEC_NO_CREATIVE_FOUND_BY_CODE | `537` | BRR_NO_CREATIVE_FOUND_BY_CODE | Creative expired or not found by code |
| `308` | NEC_DEAL_NOT_AVAILABLE | `201` | BRR_DEAL_NOT_AVAILABLE | Deal is not available for auction |
| `309` | NEC_DEAL_NO_MEMBER | `201` | BRR_DEAL_NOT_AVAILABLE | Deal is not available to buying member |
| `310` | NEC_DEAL_BELOW_FLOOR | `606` | BRR_BLOCKED_BY_DEAL_BELOW_FLOOR | Bid is below the deal floor |
| `311` | NEC_DEAL_BRAND_BANNED | `605` | BRR_BLOCKED_BY_DEAL_BRAND | Creative brand banned on deal |
| `312` | NEC_DEAL_INVALID_SIZE | `608` | BRR_BLOCKED_BY_DEAL_SIZE | Deal bans size |
| `313` | NEC_VIDEO_UNSUPPORTED_ATTRIBUTE | `538` | BRR_VIDEO_UNSUPPORTED_ATTRIBUTE | Creative has unsupported video attribute |
| `314` | NEC_FAIL_MIN_DURATION | `539` | BRR_FAIL_MIN_DURATION | Creative duration fails minimum duration |
| `315` | NEC_FAIL_MAX_DURATION | `540` | BRR_FAIL_MAX_DURATION | Creative duration exceeds maximum duration |
| `316` | NEC_VAST_MISSING_LINEAR_ELEMENT | `541` | BRR_VAST_MISSING_LINEAR_ELEMENT | Creative is missing a linear element required for VAST |
| `317` | NEC_VIDEO_MISSING_ATTRIBUTE | `542` | BRR_VIDEO_MISSING_ATTRIBUTE | Creative is missing a video_attributes object |
| `318` | NEC_DEAL_SEGMENT_ADDS_NOT_ALLOWED_VIEW | `901` | BRR_OTHER_DATA_PROTECTION | Deal bans segment adds on view |
| `319` | NEC_DEAL_SEGMENT_ADDS_NOT_ALLOWED_CLICK | `901` | BRR_OTHER_DATA_PROTECTION | Deal bans segment adds on click |
| `320` | NEC_FAIL_VIDEO_FRAMEWORK | `543` | BRR_FAIL_VIDEO_FRAMEWORK | Creative video framework is not supported |
| `321` | NEC_SPEND_PROTECT_INELIGIBLE | `900` | BRR_OTHER | Auction is not spend protection eligible |
| `322` | NEC_DEAL_LANGUAGE_BANNED | `602` | BRR_BLOCKED_BY_DEAL_LANGUAGE | Creative language banned on deal |
| `323` | NEC_DEAL_TECHNICAL_ATTRIBUTE_BANNED | `603` | BRR_BLOCKED_BY_DEAL_TECHNICAL_ATTRIBUTE | Creative technical attribute banned on deal |
| `324` | NEC_DEAL_CREATIVE_BANNED | `601` | BRR_BLOCKED_BY_DEAL_CREATIVE | Creative banned on deal |
| `325` | NEC_DEAL_CATEGORY_BANNED | `604` | BRR_BLOCKED_BY_DEAL_CATEGORY | Creative category banned on deal |
| `326` | NEC_DEAL_BAD_MEDIA_TYPE | `607` | BRR_BLOCKED_BY_DEAL_MEDIA_SUBTYPE | Deal does not have supported media (sub)type for creative |
| `327` | NEC_DEAL_INVALID_PAYMENT_TYPE | `609` | BRR_BLOCKED_BY_DEAL_PAYMENT_TYPE | Deal does not support bid payment type |
| `328` | NEC_SPEND_PROTECT_INVALID_ID | `900` | BRR_OTHER | Spend protection pixel ID invalid |
| `329` | NEC_FAIL_BITRATE | `544` | BRR_FAIL_BITRATE | Creative does not have bitrate in range |
| `330` | NEC_VAST_UNKNOWN_TYPE | `545` | BRR_VAST_UNKNOWN_TYPE | Creative has creative_video_attribute with vast_type unrecognized by impbus |
| `331` | NEC_VAST_MISSING_INLINE | `546` | BRR_VAST_MISSING_INLINE | Creative is missing creative_vast_inline required for VAST |
| `332` | NEC_VAST_MISSING_INLINE_LINEAR | `547` | BRR_VAST_MISSING_INLINE_LINEAR | Creative is missing creative_vast_inline_linear required for VAST |
| `333` | NEC_VAST_MISSING_INLINE_LINEAR_MEDIA | `548` | BRR_VAST_MISSING_INLINE_LINEAR_MEDIA | Creative is missing creative_vast_inline_linear media_files required for VAST |
| `334` | NEC_VAST_MISSING_DURATION | `549` | BRR_VAST_MISSING_DURATION | Creative does not have a specified duration required for inline VAST |
| `334` | NEC_DEAL_ADSERVER_BANNED | `610` | BRR_BLOCKED_BY_DEAL_ADSERVER | Creative ad-server banned on deal |
| `335` | NEC_INVALID_PAYMENT_TYPE | `232` | BRR_INVALID_PAYMENT_TYPE | Invalid payment type |
| `336` | NEC_VIEWABILITY_DETECTION_DISABLED | `233` | BRR_VIEWABILITY_DETECTION_DISABLED | Viewability detection required for view payment |
| `337` | NEC_ETV_DISABLED | `234` | BRR_ETV_DISABLED | Exchange traded view marketplace is disabled for member |
| `338` | NEC_VAST_MISSING_VIDEO | `550` | BRR_VAST_MISSING_VIDEO | Creative is missing video required for VAST |
| `339` | NEC_FAIL_MEDIA_FILE_WIDTH | `551` | BRR_FAIL_MEDIA_FILE_WIDTH | Creative does not have a media file that meets width requirements |
| `340` | NEC_FAIL_MEDIA_FILE_HEIGHT | `552` | BRR_FAIL_MEDIA_FILE_HEIGHT | Creative does not have a media file that meets height requirements |
| `341` | NEC_FAIL_MEDIA_FILE_MIN_WIDTH | `553` | BRR_FAIL_MEDIA_FILE_MIN_WIDTH | Creative does not have a media file that meets minimum width requirements |
| `342` | NEC_FAIL_MEDIA_FILE_MIN_HEIGHT | `554` | BRR_FAIL_MEDIA_FILE_MIN_HEIGHT | Creative does not have a media file that meets minimum height requirements |
| `343` | NEC_FAIL_MEDIA_FILE_ASPECT_RATIO | `555` | BRR_FAIL_MEDIA_FILE_ASPECT_RATIO | Creative does not have a media file that meets aspect ratio requirements |
| `347` | NEC_BELOW_FLOOR_YM | `401` | BRR_BELOW_FLOOR_YM | Bid is below the ym_floor price |
| `348` | NEC_CURATION_DISALLOWED_FOR_GO_BID | `614` | BRR_CURATION_DISALLOWED_FOR_GO_BID | Guaranteed outcome bids are not allowed on curated deals |
| `349` | NEC_DEAL_FAIL_ADVERTISER_EXCLUSION | `615` | BRR_COMPETITIVE_EXCLUSION_BY_DEAL | Bid is rejected due to exclusion set on deal's advertiser |
| `350` | NEC_SELLER_DEAL_DISALLOWED_FOR_GO_BID | `616` | BRR_SELLER_DEAL_DISALLOWED_FOR_GO_BID | Guaranteed outcome bids are not allowed on seller deals |
| `403` | NEC_AD_PROFILE_MEMBER | `307` | BRR_BLOCKED_BY_AP_MEMBER | Buying member banned on member's ad profile |
| `404` | NEC_AD_PROFILE_CREATIVE | `301` | BRR_BLOCKED_BY_AP_CREATIVE | Creative banned on member's ad profile |
| `405` | NEC_AD_PROFILE_CR_UNAUDITED | `308` | BRR_BLOCKED_BY_AP_AUDIT_STATUS | Unaudited creative banned on member's ad profile |
| `406` | NEC_AD_PROFILE_CR_ATTRIBUTE | `303` | BRR_BLOCKED_BY_AP_TECHNICAL_ATTRIBUTE | Creative technical_attribute banned on member's ad profile |
| `407` | NEC_AD_PROFILE_CR_CATEGORY | `304` | BRR_BLOCKED_BY_AP_CATEGORY | Creative category banned on member's ad profile |
| `408` | NEC_AD_PROFILE_CR_BRAND | `305` | BRR_BLOCKED_BY_AP_BRAND | Creative brand banned on member's ad profile |
| `409` | NEC_AD_PROFILE_CR_LANGUAGE | `302` | BRR_BLOCKED_BY_AP_LANGUAGE | Creative language banned on member's ad profile |
| `410` | NEC_AD_PROFILE_CR_ADSERVER | `306` | BRR_BLOCKED_BY_AP_ADSERVER | Creative ad-server banned on member's ad profile |
| `411` | NEC_DYNAMIC_LANGUAGE_BANNED | `702` | BRR_BLOCKED_BY_DYNAMIC_LANGUAGE | Creative language banned on dynamic exclusions |
| `412` | NEC_DYNAMIC_TECHNICAL_ATTRIBUTE_BANNED | `703` | BRR_BLOCKED_BY_DYNAMIC_TECHNICAL_ATTRIBUTE | Creative technical attribute banned on dynamic exclusions |
| `413` | NEC_DYNAMIC_ADSERVER_BANNED | `700` | BRR_BLOCKED_BY_DYNAMIC_ADSERVER | Creative ad-server banned on dynamic exclusions |
| `414` | NEC_DYNAMIC_CATEGORY_BANNED | `704` | BRR_BLOCKED_BY_DYNAMIC_CATEGORY | Creative category banned on dynamic exclusions |
| `415` | NEC_DYNAMIC_BRAND_BANNED | `701` | BRR_BLOCKED_BY_DYNAMIC_BRAND | Creative brand banned on dynamic exclusions |
| `417` | NEC_AD_PROFILE_UNKNOWN_DYNAMIC_BRAND | `705` | BRR_AD_PROFILE_UNKNOWN_DYNAMIC_BRAND | Ad profile contains brand or category restrictions, and dynamic brand is unknown |
| `418` | NEC_AD_PROFILE_UNKNOWN_DYNAMIC_LANGUAGE | `706` | BRR_AD_PROFILE_UNKNOWN_DYNAMIC_LANGUAGE | Ad profile contains language restrictions, and dynamic language is unknown |
| `420` | NEC_CATEGORY_REQ_ALLOWLIST | `304` | BRR_BLOCKED_BY_AP_CATEGORY | Creative category requires allow-listing |
| `421` | NEC_BID_PAGE_CAPPED | `402` | BRR_PAGE_CAPPED | Bid is rejected due to page cap |
| `1000` | NEC_NO_MEMBERS | `235` | BRR_NO_MEMBERS | No eligible members |
| `1001` | NEC_BIDDER_UNAVAILABLE | `236` | BRR_BIDDER_UNAVAILABLE | Bidder not available |
| `1002` | NEC_NO_BID_URI | `237` | BRR_NO_BID_URI | No bid URI set |
