---
title: Click Request
description: Learn how the Impression bus inserts our clicktracking URL into the creative at serve time and report any clicks that occur. This page covers implementation along with an example of the click request.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---


# Click request

The impression bus will insert our clicktracking URL into the creative at serve time and log and report any clicks that occur. If the member whose creative served is integrated with a bidder, the Impression Bus also passes along the click information to the bidder's designated click handler (defined using the `click_uri` field of the [Bidder Service](bidder-service.md)).

## Implementation

**Specs**

| Field | Scope | Type | Description |
|--|--|--|--|
| `auction_id_64` | all | int | The unique ID for the auction of the impression won. |
| `custom_notify_data` | some | string | The data passed by the bidder on the bid response. |
| `member_id` | all | int | The numeric ID of the auction's winning member. |
| `referer_url` | all | string | The referring URL of the page where the click originates. |
| `test` | all | Bool | Whether or not the impression clicked was run as a test impression. |
| `timestamp` | all | string | The timestamp of the click. |
| `user_agent` | all | string | The user agent string from the click request's HTTP header. |
| `user_id_64` | all | int | The unique ID for the user. It will be the same for all requests from this user until cookies are cleared. |
| `userdata_json` | some | string | The data for the user stored in the bidder's reserved space within our data store. |

## Example click request

``` 
{
   "click_request":{
      "timestamp":"2008-12-01 22:19:00",
      "auction_id_64":677373076784237441,
      "member_id":13,
      "user_id_64":2987961585469200312,
      "referer_url":"sports.yahoo.com",
      "user_agent":"Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.0.4) Gecko/2008102920 Firefox/3.0.4",
      "userdata_json": "{\"segments\":[2]}",
      "test": false
   }
}
```
