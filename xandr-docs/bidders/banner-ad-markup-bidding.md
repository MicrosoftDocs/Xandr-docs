---
title: Banner Ad Markup Bidding
description: In this article, find information about bidding with a banner ad markup and how to use this feature.
ms.date: 10/28/2023
---

# Banner ad markup bidding

> [!IMPORTANT]
> This feature is currently in beta testing with select clients. If you would like to participate in the beta, please reach out to your Xandr representative.

Banner Ad Markup Bidding enables your bidder to submit banner ad markup via `adm` in the OpenRTB bid response. Instead of registering every banner creative asset you have with Xandr, you are required to register only a single creative for each ad campaign or brand you represent; all banner creative assets for that brand can be passed dynamically via ad markup in the bid response. This page explains how to use this feature.

## Getting started

Your bidder must be enabled to use this feature. If you are not sure whether your bidder is enabled, please check with your Xandr account representative.

Once enabled, there are two steps required to buy Banner inventory via Ad Markup Bidding:

1. Register your creative. For each ad campaign or brand that you represent, you must register at least one creative that represents that campaign or brand. Your creative must pass platform audit. All banner creative assets associated with this brand within your bidder will serve through this creative. See [Register Banner Creatives](#register-banner-creatives) below for details.
1. Bid with your creative assets on banner inventory. See [Bid with Banner Ad Markup](#bid-with-banner-ad-markup) below for details.

## Register banner creatives

For each ad campaign or brand that you represent, you must register at least one creative that represents that campaign or brand. This is done using the [Creative Service](creative-service.md). When registering a Banner Creative, there are a few considerations to keep in mind:

- The creative must represent one of the actual banner ads that you will dynamically pass on the bid response for this ad campaign or brand. The specific ad you choose to register does not matter, but the creative must contain a valid image, consistent with an ad you would actually serve on banner inventory.
- When registering a creative, only [Xandr Macros](xandr-macros.md) are supported. OpenRTB macros (such as `${AUCTION_PRICE}`) will not be expanded.
- The creative must be submitted for platform audit.
- You do not need to specify the `brand_id` field; this will be set by Xandr during audit.

The following section provides an example of defining and registering a Banner Creative.

## Creative example

This example uses the standard creative template "HTML (Xandr Created)" (id 6). Any standard template for banner creatives may be used. See [Creative Service](creative-service.md) for more details.

### Adding a banner creative

```
$ cat banner_creative.json
 
{
  "creative": {
        "allow_audit": true,
        "allow_ssl_audit": true,
    "description": "test description",
    "code": "test_code",
    "code2": "test_code2",
        "content": "..."
        "content_secure": "..."
        "width": 300,
        "height": 250,
        "status": {
                "user_ready": true
        }
    "template": {
      "id": 6
    },
  }
}
 
$ curl -b cookies -c cookies -X POST -s @banner_creative.json 'https://api.adnxs.com/creative/123'
 
{
  "response": {
    "status": "OK",
    "id": 12345,
    "count": 1,
    "start_element": 0,
    "num_elements": 100,
    "creative": {
      "id": 12345,
      "active": true,
      "member_id": 123,
      "description": "test description",
      "code": "test_code",
      "code2": "test_code2",
      "audit_status": "pending",
      "allow_audit": true,
      "ssl_status": "pending",
      "allow_ssl_audit": true,
      "template": {
        "id": 6
      },
      ...
    },
    "dbg": {
      ...
  }
}
```

## Bid with banner ad markup

Once you have registered a Banner Creative and it has passed platform audit, you can begin bidding with that creative using the [OpenRTB protocol](https://www.iab.com/wp-content/uploads/2016/03/OpenRTB-API-Specification-Version-2-4-FINAL.pdf). Requirements include:

- Either the `crid` or `adid` field must be included in the bid response to identify the creative that was registered. The `crid` value must match the creative's `code`;  `adid` must match the creative's `id`.
- The banner creative markup must be passed as HTML content via the `seatbid.bid.adm` field.
  - If the ad markup is not passed as HTML content or is otherwise malformed, the bid is rejected.
  - When ad markup is passed, the `seatbid.bid.ext.appnexus.custom_macros` extension field is ignored.
  - If the ad markup field is not returned at all, the registered creative content will serve by default. In this case, `seatbid.bid.ext.appnexus.custom_macros`is supported as usual.
  - The following macros are supported in order to facilitate impression & click tracking. See [ADM Macros Example](#adm-macros-example) below to see how these should be used.
    - `${AN_IMP_URL}`: This macro expands to a Xandr impression tracking URL, and is intended to prepend the bidder's impression tracking pixel. When the ad is rendered, the expanded URL will redirect to the bidder's pixel and correctly expands the `{AUCTION_PRICE}` macro. Note that the bidder's pixel and the `${AUCTION_PRICE}` must be URL-encoded in `adm`.
    - `${AN_CLICK_URL}`: This macro expands to a Xandr click tracking URL, and is intended to prepend the bidder's click tracking pixel. When the ad is clicked, the expanded URL will redirect to the bidder's pixel and correctly expands the `${AUCTION_PRICE}` macro. Note that the bidder's pixel and the `${AUCTION_PRICE}` must be URL-encoded in `adm`.
    - `${AN_IS_AUDIT}`: Expands to 1 when audit events (impressions & clicks) occur, expands to 0 otherwise. Must be URL-encoded when included in a URL following the `${AN_IMP_URL}` or `${AN_CLICK_URL}` macros.
  - If the following macros are present and unencoded in `adm`, they are stripped out before serving the ad: `${AUCTION_PRICE}` and `${AN_IS_AUDIT}`. To use these macros, be sure to URL-encode them in pixels as described in the previous bullet.
- The win notification url can be optionally submitted in `seatbid.bid.nurl`.
- Creative dimensions must be submitted in the `seatbid.bid.w` and `seatbid.bid.h` fields. These dimensions will override the dimensions of the registered creative, and will be subject to the usual size checks performed during the auction.
  - If neither of these dimensions is submitted, the bid is rejected.
  - If only one of these dimensions is submitted, the bid is rejected.
  
- The `ver` field is ignored in the bid response.  

- The `adomain` field may be checked occasionally to verify that the ad’s brand aligns with publisher preferences.  

Some publishers periodically audit creatives, which can generate false impression & click tracking events. When Xandr detects audit events:

- Any URL-encoded `${AUCTION_PRICE}` macro in `adm` is expanded to the string `"AUDIT"`.
- Any URL-encoded `${AN_IS_AUDIT}` macro expands to 1
- `nurl` is not called, if it's present in the bid response.
  
  > [!NOTE]
  > The creative assets and technology vendors you bid with must match the brand and vendors of the creative asset you initially registered. If you registered an SSL creative, ad markup must also be SSL. Xandr periodically scans and reviews ad markup creative content to ensure this content is consistent with the registered creative. If there is a discrepancy, your creative can be rejected by platform audit. Frequent creative audit rejections due to rotating brands can result in revoked access to the Ad Markup Bidding feature.

### ADM macros example

The below demonstrates how a bidder might utilize the `${AN_IMP_URL}`, `${AN_CLICK_URL}`, `${AUCTION_PRICE}`, and `${AN_IS_AUDIT}` macros.

For example, let's say a bidder wants to insert the following impression tracker in `adm`:

```
<img src="media/win?price=${AUCTION_PRICE}&audit=${AN_IS_AUDIT}&otherargs=123"/> 
```

The `adm` sent in the bid response should look like this:

```
<img src="${AN_IMP_URL}https%3A%2F%2Fdsp.bidder.com%2Fwin%3Fprice%3D%24%7BAUCTION_PRICE%7D%26audit%3D%24%7BAN_IS_AUDIT%7D%26otherargs%3D123"/> 
```

The `${AN_IMP_URL}` macro will expand to a Xandr wrapper URL that will correctly replace URL-encoded macros and will redirect to the destination. The seller will see something like this:

```
<img src="media/openrtb2_tracker?[an specific args here]&pp=${AUCTION_PRICE}&urlenc=https%3A%2F%2Fdsp.bidder.com%2Fwin%3Fprice%3D%24%7BAUCTION_PRICE%7D%26audit%3D%24%7BAN_IS_AUDIT%7D%26otherargs%3D123"/>
```

## Bid response example

```
{
    "seatbid": [
        {
            "bid": [
                {
                    "nurl": "https://rtb-fakeurl.com/lax/wintrk=CwE&wp=${AUCTION_PRICE}&curr=${AUCTION_CURRENCY}&aid=${AUCTION_AD_ID}",
                    "adid": "12345",
                    "crid": "test_code",
                    "price": 2.50,
                    "adm": "<a href=\"https://adserver.com/click?crid=54321...\"><img src=\"https://image.dspcdn.com/auction_id=123456789\"/></a>",
                                        "w": 728,
                                        "h": 90,
                    "impid": "3226285750417000001",
                    "id": "6ab34155-c960-1111-abcd-52b7321adbbb"
                }
            ],
            "seat": "123"
        }
    ],
    "id": "3",
    "cur": "USD"
        }
    ]
}
```

## FAQs

### Why do I have to register a creative for each brand I represent?

Xandr policy prohibits brand rotation on creatives. By registering a creative for each ad campaign or brand you work with, your creative will be able to pass Xandr audit. This will maximize the inventory on which it can serve. We recommend uploading creatives in a manner that matches your system's creative structure, provided that each creative is for a specific ad campaign or brand. Xandr ensures that each creative complies with our audit policies by performing an initial audit and then periodically scanning the creative content that your bidder dynamically passes in its bid responses. If the dynamic content served by your bidder differs substantially from the registered creative (i.e. images and text for a different brand) it will be reaudited and may be rejected.

### Will I be charged creative audit fees for periodically reaudited creative ad markup?

No. Creative audit fees will apply only during your creative's initial audit.

### What happens if my Banner Creative passes initial audit but fails a subsequent reaudit?

Your creative will not be permitted to serve. The audit failure may be due to rotating brands. If you believe your creative has been failed incorrectly or have other questions please contact [Xandr Customer Support](https://help.xandr.com/) and select the Category "Creative Audit". Please note that frequent creative audit rejections due to rotating brands may result in revoked access to the Ad Markup Bidding feature.

### Where do I go for more help?

If you have additional questions, please contact your account representative or [Xandr Customer Support](https://help.xandr.com/).
