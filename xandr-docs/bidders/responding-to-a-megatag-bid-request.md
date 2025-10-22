---
title: Responding to a MegaTag Bid Request
description: In this article, find information about how a MegaTag auction works and how to respond to a multi-tag request.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Responding to a MegaTag bid request

> [!IMPORTANT]
>
> - **Not Supported**: The AppNexus Bidding Protocol is no longer supported; this documentation is for legacy purposes only. **We will deprecate this protocol on December 1, 2018.**
> - If you're a new bidder integrating with AppNexus, please see the [OpenRTB 2.4 Bidding Protocol](https://www.iab.com/wp-content/uploads/2016/03/OpenRTB-API-Specification-Version-2-4-FINAL.pdf).

MegaTag is a technology which consolidates all of the ad inventory on a webpage, enabling the impressions and associated metadata from multiple auctions to be combined into one bid request. Bidders can then submit a single response array containing bid information for all of the ad slots on the page to serve multiple creatives within a single page.

The documentation uses the term *ad slot* rather than *placement* to refer to the sized location on a page where an ad serves. This is because each time a user visits a page, he is faced with a single *placement*, which is comprised of multiple *ad slots.*

## How does MegaTag work

MegaTag is implemented as a client-side JavaScript program that runs in the user's browser. A MegaTag auction occurs as follows:

1. The Javascript generates a single ad request by gathering all of the ad slots to be auctioned. This ad request contains all pertinent information about each ad slot, including placement size.
1. The ad request is then sent to AppNexus to conduct a distinct auction for each of the ad slots within the placement.
1. AppNexus generates a single bid request which contains a unique auction for each ad slot on the page.
1. Bidders respond with a single bid response that contains separate bid information for each auction within a responses array.
1. Once AppNexus has completed all auctions for the placement, MegaTag generates iFrames on the publisher's page where all ad slots will be populated with the winning creatives.
1. These "friendly" iFrames are then dynamically injected into the HTML code of the publisher's page.

See [MegaTag Technical Overview](megatag-technical-overview.md), for additional information.

## When would I bid on a MegaTag auction

Advertisers often wish to run multiple advertisements on a single web page to:

- Ensure that only one expandable, audio, or video ad is displayed during a single page view on a publisher's site and how frequently they can serve.

- Ensure that advertisements from competitive brands (e.g., Coke and Pepsi) never serve alongside each other.

- Serve multiple creatives together as part of a roadblock.

- Apply a frequency cap of 1 impression per page for an advertiser, line item, or campaign.

## How do I respond to a multi-tag request

One MegaTag bid request will contain unique auction IDs for each ad slot on the page within the tags array element. Your bidder can then provide a single bid response that contains an array of response elements. Each response element must contain bid information for a distinct ad slot.

MegaTag is utilized by select premium sellers. Therefore, your bidder should be configured to loop through the tags array in a bid request for these select sellers.

## Examples

### Example multi-tag request

```
{
    "bid_request": {
        "timestamp": "2013-02-13 17:07:54",
        "bidder_timeout_ms": 100,
        "members": [
            {
                "id": 1143
            },
            {
                "id": 1323
            },
            {
                "id": 1440
            }
        ],
        "member_ad_profile_id": 19042,
        "tags": [
            {
                "auction_id_64": 3476552926870226000,
                "size": "300x250",
                "sizes": [
                    "300x250",
                    "250x250",
                    "300x600"
                ],
                "smaller_sizes_allowed": false,
                "position": "above",
                "tag_format": "javascript",
                "site_id": 190350,
                "creative_formats_map": "1111111110",
                "creative_formats": [
                    "unknown",
                    "html-url",
                    "js-url",
                    "flash",
                    "image",
                    "js-raw",
                    "html-raw",
                    "html-iframe",
                    "vast-url"
                ],
                "ad_profile_id": 203694,
                "ad_profiles": [
                    203694
                ],
                "visibility_profile_id": 156,
                "venue_id": 83202,
                "allowed_media_types": [
                    1
                ],
                "media_subtypes": [
                    "banner"
                ],
                "estimated_clear_price": 1.056,
                "estimated_average_price": 0.352,
                "id": 597879,
                "inventory_audits": [
                    {
                        "auditor_member_id": 1167,
                        "intended_audience": "general",
                        "inventory_attributes": [
                            14
                        ],
                        "content_categories": [
                            8416
                        ]
                    }
                ]
            },
            {
                "auction_id_64": 7415314500030035000,
                "size": "1x1",
                "sizes": [
                    "1x1"
                ],
                "smaller_sizes_allowed": false,
                "position": "above",
                "tag_format": "javascript",
                "site_id": 190350,
                "creative_formats_map": "1111111110",
                "creative_formats": [
                    "unknown",
                    "html-url",
                    "js-url",
                    "flash",
                    "image",
                    "js-raw",
                    "html-raw",
                    "html-iframe",
                    "vast-url"
                ],
                "ad_profile_id": 203694,
                "ad_profiles": [
                    203694
                ],
                "visibility_profile_id": 156,
                "venue_id": 83202,
                "allowed_media_types": [
                    3,
                    8
                ],
                "media_subtypes": [
                    "banner"
                ],
                "estimated_clear_price": 1,
                "estimated_average_price": 0.5,
                "id": 597880,
                "inventory_audits": [
                    {
                        "auditor_member_id": 1167,
                        "intended_audience": "general",
                        "inventory_attributes": [
                            14
                        ],
                        "content_categories": [
                            8416
                        ]
                    }
                ]
            },
            {
                "auction_id_64": 260216368276039840,
                "size": "300x250",
                "sizes": [
                    "300x250",
                    "250x250",
                    "300x600"
                ],
                "smaller_sizes_allowed": false,
                "position": "below",
                "tag_format": "javascript",
                "site_id": 190350,
                "creative_formats_map": "1111111110",
                "creative_formats": [
                    "unknown",
                    "html-url",
                    "js-url",
                    "flash",
                    "image",
                    "js-raw",
                    "html-raw",
                    "html-iframe",
                    "vast-url"
                ],
                "ad_profile_id": 203694,
                "ad_profiles": [
                    203694
                ],
                "visibility_profile_id": 156,
                "venue_id": 83202,
                "allowed_media_types": [
                    1
                ],
                "media_subtypes": [
                    "banner"
                ],
                "estimated_clear_price": 1.056,
                "estimated_average_price": 0.352,
                "id": 597908,
                "inventory_audits": [
                    {
                        "auditor_member_id": 1167,
                        "intended_audience": "general",
                        "inventory_attributes": [
                            14
                        ],
                        "content_categories": [
                            8416
                        ]
                    }
                ]
            },
            {
                "auction_id_64": 8404278393772071000,
                "size": "728x90",
                "sizes": [
                    "728x90",
                    "468x60"
                ],
                "smaller_sizes_allowed": false,
                "position": "below",
                "tag_format": "javascript",
                "site_id": 190350,
                "creative_formats_map": "1111111110",
                "creative_formats": [
                    "unknown",
                    "html-url",
                    "js-url",
                    "flash",
                    "image",
                    "js-raw",
                    "html-raw",
                    "html-iframe",
                    "vast-url"
                ],
                "ad_profile_id": 203694,
                "ad_profiles": [
                    203694
                ],
                "visibility_profile_id": 156,
                "venue_id": 83202,
                "allowed_media_types": [
                    1
                ],
                "media_subtypes": [
                    "banner"
                ],
                "estimated_clear_price": 0.771,
                "estimated_average_price": 0.257,
                "id": 598003,
                "inventory_audits": [
                    {
                        "auditor_member_id": 1167,
                        "intended_audience": "general",
                        "inventory_attributes": [
                            14
                        ],
                        "content_categories": [
                            8416
                        ]
                    }
                ]
            }
        ],
        "bid_info": {
            "user_id_64": 70184478430632760,
            "no_cookies": false,
            "payment_rule_id": 174001,
            "selling_member_id": 1167,
            "no_flash": false,
            "user_agent": "Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Win64; x64; Trident/5.0)",
            "browser": 16,
            "operating_system": 1,
            "language": 5,
            "accepted_languages": "fr-FR",
            "session_freq": 21,
            "pub_session_freq": 21,
            "ip_address": "217.128.220.29",
            "country": "FR",
            "region": "A8",
            "city": "Paris",
            "time_zone": "Europe/Paris",
            "within_iframe": false,
            "publisher_id": 120697,
            "url": "https://www.appnexus.com/",
            "domain": "appnexus.com",
            "inventory_audits": [
                {
                    "auditor_member_id": null,
                    "intended_audience": "general",
                    "inventory_attributes": [
                        8,
                        14
                    ],
                    "content_categories": [
                        23,
                        8428
                    ]
                }
            ],
            "userdata_json": "{}",
            "segments": []
        }
    }
}
```

### Example multi-tag response

```
{
    "bid_response": {
        "responses": [
            {
                "member_id": 1143,
                "price": 2.22,
                "creative_id": "540839",
                "auction_id_64": 3476552926870226000
            },
            {
                "member_id": 1143,
                "price": 2.14,
                "creative_id": "540838",
                "auction_id_64": 7415314500030035000
            },
            {
                "member_id": 1143,
                "price": 2.12,
                "creative_id": "540893",
                "auction_id_64": 260216368276039840
            },
            {
                "member_id": 1143,
                "price": 2.16,
                "creative_id": "540815",
                "auction_id_64": 8404278393772071000
            }
        ]
    }
}
```
