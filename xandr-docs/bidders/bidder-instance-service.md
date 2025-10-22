---
title: Bidder Instance Service
description: Explore this article to understand the Bidder Instance service, including its JSON fields, REST API, and a detailed set of examples.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidder Instance service

A bidder will likely have at least two instances running at any given time. Each instance is associated with the impression bus in one of the Xandr datacenters. The instance itself may either be hosted with Xandr at the datacenter or located nearby. To decrease latency for global impressions, you may set up bidder instances in the various Xandr datacenters (see `datacenter_id` below). Each bidder instance is associated with one datacenter. As load on your bidders increases, you will likely require multiple instances per datacenter. Instead of setting up your own local load-balancing pool for these multiple instances, the impression bus can handle the load balancing for you.

You will need to register the hostname/IP/port combination for each of your bidder instances with the impression bus using the Bidder Instance Service API. This API service also allows you to view, modify, and remove any instances. Each bidder instance must use the nomenclature for request handlers that is defined by the [Bidder Service](bidder-service.md).

> [!NOTE]
> For answers to frequently asked questions about how bidder instances work, see the [Bidder Instance - FAQ](bidder-instance---faq.md).

## REST API

| HTTP Method | Endpoint | Description |
|---|---|---|
| `GET` | [https://api.adnxs.com/bidder-instance/BIDDER_ID](https://api.adnxs.com/bidder-instance/BIDDER_ID) | View all bidder instances. It won't show other user's bidders. |
| `GET` | [https://api.adnxs.com/bidder-instance/BIDDER_ID/BIDDER_INSTANCE_ID](https://api.adnxs.com/bidder-instance/BIDDER_ID/BIDDER_INSTANCE_ID) | View a particular bidder instance. |
| `POST`  | [https://api.adnxs.com/bidder-instance/BIDDER_ID](https://api.adnxs.com/bidder-instance/BIDDER_ID)<br>(bidder instance JSON) | Add a new bidder instance. |
| `PUT`  | [https://api.adnxs.com/bidder-instance/BIDDER_ID/BIDDER_INSTANCE_ID](https://api.adnxs.com/bidder-instance/BIDDER_ID/BIDDER_INSTANCE_ID)<br>(bidder instance JSON) | Modify an existing bidder.<br><br>**Note:** The bidder instance service currently does not support deletes - to remove an instance, set it to inactive.<br><br>**Warning:** When creating/modifying bidder instances, never use the deprecated "datacenter" parameter to set the datacenter for your instance. Instead, always use the "datacenter_id" parameter with the IDs defined below. |

## JSON fields

| Field | Required | Type | Description |
|:---|:---|:---|:---|
| `id` | yes (on `PUT`) | int | The ID of the bidder instance. |
| `bidder_id` | yes | int | The ID of the bidder. |
| `active` | no, default is true | boolean | Whether the bidder instance is active or not. |
| `datacenter_id` | yes (on `POST`) | int | The datacenter ID with which your instance is associated NYM = 6, LAX = 4, , AMS = 15 , FRA = 7, SIN = 13. Legacy IDs: AMS = 12 (until July 12, 2022), SIN = 8 (until October 15, 2019) |
| `ip_address` | yes | string | IP address for the bidder instance. |
| `port` | yes | int | Port for the bidder instance. |
| `last_activity` | no | timestamp | The timestamp of last modification to this bidder instance. |
| `hostname` | no | varchar(128) | The hostname for the bidder instance (Be sure not to include 'https://' - eg. "hostname":"rtb.yourdomain.com") |
| `qps_limit` | no | int | The max queries per second sent to this bidder instance. |

> [!NOTE]
> QPS limits **must** be set the same for all bidder instances in a datacenter. To do this, set the `qps_limit` to the same value for all bidder instances active in a datacenter. For example, if you have three bidder instances in LAX, and want to set the QPS limit to 50,000 for the entire datacenter, you would set the `qps_limit` to 50,000 on each of the three bidder instances. If `qps_limit` is not the same across all bidder instances within a datacenter, you may get unintended results, so ensure that the `qps_limit` values are the same in each datacenter.
>
> You can add a hostname to your bidder instance at any time. However, our api requires an ip address when adjusting the bidder instance, but if you include a hostname field with a value (your url or domain) in the api call, our systems will connect to the hostname and ignore the ip address. If you are posting a new bidder instance with a hostname, you can use a placeholder value for the ip_address field.

## Examples

### Authentication token

Authentication is always the first step when using the API Services. The authentication token can then be written to our cookie file for future use. For more detailed instructions, see [Authentication Service](authentication-service.md).

### View existing instances

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/bidder-instance/2'
{
   "response":{
      "status":"OK",
      "instances":[
         {
            "id":14,
            "bidder_id":2,
            "active":true,
                "datacenter_id": 6,
            "ip_address":"8.12.231.108",
            "port":8081,
            "last_activity":"2016-12-31 17:07:17"
            "hostname": null
         }
      ]
   }
}
```

### Add new instance

I have a New York (NYM2) instance; now I want to register my LAX1 bidder instance. I create the following JSON:

```
$ cat bidder_instance
{
   "instance":{
      "bidder_id":2,
      "active":true,
      "datacenter_id":4,
      "ip_address":"8.12.231.108",
      "port":8081,
      "hostname":"rtb.yourdomain.com"
   }
}
```

Then to add this new instance to my bidder (2):

```
$ curl -b cookies -c cookies -X POST --data-binary @bidder_instance 'https://api.adnxs.com/bidder-instance/2'
{
   "response":{
      "status":"OK",
      "id":53
   }
}
```

And to view the newly added instance:

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/bidder-instance/2/53'
{
   "response":{
      "status":"OK",
      "instance":[
         {
            "id":53,
            "bidder_id":2,
            "active":true,
            "datacenter_id":4,
            "ip_address":"64.210.63.108",
            "port":8081,
            "last_activity":"2016-12-31 19:24:23"
            "hostname":"rtb.yourdomin.com"
         }
      ]
   }
}
```

### Add a QPS cap to an existing instance

If I want to add a QPS cap to an existing instance:

```
$ cat bidder-instance
{
   "instance":{
      "id":53,
      "qps_limit":75000
   }
}
$ curl -b cookies -c cookies -X PUT --data-binary @bidder-instance  "https://api.adnxs.com/bidder-instance/2/53"
{
   "response":{
      "status":"OK",
      "id":53
   }
}
```

Then if I want to view the instance:

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/bidder-instance/2'
{
   "response":{
   "status":"OK",
      "instances":[
         {
            "id":14,
            "bidder_id":2,
            "active":true,
            "datacenter_id":6,
            "ip_address":"8.12.231.108",
            "port":8081,
            "last_activity":"2016-12-31 17:07:17"
            "hostname":null
         },
         {
            "id":53,
            "bidder_id":2,
            "active":true,
            "datacenter_id":4,
            "ip_address":"64.210.63.124",
            "port":8081,
                        "qps_limit":75000
            "last_activity":"2016-12-31 19:51:13"
            "hostname":"rtb.yourdomain.com"         }
      ]
   }
}
```

### Modifying an instance

If I need to change an IP address:

```
$ cat bidder-instance
{
   "instance":{
      "id":53,
      "ip_address":"64.210.63.124"
   }
}
$ curl -b cookies -c cookies -X PUT --data-binary @bidder-instance  "https://api.adnxs.com/bidder-instance/2/53"
{
   "response":{
      "status":"OK",
      "id":53
   }
}
```

Then to view the current status of all instances for my bidder(2):

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/bidder-instance/2'
{
   "response":{
   "status":"OK",
      "instances":[
         {
            "id":14,
            "bidder_id":2,
            "active":true,
            "datacenter_id":6,
            "ip_address":"8.12.231.108",
            "port":8081,
            "last_activity":"2016-12-31 17:07:17"
            "hostname":null
         },
         {
            "id":53,
            "bidder_id":2,
            "active":true,
            "datacenter_id":4,
            "ip_address":"64.210.63.124",
            "port":8081,
            "last_activity":"2016-12-31 19:51:13"
            "hostname":"rtb.yourdomain.com"         }
      ]
   }
   }
```

## Related topics

- [Bidder Instance - FAQ](bidder-instance---faq.md)
- [Bidder Service](bidder-service.md)
