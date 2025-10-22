---
title: Click Response
description: On recieving a Click Request, Bidder writes a Click Response which is passed to userdata_json field of Bid Requests. This page covers implementation and an example of a pixel response.  
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---


# Click response

> [!NOTE]
>
> - **Not Supported**: The Xandr bidding protocol is no longer supported; this documentation is for legacy purposes only.
> - If you're a new bidder integrating with Xandr, please see the [OpenRTB 2.4 Bidding Protocol](https://www.iab.com/wp-content/uploads/2016/03/OpenRTB-API-Specification-Version-2-4-FINAL.pdf).

Once a bidder receives a [Click Request](click-request.md), it can write data to the bidder's reserved segment of the AppNexus data store through a ***click response***. This data will then be passed into the `userdata_json` field of any future [Bid Requests](bid-request.md).

## Implementation

**Specs**

| Field | Type | Description |
|--|--|--|
| `userdata_js` | string | Javascript string to execute updating the user's `userdata_json` on a future [Bid Request](bid-request.md). |
| `segment_actions` | array | List of segments to modify for the user. |

## Example pixel response

This example will call the hypothetical `setZip` function on the user, add segment `1234` with a `60` minute expiration, and remove segment code `"abcd"` from the user.

``` 
{
    "click_response": {
        "userdata_js": "setZip('12345')",
        "segment_actions": [{"action": "add", "id":1234, "expires_min": 60},{"action": "remove", "code":"abcd","member_id":567}],
    }
}
```

## Related topic

[Click Request](click-request.md)
