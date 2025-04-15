---
title: Integrate a Bidder
description: This article provides instructions to integrate a bidder with Xandr.
ms.date: 11/27/2023
---

# Integrate a bidder

This page describes how to integrate a bidder with Xandr. It begins with an overview of the different "layers" of the integration, and ends with a worked example (using actual API calls) of a simple integration that will get you up and running quickly in our testing environment. It also provides links to more detailed information elsewhere on our Wiki.

## System overview

> [!NOTE]
> **Bidding Protocol**
>
> Xandr currently supports the OpenRTB 2.4 bidding protocol. For more info check out our [Bidding Protocol](./bidding-protocol.md) page.

At a high level, there are two "layers" of the system we need to be concerned with during bidder setup:

- Real-Time Layer (RTB): This is the heart of the action, where your bidder will participate in the real-time auction.
  - Our server receives a bid request from a webpage (or SSP partner), and format it to prepare to send to our bidders.
  - Using the settings in the bidder instance (and your bidder object), we send the request along to your servers.
    - The endpoint the request hits depends on the request type.

    :::image type="content" source="media/rtb-png.png" alt-text="Diagram that explains the bidder's participation in the real-time auction.":::

- Configuration Layer (API): This is where you will configure your bidder's "business logic" so it can bid on impressions; in other words, filtering out unwanted impressions, and setting up users, adding the creatives your members want to serve, etc.

  :::image type="content" source="media/config-layer.png" alt-text="Diagram that explains how the bidder's business logic can be configured.":::

## Note on object hierarchy

It is important to understand how our platform objects relate to one another. Below is an outline of our object hierarchy.

### Bidders, Members, Seats

- Bidders are the highest object in our buy side hierarchy. It represents your entity's presence on our platform.
- Below them are members. The relationship used to be one-to-many, with a bidder possibly having several member breakouts.
  - This is no longer the case. It is now one-to-one, as we no longer support additional member breakouts.
  - You will be integrated with a single member, which we refer to as your 'Default Member'.
- Members are considered entities that have contractual agreements to buy (or sell) through the impression bus (for more details, see the [Member Service](./member-service.md)).
  - Creatives are associated with your default member, not your bidder.
- The bidders themselves are not members, but rather they are the technology providers for members.
  - The bidder is where you set up a connection with Xandr (such as what kind of requests to receive, to which endpoint, etc.).
  - The member is where you set up campaign-related objects such as creatives.
  - The bidder is integrated into our UI. The impression bus connects bidders with various sources of inventory, including aggregators, ad exchanges, and network resold inventory.
- Seats are your internal entities which you can use to bid in our auctions, and purchase impressions with their corresponding internal ID.
- The diagram below illustrates this hierarchy
  - With the previous member breakouts, we held a mapping of which of a bidder's seats corresponded to which breakout member. This allowed bidders to bid with their internal IDs 100% of the time.
  - Since you will be integrating with only one member, and with buyer seat bidding, you will only have the one default member, and do not have to worry about the seat-member mapping.
  :::image type="content" source="media/hierarchy.png" alt-text="Diagram that illustrates the hierarchy between bidders, members, and seats.":::

### Users

- Traditionally, bidders can act on behalf of themselves, or they can have several 3rd-party members.
- Members must have at least one user, regardless of whether the member acts on behalf of a third party (for more details, see the [User Service](user-service.md)).
  - Members can have many users.
- The bidder, as a technology provider, also has at least one user.
- The users for bidders adjust the bidder profile, add bidder instances, etc.
- Member users upload creatives for that member, etc.
- Even if the bidder is the same corporation as a member, and the bidder only acts on behalf of itself, the bidder is logically distinct from the member in the same fashion.

  :::image type="content" source="media/users.png" alt-text="Diagram that shows the components of bidder and their roles.":::

## How to set up your bidder

In this section we'll walk through the entire process of setting up a bidder on the platform. We'll begin by making the API calls necessary to hook up the pipes.

> [!TIP]
> **APIs**
>
> Most client testing is done in our production APIs. We also have a testing environment API which allows for testing of your object creation and updating workflows.
>
> Most of the examples calls below are done in the production API environment.

## Authenticate with the API

Before we can do anything else, we have to log in. Below is an example of the authentication json you can use. The authentication process for our production and testing environment is the same. The only difference is the endpoint.

> [!TIP]
> For more detailed information about authenticating via our API, see the [Authentication Service](./authentication-service.md).

### Example authentication JSON

```
$ cat auth.json
        
        {
        "auth":
        {
        "username" : "rloveland",
        "password" : "AppNexus1!"
        }
        }
      
```

Post to the production API to authenticate:

### Example auth call in production API

```
$ export IB="https://api.adnxs.com";
$ curl -b cookies -c cookies -X POST -d @auth.json $IB/auth
        
{ response": { "status": "OK", ... } }
        
      
```

Similarly, post to the test environment to authenticate:

### Example auth call in testing API

```
$ export IB_TESTING="https://api-test.adnxs.com";
$ curl -b cookies -c cookies -X POST -d @auth.json $IB_TESTING/auth
        
{ response": { "status": "OK", ... } }
      
```

## View your bidder object

The bidder object represents your bidder in our system. As such, it has a lot of fields that you can use to configure how your bidder interacts with our platform. Think of it as the central "hook" on which you'll hang much of the rest of your configuration. A bidder object should already have been created for you by your Xandr representative.

In the example below, we make a `GET` call to view the bidder object, but we don't explain any of its details. For more detailed information about the bidder object, see the [Bidder Service](./bidder-service.md).

### Expand for call example

```
$ export IB="https://api.adnxs.com";
$ curl -b cookies $IB/bidder/123

{
  "response": {
    "bidder": {
      "active": true,
      "always_send_owned_segments": true,
      "audit_notify_uri": null,
      "bid_percent": 100,
      "bid_uri": "/xandr/bid",
      "child_profiles": null,
      "click_uri": null,
      "daily_budget": null,
      "daily_budget_imps": null,
      "default_currency": "USD",
      "default_member": {
        "id": 9876,
        "name": "Example Bidder's Default Member Name"
      },
      "dongle": null,
      "exclude_unowned": false,
      "id": 123,
      "last_activity": "2021-02-03 19:47:25",
      "lifetime_budget": null,
      "lifetime_budget_imps": null,
      "max_allowed_profiles": 5,
      "max_seats": 10000,
      "name": "ExampleBidder",
      "notify_full_auction": false,
      "notify_uri": null,
      "num_conns": 3,
      "object_limit_notify_email": null,
      "parent_profile_id": null,
      "pixel_uri": null,
      "protocol_id": 10,
      "protocol_name": "openrtb2",
      "ready_uri": "/status/ready",
      "send_class_2": true,
      "send_class_3": true,
      "send_owned_blocklist": false,
      "send_public_deals": false,
      "send_unaudited": true,
      "setuid_function": null,
      "short_name": "examplebidder",
      "supports_deal_buyers": "seats",
      "userdata_entity_id": null,
      "userdata_javascript": null,
      "vendor_id": null
    },
    "count": 1,
    "dbg": {
      "output_term": "bidder",
      "version": "1.0.5",
      "warnings": [
        
      ]
    },
    "num_elements": 100,
    "start_element": 0,
    "status": "OK"
  }
}     
```

## Bidder object configurations

**For the following fields of the "Bidder" object, IP Address/Hostname should not be included preceding the path.**

IP Address <u>will</u> be configured separately on the "Bidder Instance" object(s) in the next step of the integration process.

| Field | Required | Description |
|---|---|---|
| **bid_uri** |  | the path/filename that specifies the destination for [Bid Requests](./outgoing-bid-request-to-bidders.md) (e.g. "/bidder") |
| **ready_uri** |  | the path/filename that specifies the destination for [Ready Requests](./ready-request.md) (e.g. "/ready") |
| **notify_uri** |  | the path/filename that specifies the destination for [Notify Requests](./notify-request.md) (e.g. "/notify") |
| **pixel_uri** | **optional** | the path/filename that specifies the destination |
| **click_uri** | **optional** | the path/filename that specifies the destination for [Click Requests](./click-request.md) |
|**audit_notify_uri** | **optional** | the path/filename that specifies the destination for [Audit Notify Requests](./audit-notify-request.md) (For example, "`https://examplebidder.com/audit_notify_endpoint`") |

## View your member object

You need to have at least one member that buys through your bidder. You should have had a member created for you by your Xandr representative as part of the onboarding process. The member is where you will configure much of the "business logic" such as user segments, creatives, etc.

> [!TIP]
> In the example below, we make a `GET` call to view the member object, but we don't explain any of its details. Some of the fields which are displayed to you may be deprecated. For more detailed information about the member object, including which fields are currently supporting, see the [Member Service](./member-service.md).

### Expand for call example

```
$ export IB="https://api.adnxs.com";
$ curl -b $IB/member/1234

{
  "response": {
    "count": 1,
    "dbg": {
      "output_term": "member",
      "version": "1.18.1651",
      "warnings": [
        
      ]
    },
    "member": {
      "account_owner_user": {
        "first_name": "Peter",
        "id": 123456,
        "last_name": "Driver"
      },
      "active": true,
      "active_contract": null,
      "age_segment_id": null,
      "agent_id": null,
      "allow_ad_profile_override": true,
      "allow_priority_audit": false,
      "audit_notify_email": null,
      "bidder_id": 1234,
      "billing_address_1": null,
      "billing_address_2": null,
      "billing_city": null,
      "billing_country": null,
      "billing_name": "ExampleMemberName",
      "billing_postal_code": null,
      "billing_region": null,
      "buyer_clearing_fee_pct": null,
      "buyer_credit_limit": 2500,
      "code": null,
      "contact_email": null,
      "contact_info": null,
      "contracts": null,
      "curation_deductions_allowed": false,
      "daily_imps_self_audited": null,
      "daily_imps_unaudited": null,
      "daily_imps_verified": null,
      "deal_visibility_profile_id": null,
      "default_accept_data_provider_usersync": true,
      "default_accept_demand_partner_usersync": true,
      "default_accept_supply_partner_usersync": true,
      "default_ad_profile_id": null,
      "default_buyer_group_id": null,
      "default_content_retrieval_timeout_ms": 0,
      "default_creatives": null,
      "default_enable_for_mediation": false,
      "default_external_audit": false,
      "default_tag_id": null,
      "description": null,
      "developer_id": null,
      "domain_blocklist_email": null,
      "dongle": null,
      "email_code": null,
      "enable_click_and_imp_trackers": false,
      "enable_facebook": false,
      "expose_eap_ecp_placement_settings": false,
      "gender_segment_id": null,
      "id": 1234,
      "is_iash_compliant": false,
      "last_activity": "2020-03-19 06:00:39",
      "max_hosted_video_size": null,
      "native_custom_keys": null,
      "platform_exposure": "public",
      "plugins_enabled": false,
      "pops_enabled_UI": false,
      "price_buckets": null,
      "prioritize_margin": false,
      "reporting_decimal_type": "decimal",
      "seller_member_groups": null,
      "seller_revshare_pct": null,
      "serving_domain": null,
      "sherlock_notify_email": null,
      "short_name": null,
      "tax_region_id": null,
      "thirdparty_pixels": null,
      "timezone": "EST5EDT",
      "vendor_id": null,
      "visibility_profile_id": null,
      "xd_coop": false
    },
    "num_elements": 100,
    "start_element": 0,
    "status": "OK"
  }
}
```

## Create a bidder profile

In this step, we'll go through the options in the bidder profile that helps shape the traffic you receive. The bidder profile can be updated using both the API and our [bidder UI](./bidder-platform-user-interface.md). The main documentation for these are found here:

- API: [Enhanced Bidder Profiles](./enhanced-bidder-profiles.md)
- Bidder UI: [Creating a New Bidder Profile](./creating-a-new-bidder-profile.md)
- Our bidder UI provides many other services, such as metrics and reporting. These can be found here:
  - Metrics: [Metrics Screen](./metrics-screen.md)
  - Creatives: [Creatives Screen](./creatives-screen.md)
  - Reporting: [Reporting Screen](./reporting-screen.md)

In the example below, the targeting breaks down like this:

- Include only our [Direct Exchange](./exchange-service.md) members
- [Accept US based traffic only](./country-service.md)
- Banner traffic, of all sizes
- Web traffic
- [Allow for unknown users](./unknown-users.md)

### Bidder profile example JSON

```
$ cat create-bidder-profile-json

{
  "bidder_profile": {
    "active": true,
    "bidder_id": 1234,
    "description": "Example Bidder Profile",
    "targeting": {
      "ad_types": {
        "audio": {
          "action": "exclude"
        },
        "banner": {
          "action": "include",
          "sizes": [
            
          ]
        },
        "native": {
          "action": "exclude"
        },
        "video": {
          "action": "exclude"
        }
      },
      "countries": {
        "action": "include",
        "targets": [
          {
            "active": true,
            "code": "US",
            "id": 233,
            "name": "United States"
          }
        ]
      },
      "exchanges": {
        "action": "exclude",
        "targets": [
          {
            "id": 2,
            "name": "Connect"
          },
          {
            "id": 3,
            "name": "Network"
          }
        ]
      },
      "supply_types": {
        "action": "include",
        "targets": [
          "web"
        ]
      }
    },
    "unknown_users_action": "include"
  }
}
```

## Testing profile

- Your Xandr Integration Engineer will help you to set up a bidder profile for testing.
- This profile will block all platform traffic except for that which is sent from our testing publisher
- Traffic from our testing member will allow you to simulate the bid stream, without having to worry about spend.

## Add a test creative

In this step, we'll add a creative. After we upload this creative, you will need to set up your bidder to respond to a [Bid Request](./outgoing-bid-request-to-bidders.md) with a properly formatted [Bid Response](./incoming-bid-response-from-bidders.md). The bid response should include this creative, either in the `"crid"` field, corresponding to your internal ID for the creative, or the `"adid"`, which is the Xandr ID for the creative. This will test that your integration is working as expected.

> [!TIP]
> For more detailed information about the many types of creative configurations, see the [Creative Service](./creative-service.md).
>
> For some tips on getting your creative set up, see our [Quick Start Creative Buying Guide](quick-start-creative-buying-guide.md).

- This example shows a (very) old fashioned car design using the content field of the creative object. It uses our standard banner raw-html template.
- For more information on using the Client Testing environment to test the uploading of creatives, see [Using the Client Testing environment](#using-the-client-testing-environment) below.

> [!NOTE]
> **Statuses**
>
> - The `"allow_audit"` and `"allow_ssl_audit"` fields have each been set to `true`.
> - The `"allow_audit"` field submits the creative for our platform human audit.
> - The `"allow_ssl_audit"` submits the creative for our automated scan to determine if the creative can serve on secure inventory.

### Example creative JSON

```
$ cat add-creative.json
{
  "creative": {
    "width": 682,
    "height": 488,
    "landing_page_url": "https://en.wikipedia.org/wiki/Car",
    "content": "document.write('<a href=\\\"https://en.wikipedia.org/wiki/Car\\\" target=\\\"_blank\\\">\\r\\n <img src=\\\"https://upload.wikimedia.org/wikipedia/commons/3/3e/SteamMachineOfVerbiestIn1678.jpg\\\" />\\r\\n</a>')",
    "content_secure": "document.write('<a href=\\\"https://en.wikipedia.org/wiki/Car\\\" target=\\\"_blank\\\">\\r\\n <img src=\\\"https://upload.wikimedia.org/wikipedia/commons/3/3e/SteamMachineOfVerbiestIn1678.jpg\\\" />\\r\\n</a>')",
    "template": {
      "id": 6
    },
    "original_content": "<a href=\"https://en.wikipedia.org/wiki/Car\" target=\"_blank\">\r\n <img src=\"https://upload.wikimedia.org/wikipedia/commons/3/3e/SteamMachineOfVerbiestIn1678.jpg\" />\r\n</a>",
    "original_content_secure": "<a href=\"https://en.wikipedia.org/wiki/Car\" target=\"_blank\">\r\n <img src=\"https://upload.wikimedia.org/wikipedia/commons/3/3e/SteamMachineOfVerbiestIn1678.jpg\" />\r\n</a>",
    "click_action": "click-to-web",
    "click_target": "https://en.wikipedia.org/wiki/Car",
    "click_url": "https://en.wikipedia.org/wiki/Car",
    "allow_ssl_audit": true,
    "allow_audit": true
  }
}
```

### Example creative upload

```
$ export IB="https://api.adnxs.com";
$ curl -b cookies -X POST -d @add-creative.json $IB/creative/1234
{
    "response": {
        "count": 1,
        "creative": {
            "active": true,
            "added_by_bidder": null,
            "adservers": null,
            "adx_audit": null,
            "allow_audit": true,
            "allow_ssl_audit": true,
            "audit_feedback": null,
            "audit_status": "pending",
            "backup_upload_status": nul
            "brand": {
                "category_id": 0,
                "id": 1,
                "name": "Unknown"
            },
            "brand_id": 1,
            "campaign": null,
            "categories": null,
            "click_action": "click-to-web",
            "click_target": "https://en.wikipedia.org/wiki/Car",
            "click_url": "https://en.wikipedia.org/wiki/Car",
            "code": null,
            "code2": null,
            "content": "document.write('<a href=\\\"https://en.wikipedia.org/wiki/Car\\\" target=\\\"_blank\\\">\\r\\n <img src=\\\"https://upload.wikimedia.org/wikipedia/commons/3/3e/SteamMachineOfVerbiestIn1678.jpg\\\" />\\r\\n</a>')",
            "content_secure": "document.write('<a href=\\\"https://en.wikipedia.org/wiki/Car\\\" target=\\\"_blank\\\">\\r\\n <img src=\\\"https://upload.wikimedia.org/wikipedia/commons/3/3e/SteamMachineOfVerbiestIn1678.jpg\\\" />\\r\\n</a>')",
            "content_source": "standard",
            "created_on": "2021-02-05 21:56:47",
            "custom_request_template": null,
            "description": null,
            "facebook_audit_feedback": null,
            "facebook_audit_status": null,
            "file_name": null,
            "flash_backup_url": null,
            "flash_backup_url_secure": null,
            "flash_click_variable": null,
            "height": 488,
            "id": 271833576,
            "ios_ssl_audit": null,
            "is_blanking": null,
            "is_expired": false,
            "is_hosted": false,
            "is_prohibited": false,
            "is_rotating": null,
            "is_self_audited": false,
            "is_suspicious": false,
            "landing_page_url": "https://en.wikipedia.org/wiki/Car",
            "language": {
                "id": 1,
                "name": "English"
            },
            "last_activity": "2021-02-05 21:56:47",
            "last_checked": null,
            "media_assets": null,
            "media_url": null,
            "media_url_secure": null,
            "member_id": 1234,
            "mobile": null,
            "native_attribute": null,
            "no_adservers": false,
            "not_found": 0,
            "original_content": "<a href=\"https://en.wikipedia.org/wiki/Car\" target=\"_blank\">\r\n <img src=\"https://upload.wikimedia.org/wikipedia/commons/3/3e/SteamMachineOfVerbiestIn1678.jpg\" />\r\n</a>",
            "original_content_secure": "<a href=\"https://en.wikipedia.org/wiki/Car\" target=\"_blank\">\r\n <img src=\"https://upload.wikimedia.org/wikipedia/commons/3/3e/SteamMachineOfVerbiestIn1678.jpg\" />\r\n</a>",
            "passed_sherlock_audit": true,
            "pixels": null,
            "placement": null,
            "political": null,
            "segments": null,
            "size_in_bytes": 0,
            "sla": "0",
            "sla_eta": "2021-02-08 15:58:47",
            "ssl_status": "pending",
            "status": {
                "hosted_assets_association_complete": null,
                "user_ready": true
            },
            "suspicious_activity_timestamp": null,
            "technical_attributes": [
                {
                    "id": 1,
                    "name": "Image"
                }
            ],
            "template": {
                "id": 6
            },
            "text_description": null,
            "text_display_url": null,
            "text_title": null,
            "thirdparty_campaign_id": null,
            "thirdparty_creative_id": null,
            "thirdparty_page": null,
            "thirdparty_pixels": null,
            "thirdparty_viewability_providers": null,
            "vendors": null,
            "video_attribute": null,
            "width": 682
        },
        "dbg": {
            "output_term": "creative",
            "version": "1.18",
            "warnings": []
        },
        "id": "271833576",
        "num_elements": 100,
        "start_element": 0,
        "status": "OK"
    }
}
```

## Add a bidder instance

The bidder instance object represents a particular bidder server running in the data center. This information stored in this object determines where we send traffic. In this example, we set the data center ID to (NYM).

> [!WARNING]
> This step assumes that you already have a bidder up and running that can respond to bid requests, ready requests, etc., as detailed in the [System Overview](#system-overview).
> [!TIP]
> For more information about configuring a bidder instance, see the [Bidder Instance Service](./bidder-instance-service.md)

In this example we set an IP address and port to which traffic should be sent.

- We also support the use of hostnames.
  - When present, hostnames take precedent.
  - Our bidder-instance service requires an IP address to be present on upload. If you would like to use a hostname, a dummy IP can put placed in the object upload.
- The full path we will send traffic to is
  - https://\[hostname or IP\]:\[port\]\[bidder.bid_uri\]

    - The `bidder.bid_uri` is set in your bidder object.
    - This path should be unique per bidder
- It is also highly recommended that you place a queries per second (QPS) limit on the bidder instance to ensure your servers are not inundated with traffic.
- We highly recommend keeping the bidder instance inactive until you are ready to receive traffic in order to avoid accidental spend.

### Example bidder instance object

```
$ cat create-bidder-instance.json
{
    "instance": {
        "bidder_id": 123,
        "active": true,
        "datacenter_id": 6,
        "ip_address": "10.3.64.215",
        "port": 80
        "qps_limit": 10000,
    }
}
```

### Output

```
$ export IB="https://api.adnxs.com";
$ curl -b cookies -X POST -d @create-bidder-instance.json $IB/bidder-instance/123
{
  "response": {
    "status": "OK",
    "count": 1,
    "start_element": null,
    "num_elements": null,
    "id": 1543,
    "instance": {
      "id": 1543,
      "bidder_id": 123,
      "active": true,
      "datacenter_id": 6,
      "ip_address": "10.3.64.215",
      "port": 80,
      "hostname": null,
      "qps_limit": 10000,
      "dns_interval": null,
      "min_conns": 1,
      "max_conns": null,
      "receive_type_id": 0
    },
    "count": 1,
    "dbg": {
      "output_term": "bidder",
      "version": "1.0.5",
      "warnings": [
        
      ]
    },
    "num_elements": 100,
    "start_element": 0,
    "status": "OK"
  }
}
```

## Bid response

- The bid response should be formatted correctly in order for your bidder to submit bids properly. The required fields can be found [here](./incoming-bid-response-from-bidders.md).

  > [!NOTE]
  > Since you are integrating with buyer seat ID, the seatbid.seat field should be your own internal IDs.

- If you require an example of a bid request to use, your Xandr representative should be able to provide you with one. The supported bid request fields with examples can be found [here](./outgoing-bid-request-to-bidders.md).

### User sync

- In order to inform your bidding activity, we have methods for syncing your internal user IDs with Xandr's.
- For our bidder partners, the norm is to use `/getuid`. More information on this service can be found here: [Synchronize Your User IDs](./synchronize-your-user-ids.md).

## Test the integration

### Ready requests

- In order to receive bid requests from our servers, your bidder must first respond correctly to our ready requests.
- Ready requests are sent to https://\[hostname or IP\]:\[port\]\[bidder.ready_uri\]
  - The `bidder.ready_uri` is set in your bidder object.
- Your response must contain `"1"` somewhere in the body.
- Further Details can be found [here](./ready-request.md).

### Bid stream testing

- Your Xandr Integration Engineer will help you test the bid stream.
- This will likely involve sending you bid requests from a testing publisher page.
- Ideally you will respond to these requests, win our auction, and have your creative served to the test page
- From there you can proceed to
  - Test any macros or trackers to make sure they work as expected.
  - Check that discrepancies are within acceptable ranges.

## Creative registration process

> [!NOTE]
> We recommend you log the Xandr creative IDs on your system.

- Creative pre-registration is a requirement for display, video, and native creatives
  - You must be able to readily upload creatives to our systems and submit them to our audit process
- Review our [Creative Standards and Auditing](./creative-standards-and-auditing.md). Sellers require creatives to pass our audit policies in order to serve on their inventory.
- The registration process involves building API services to
  - Add the creative objects
  - Check for Status updates:
    - `audit_status`: this field indicates if the creative has passed the human audit that confirms the creative renders and clicks properly.
    - `ssl_status`: this field indicates if the creative has passed our automates SSL scanner.
    - `is_prohibited`: this field indicates if the creative has violated one of our policies.
  - Adjusts the creatives to correct any issues, as needed, based on the status fields.
- You can use our client testing environment to test your upload workflows.
  - Creatives submitted to our client testing environment are not audited. Please coordinate with your Xandr Integrations Engineer to test your creatives.
- Your creative submission workflows can be worked on in parallel with bid stream testing.

If you are still not seeing the bid requests you expect, double-check your configuration against the instructions on this page. Contact your Xandr representative if the problem persists.

## Using the client testing environment

The Client Testing environment provides a version of the Impbus and Impbus API that you can use to test your workflows and API implementations. The Client Testing environment's codebase and data are now updated every month. This means your testing environment will never be more than 30 days (and often less) behind the version of Xandr code that is running in Production. In addition, all Production data will also automatically be copied over to the Client Testing environment (including your member accounts and credentials) each month. This will allow far more robust testing against the latest features.

For reference, here are the endpoints for the Production and Client Testing environments.

## Example updates

### Bidder object `ready_uri` and `bid_uri`

Update these fields to ensure our ready requests and bid requests, respectively, are sent to the right endpoints.

#### Example bidder update

```
$ cat update-uris.json
{
    "bidder": {
        "ready_uri": "/example_ready_endpoint",
        "bid_uri": "/example_bid_endpoint"

    }
}
```

#### Example bidder update output

```
$ export IB="https://api.adnxs.com";
$ curl -b cookies -X PUT -d @update-uris.json $IB/bidder/1234?fields=active,bid_uri,id,ready_uri

{
    "response": {
        "bidder": {
            "active": true,
            "bid_uri": "/example_bid_endpoint",
            "id": 1234,
            "ready_uri": "/ready/",
        },
        "count": 1,
        "dbg": {
            "output_term": "bidder",
            "version": "1.0.5",
            "warnings": []
        },
        "id": "1234",
        "num_elements": 100,
        "start_element": 0,
        "status": "OK"
    }
} 
```

### Update member object audit notify email

Update these fields to ensure you receive notifications for creatives you upload to our system.

#### Example member update

```
$ cat update-email.json
{
    "member": {
        "audit_notify_email": "your_email@email.com"

    }
}
```

#### Example member update output

```
$ export IB="https://api.adnxs.com";
$ curl -b cookies -X PUT -d @update-email.json $IB/member/5678?fields=active,audit_notify_email,id

{
    "response": {
        "member": {
            "active": true,
            "audit_notify_email": "your_email@email.com",
            "id": 5678,
        },
        "count": 1,
        "dbg": {
            "output_term": "member",
            "version": "1.0.5",
            "warnings": []
        },
        "id": "5678",
        "num_elements": 100,
        "start_element": 0,
        "status": "OK"
    }
} 
```

## Related topics

- [Bidder Instance Service](./bidder-instance-service.md)
- [Bidder Profile Service](./enhanced-bidder-profiles.md)
- [Creative Service](./creative-service.md)
- [Bid Request Specification](./outgoing-bid-request-to-bidders.md)
- [Bid Response Specification](./incoming-bid-response-from-bidders.md)
