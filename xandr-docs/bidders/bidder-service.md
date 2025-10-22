---
title: Bidder Service
description: In this article, learn about bidder service, their JSON fields, REST API, along with a detailed set of examples.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidder service

The Bidder Service connects a bidder to Xandr's impression bus and allows the bidder and the impression bus to begin communication. Your Xandr representative will create the bidder in the system, and you will use the Bidder Service to make modifications or retrieve your bidder ID.

You may need your bidder ID for some of the Services. To find out what your bidder ID is, run the "see all bidders" command described below.

Some bidder functions are accessible only to certain users, as they are based upon contractual obligations:

Modifying the data provider fields (via `PUT`) - requires a data access agreement with each provider

In bidder sandbox environments, all functionality is available for integration purposes.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.adnxs.com/bidder/](https://api.adnxs.com/bidder/) | View the bidder that your user has permissions to. It won't show other users' bidders. |
| `GET` | [https://api.adnxs.com/bidder/BIDDER_ID](https://api.adnxs.com/bidder/BIDDER_ID) | View a particular bidder. |
| `POST` | [https://api.adnxs.com/bidder](https://api.adnxs.com/bidder)<br>(bidder JSON) | Add a new bidder. |
| `PUT` | [https://api.adnxs.com/bidder/BIDDER_ID](https://api.adnxs.com/bidder/BIDDER_ID)<br>(bidder JSON) | Modify an existing bidder. |
| `DELETE` | [https://api.adnxs.com/bidder/BIDDER_ID](https://api.adnxs.com/bidder/BIDDER_ID) | Delete an existing bidder. |

## JSON fields

| Field | Required | Type | Description |
|:---|:---|:---|:---|
| `id` | yes, on update | int | The ID of the bidder. |
| `short_name` | yes (on add) | string | An optional short name for the bidder. While not technically required, this field is necessary for metrics, so it should be considered required. <br><br>**Note:** Only alphanumeric characters (A-Z, 0-9) and underscores are allowed. Do not use spaces, special characters, periods, or other punctuation marks. |
| `name` | yes (on add) | string | Name associated with the bidder. |
| `active` | no, default is true | Boolean | Whether the bidder will receive requests or not. |
| `bid_uri` | yes (on add) | string(255) | The URI for bid requests (for example, `/bid`). |
| `notify_uri` | no | string (255) | The URI for notification requests (for example, `/notify`). Use null, not an empty string, to set this to blank.<br><br>**Note:**<br> - The `notify_uri` must be a relative URI. Xandr does not currently support putting the `bid_uri` and `notify_uri` on separate hosts.<br> - If null, the bidder does not receive notify requests. |
| `click_uri` | no | string(255) | The URI for click requests (for example, `/click`). Use null, not an empty string, to set this to blank. See [Click Request](click-request.md). |
| `pixel_uri` | no | string(255) | The URI for pixel requests (for example, `/pixel`). Use null, not an empty string, to set this to blank. See Pixel Request. |
| `ready_uri` | yes (on add) | string(50) | The URI for a [Bidder Instance](bidder-instance-service.md) status check (for example, `/ready`). |
| `audit_notify_uri` | no | string(255) | The URI for passing creative auditing updates (eg `https://send.mycompany.com/auditnotifyrequests`) |
| `parent_profile_id` | no | int | The ID of the parent bidder profile. Bidder profiles can be used to filter bid request traffic that reaches a bidder. See [Legacy Bidder Profile Service](legacy-bidder-profile-service.md) and [Bidder Profile - FAQ](bidder-profile---faq.md). |
| `child_profiles` | no | Array of objects with the ID of the [bidder profiles](legacy-bidder-profile-service.md). | Array of objects specifying the child profiles to be used. For example: `[{"id":123}, {"id":124}]`. |
| `dongle` | no | string | A password that protects a bidder's debug output in a debug impression. See `debug_text` in the [Bid Response](incoming-bid-response-from-bidders.md). **Available to users of type "bidder" only**. |
| `notify_full_auction` | no | Boolean | Setting this to "true" means that the impression bus will include `full_tag_info` and `bid_info` in the [Notify Request](notify-request.md). Post-pending notifies (`post_pending` set to `true` in the Notify Request) do not include these tags because the bid acceptance callback has not yet been received. |
| `notify_lost` | no, default is `false` | Boolean | Indicates whether the bidder is notified about all lost bids at the URI specified in the `notify_uri` field. If no URI is provided, no notifications are sent.<br> - If `true`, the bidder is notified about all lost bids.<br> - If `false`, the bidder is only notified about lost bids with [Notify Request error code IDs](bid-error-codes.md) above 100. We don't log errors or send lost notifies if the error id is less than 100 for OpenRTB bidders. |
| `notify_pending` | no, default is `false` | Boolean | Indicates whether the bidder is notified about pending bids at the URI specified in the `notify_uri` field. If no URI is provided, no notifications are sent. |
| `notify_no_bid` | no, default is `false` | Boolean | Indicates whether the bidder is notified when the bidder has no bid for a request. The notification is sent to the URI specified in the `notify_uri` field. If no URI is provided, no notifications are sent. |
| `exclude_unowned` | no | Boolean | Exclude inventory not owned by a member associated with this bidder. |
| `send_unaudited` | no, default is `false` | Boolean | This flag determines whether or not your bidder will be sent unaudited traffic.<br><br>**Warning:** Strictly speaking, this field is deprecated, but it should ALWAYS be set to `true`. If this field is set to `false`, your bidder will not receive any [Bid Requests](outgoing-bid-request-to-bidders.md). |
| `bid_percent` | no | int | The percent (50 = 50%) of total platform traffic that you wish to receive. Requests that are sent to your bidder are randomly chosen, although you can choose for your bidder to always receive requests for users in segments of members associated with your bidder. If you set bid_percent to 0, your bidder will only receive requests for users in at least one of your members' segments. This filter is applied to traffic that makes it through the [Legacy Bidder Profile Service](legacy-bidder-profile-service.md). |
| `always_send_owned_segments` | no | Boolean | Determines whether impressions for users in segments owned by or shared with the Bidder should bypass passthrough_percent on [Bidder Profiles](legacy-bidder-profile-service.md).<br><br>**Note:** This only overrides the passthrough_percent on the bidder profile; all other restrictions such as country or region, member, size, or domain filters would still be taken into consideration when deciding whether an impression will be sent to the bidder.  |
| `object_limit_notify_email` | no | array of strings | Xandr limits the number of objects each bidder can create and use on the platform. This limit includes inactive and unused objects. This field contains the email addresses that will be notified when you hit the 85%, 95%, and 100% threshold for object limits. |
| `protocol_id` | no | int | **Read-only**. This describes the protocol associated with this bidder, which describes the type of bidder it is. For example, a `protocol_id` of `6` means that this bidder uses the OpenRTB 2.0 specification for its integration with Xandr. The default integration value for a newly created bidder is `1`, `none`. This is the default protocol as defined in [Bid Request](outgoing-bid-request-to-bidders.md) and [Bid Response](incoming-bid-response-from-bidders.md). Bidders with a `protocol_id` of 6 integrate according to the [OpenRTB 2.0 Spec (PDF)](https://www.iab.net/media/file/OpenRTB_API_Specification_Version2.0_FINAL.PDF).<br>[Spec for OpenRTB 2.4](bidding-protocol.md), `protocol_id`: 10. <br>The following values are supported (each ID is followed by the `protocol_name` associated with that ID):<br> - 1: `none`<br> - 2: `wp7`<br> - 3: `contentads`<br> - 4: `admarket`<br> - 5: `adexpert`<br> - 6: `openrtb2.0`<br> - 10: `openrtb2.4` |
| `protocol_name` | no | string | **Read-only**. The name of the protocol associated with this bidder. See the definition of `protocol_id` above for all of the the accepted values of `protocol_id` and their mappings to names. |
| last_activity | no | timestamp | The timestamp of last modification to this bidder instance. |
| `max_seats` | no | Integer | Bidders bidding with custom buyer seat IDs will have this field include a value greater than 0. This is the maximum number of seats allowed to be registered under a bidder.<br><br>**Note:** This feature is currently in Closed Beta. If you are interested in participating, reach out to your Xandr representative. |
| `default_member` | no | Object | Bidders using buyer seat ID bidding will have a default member designated in this field. Note the default member will be the main billing member for the bidder and is also used as the member ID for creative registration.<br><br>**Note:** This feature is currently in Closed Beta. If you are interested in participating, reach out to your Xandr representative. |

> [!NOTE]
> Use Bidder Profile Service to Filter and Throttle.

To filter the traffic your bidder will receive, use the [Legacy Bidder Profile Service](legacy-bidder-profile-service.md). A few filtering and throttling fields still exist in the Bidder Service, but they will be migrated to the Bidder Profile Service soon. Class filters are available in both; we recommend using the Bidder Profile Service for these.

## Deprecated fields

| Field | Required | Type | Description |
|:---|:---|:---|:---|
| `send_class_2` | no, default is `true` | Boolean | This flag determines whether or not your bidder will be sent Class 2 traffic. Note that throttling by inventory class is also possible via the [Legacy Bidder Profile Service](legacy-bidder-profile-service.md). |
| `send_class_3` | no, default is `true` | Boolean | This flag determines whether or not your bidder will be sent Class 3 traffic. Note that throttling by inventory class is also possible via the [Legacy Bidder Profile Service](legacy-bidder-profile-service.md). |
| `send_unaudited` | no, default is `false` | Boolean | This flag determines whether or not your bidder will be sent unaudited traffic.<br><br>**Note:** Throttling by inventory class is also possible via the [Legacy Bidder Profile Service](legacy-bidder-profile-service.md).<br><br>**Warning:** You must set this field in order to see bid requests<br>You **must** set `send_unaudited` to `true` in order for your bidder to receive bid requests. For more information, see [Integrate a Bidder](integrate-a-bidder.md). |
| `send_owned_blocklist` | no | Boolean | Send blocklist inventory if owned by a member associated with this bidder. |
| `userdata_entity_id` | no | int | This field is deprecated. |
| `userdata_javascript` | no | string | Custom JavaScript functions that can be called when a bidder updates a user's cookie data. |
| `setuid_function` | no | string | The name of the JavaScript function to be used on *SetUID* calls. |

## Examples

### Authentication token

Authentication is always the first step when using the API Services. The authentication token can then be written to our cookie file for future use. For more detailed instructions, see [Authentication Service](authentication-service.md).

### View bidder information

If Xandr has already added your bidder for you, you will already have some bidder information, like your bidder ID, in JSON format. You can view this information with the below command.

```
S curl -b cookies -c cookies "https://api.adnxs.com/bidder"
{
   "response":{
      "status":"OK",
      "bidder":{
         "id":4,
         "name":"Test Bidder",
         "short_name":"TestBidder",
         "active":true,
         "parent_profile_id": 12345,
         "child_profiles":[{"id":1000},{"id":2000},{"id":3000}],
         "bid_uri":"/bid",
         "notify_uri":"/notify",
         "click_uri":null,
         "ready_uri":null,
         "pixel_uri":"/pixel",
         "audit_notify_uri":null,
         "last_activity":"2009-01-07 22:07:08"
      }
   }
}
```

### Modify a bidder

Now that you know your bidder ID, you can use a text file in JSON format to modify your bidder. Below is an example JSON that will change the ready URI parameter.

> [!NOTE]
> These included fields will be updated. All other fields will be unchanged.

```
$ cat bidder
{
      "bidder":{
         "id":4,
         "ready_uri":"/ready"
      }
   }
```

Then you use the `PUT` command to update this data in the impression bus cache.

```
$ curl -b cookies -c cookies -X PUT --data-binary @bidder 'https://api.adnxs.com/bidder/4'
{
   "response":{
      "status":"OK",
      "id":4
   }
}
```

Now when you view Bidder 4, you get:

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/bidder/4'
{
   "response":{
      "status":"OK",
      "bidder":{
         "id":4,
         "name":"Test Bidder",
         "short_name":"TestBidder",
         "active":true,
         "parent_profile_id": 12345,
         "child_profiles":[{"id":1000},{"id":2000},{"id":3000}],      
         "bid_uri":"/bid",
         "notify_uri":"/notify",
         "click_uri":null,
         "ready_uri":"/ready",
         "ready_string":"Ready:1"
         "pixel_uri":"/pixel",
         "audit_notify_uri":null,
         "last_activity":"2009-01-07 22:07:08"
      }
      }
}
```

## Related topics

- [Legacy Bidder Profile Service](legacy-bidder-profile-service.md)
- [Bidder Profile - FAQ](bidder-profile---faq.md)
- [Bidder Instance Service](bidder-instance-service.md)<a href="" class="xref"></a>
- [Integrate a Bidder](integrate-a-bidder.md)
