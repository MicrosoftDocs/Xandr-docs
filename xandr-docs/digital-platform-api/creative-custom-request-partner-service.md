---
title: Creative Custom Request Partner Service
description: In this article, learn about the Creative Custom Request Partner service, their JSON fields, and REST API with thorough examples.
ms.date: 10/07/2024
ms.custom: digital-platform-api
---

# Creative Custom Request Partner service

> [!NOTE]
> Mediation is only available to Microsoft Monetize Ad Server customers.

For context on mediation, see [Selling Your Inventory through Mediation](../monetize/mediation-selling-your-inventory-through-mediation.md).

Mediation partners, also known as custom request partners, can be identified and defined through this service. These partners are assigned to customer-specific Networks via the [UI](../monetize/mediation-networks.md) or [Mediated Network Service](mediated-network-service.md).

Each partner is also associated with templates defined in the [Creative Custom Request Template Service](creative-custom-request-template-service.md).

## REST API

| HTTP Method | Endpoint | Description |
|---|---|---|
| `GET` | [https://api.appnexus.com/creative-custom-request-partner](https://api.appnexus.com/creative-custom-request-partner) | View all partners. |
| `GET` | [https://api.appnexus.com/creative-custom-request-partner?id=NETWORK_ID](https://api.appnexus.com/creative-custom-request-partner?id=NETWORK_ID) | View a specific partner. |
| `POST` | [https://api.appnexus.com/creative-custom-request-partner](https://api.appnexus.com/creative-custom-request-partner) | Create a new partner. |
| `PUT` | [https://api.appnexus.com/creative-custom-request-partner?id=NETWORK_ID](https://api.appnexus.com/creative-custom-request-partner?id=NETWORK_ID)| Update a partner. |
| `DELETE` | [https://api.appnexus.com/creative-custom-request-partner?id=NETWORK_ID](https://api.appnexus.com/creative-custom-request-partner?id=NETWORK_ID) | Delete a partner. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The unique identification number of the custom partner. |
| `name` | string | The name of the partner.<br>**Required On:** `POST` |
| `macro_type` | string | Indicates the type of macros used to define the partner. Allowed values:<br> - `standard`: The integration is not via a user-defined **Custom Network**, and has access to our standard creative macros to build the request. This can include supported SDK integrations.<br> - `customsdk`: The integration is with a user-created **Custom Mobile Network**.<br> - `customweb`: The integration is with a user-created **Custom Web Network**.<br> - `customvideo`: The integration is with a user-created **Custom Video Network**.<br>**Default:** `standard` <br>**Required On:** `POST` |
| `member_id` | int | Determines who can use this custom creative request partner. A value of `0` indicates that any member can integrate with (i.e., use mediation to sell to) this partner. If the value is a particular non-zero member ID, the partner is only available to that member.<br>**Default:** `0` |
| `last_modified` | datetime | **Read Only.** The date and time that this record was last changed. |
| `creative_custom_request_templates` | array | This array contains details about the macros that will be used by this custom partner. This can be `null` if no macro information is required. For more details, see [Creative Custom Request Template Service](creative-custom-request-template-service.md). |
<!-- | `creative_custom_request_partner_credentials` | array | This array contains information about the authentication credentials required for this custom request partner. This can be `null` if no credential information is required. For more details, see [Creative Custom Request Partner Credentials](#creative-custom-request-partner-credentials) below. |
| `creative_custom_request_partner_integration` | array | This array indicates whether the partner is supported and active. This can be `null` if no integration information is required. For more details, see [Creative Custom Request Integration](#creative-custom-request-integration) below. | -->

<!-- ### Creative custom request partner credentials

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The unique ID of this set of partner credentials. |
| `creative_custom_request_partner_id` | int | The ID of the custom request partner that these credentials are associated with. |
| `name` | string | The name of this particular credential object, e.g., `"username"`, `"password"`. This is not limited to usernames or passwords; it could also be an Oauth key. |
| `is_required` | boolean | Indicates whether this credentials field is required. |
| `is_obscured` | boolean | Tells whether to obscure this field from the user. |
| `last_modified` | datetime |**Read Only.** The date and time when this record was last changed. |
| `type` | string | Indicates the type of value that this parameter will accept. The values are the same as those specified in the `type` field of the [Creative Custom Request Template Service](creative-custom-request-template-service.md)'s `macro` object, since the credentials functionality is designed and implemented in terms of template macros:<br> - `decimal`<br> - `integer`<br> - `select_from_list`<br> - `"string"`<br> - `string_list`<br> - `true_false`<br> - `url`<br>The default value is `"string"`. |

### Creative custom request integration

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The unique ID associated with this partner's integration information. |
| `creative_custom_request_partner_id` | int | The custom request partner associated with this integration information. |
| `supported` | boolean | This is set to `true` if we support pulling data from this network for use in our publisher reporting. |
| `active` | boolean | Whether we are currently able to collect data from the partner or not. In other words, whether we are able to log in to this network's systems. |
| `last_modified` | datetime | **Read Only.** The date and time when this record was last changed. |
| `data_timezone` | string | The time zone used by the reporting system that we pulled the data from. |
| `data_granularity` | string | How often we pull data from the external partner. Allowed values:<br> - `daily`<br> - `hourly` |

### Creative custom request template

For a list of this object's fields and their definitions, see the [Creative Custom Request Template Service](creative-custom-request-template-service.md). -->

## Examples

### View all custom partners

```
{code}$ curl -b cookies -c cookies 'https://api.appnexus.com/creative-custom-request-partner'
{
    "response":{
        "status":"OK",
        "count":19,
        "start_element":0,
        "num_elements":100,
        "creative-custom-request-partners":[
            {
                "id":1,
                "name":"unknown",
                "macro_type":"standard",
                "member_id":null,
                "last_modified":"2014-03-21 21:43:33",
                "creative_custom_request_templates":[
                    {
                        "id":14,
                        "name":null,
                        "type_id":6,
                        "creative_custom_request_partner_id":1,
                        "member_id":0,
                        "hostname":null,
                        "uri":null,
                        "port":80,
                        "is_post":false,
                        "content":"[ { \"tag\":\"#{TAG}\" } ] ",
                        "timeout_ms":0,
                        "is_client":true,
                        "last_modified":"2014-03-18 13:30:44",
                        "macros":[
                            {
                                "id":68,
                                "template_id":14,
                                "code":"TAG",
                                "name":"TAG",
                                "type":"string",
                                "is_required":false,
                                "last_modified":"2014-03-18 13:30:44"
                            }
                        ]
                    },
                    {
                        "id":39,
                        "name":null,
                        "type_id":6,
                        "creative_custom_request_partner_id":1,
                        "member_id":0,
                        "hostname":null,
                        "uri":null,
                        "port":80,
                        "is_post":false,
                        "timeout_ms":0,
                        "is_client":true,
                        "last_modified":"2014-04-29 20:25:04",
                        "macros":null
                    },
                    {
                        "id":40,
                        "name":"Millennial Media Async",
                        "type_id":6,
                        "creative_custom_request_partner_id":1,
                        "member_id":0,
                        "hostname":null,
                        "uri":null,
                        "port":80,
                        "is_post":false,
                        "content":"[ { \"tag\":\"document.write('window.async = true; var cb = function(adFilled) { window.async = false; if (!adFilled) ADNXSMediation.noAd(); setTimeout(function(){ ADNXSMediation.next() }, 0); } ; window.mmAPI.placeAd({ containerElementId: \\\"adContainer\\\", apid: \\\"#{APID} \\\", placementType: \\\"inline\\\", width: ${WIDTH}, height: ${HEIGHT}, allowLocation: #{LOC} }, cb);');\" } ] ",
                        "timeout_ms":0,
                        "is_client":true,
                        "last_modified":"2014-05-27 19:45:45",
                        "macros":[
                            {
                                "id":118,
                                "template_id":40,
                                "code":"APID",
                                "name":"APID",
                                "type":"string",
                                "is_required":true,
                                "last_modified":"2014-05-27 19:45:45"
                            },
                            {
                                "id":119,
                                "template_id":40,
                                "code":"LOC",
                                "name":"Allow Location",
                                "type":"true_false",
                                "is_required":true,
                                "last_modified":"2014-05-27 19:45:45"
                            }
                        ]
                    },
                    {
                        "id":41,
                        "name":"Millennial Media Async",
                        "type_id":6,
                        "creative_custom_request_partner_id":1,
                        "member_id":0,
                        "hostname":null,
                        "uri":null,
                        "port":80,
                        "is_post":false,
                        "content":"[ { \"tag\": \"http:\/\/s3.amazonaws.com\/APN-test\/millennial-web-2.js\", \"vars\":\"var APN={ } ;APN.apid='#{APID} ';APN.w=${WIDTH} ;APN.h=${HEIGHT} ;APN.loc=#{ LOC } ;\", \"width\":${WIDTH}, \"height\":${HEIGHT} } ] ",
                        "timeout_ms":0,
                        "is_client":true,
                        "last_modified":"2014-05-30 13:28:41",
                        "macros":[
                            {
                                "id":120,
                                "template_id":41,
                                "code":"APID",
                                "name":"APID",
                                "type":"string",
                                "is_required":true,
                                "last_modified":"2014-05-27 20:09:25"
                            },
                            {
                                "id":121,
                                "template_id":41,
                                "code":"LOC",
                                "name":"Allow Location",
                                "type":"true_false",
                                "is_required":true,
                                "last_modified":"2014-05-27 20:09:25"
                            }
                        ]
                    },
                    {
                        "id":42,
                        "name":"Millennial Media Async",
                        "type_id":6,
                        "creative_custom_request_partner_id":1,
                        "member_id":0,
                        "hostname":null,
                        "uri":null,
                        "port":80,
                        "is_post":false,
                        "content":"[ { \"tag\": \"document.write(\\\" window.async = true; var cb = function(adFilled) { window.async = false;  if (!adFilled) ADNXSMediation.noAd();  setTimeout(function(){ ADNXSMediation.next() }, 0); } ; window.mmAPI.placeAd({ containerElementId: \\\\\"adContainer\\\\\", apid: \\\\\"#{APID} \\\\\", placementType: \\\\\"inline\\\\\", width: #{WIDTH}, height: #{HEIGHT}, allowLocation: #{LOC} }, cb);\\\");\" } ] ",
                        "timeout_ms":0,
                        "is_client":true,
                        "last_modified":"2014-05-27 21:31:29",
                        "macros":[
                            {
                                "id":122,
                                "template_id":42,
                                "code":"APID",
                                "name":"APID",
                                "type":"string",
                                "is_required":true,
                                "last_modified":"2014-05-27 21:31:29"
                            },
                            {
                                "id":123,
                                "template_id":42,
                                "code":"LOC",
                                "name":"Allow Location",
                                "type":"true_false",
                                "is_required":true,
                                "last_modified":"2014-05-27 21:31:29"
                            }
                        ]
                    }
                ]
            },
            {
                "id":17,
                "name":"inMobi",
                "macro_type":"standard",
                "member_id":null,
                "last_modified":"2014-04-23 22:24:46",
                "creative_custom_request_templates":null
            },
}
{code}
```

### View custom partners associated with a specific member

```
{code}
$ curl -b cookies -c cookies 'https://api.appnexus.com/creative-custom-request-partner?id=17'    
{
    "response":{
        "status":"OK",
        "count":1,
        "start_element":0,
        "num_elements":100,
        "creative-custom-request-partner":{
            "id":17,
            "name":"inMobi",
            "macro_type":"standard",
            "member_id":null,
            "last_modified":"2014-04-23 22:24:46",
            "creative_custom_request_templates":null
        }
    }
}           
}
{code}
```

### Create a custom partner

```
{code}$ cat create-custom-creative-request-partner-service.json
{
    "creative-custom-request-partner": {
        "name": "Fred's Company",
        "macro_type": "standard"
    }
}
$ curl -b cookies -c cookies -X POST -d @custom-creative-request-partner-service.json 'https://api.appnexus.com/creative-custom-request-partner'
 
{
    "response":{
        "status":"OK",
        "count":1,
        "id":49,
        "start_element":0,
        "num_elements":100,
        "creative-custom-request-partner":{
            "id":49,
            "name":"Fred's Company",
            "macro_type":"standard",
            "member_id":null,
            "last_modified":"2014-06-02 17:55:27",
            "creative_custom_request_templates":null
        }
    }
}
{code}
```

### Edit a custom partner

```
{code}$ cat edit-custom-creative-request-partner-service.json
{
    "creative-custom-request-partner":{
        "member_id": 3261
    }
}
$ curl -b cookies -c cookies -X PUT -d @edit-ccr-partner-service.json 'https://api.appnexus.com/creative-custom-request-partner?id=17'
{
    "response":{
        "status":"OK",
        "count":1,
        "id":"17",
        "start_element":0,
        "num_elements":100,
        "creative-custom-request-partner":{
            "id":17,
            "name":"inMobi",
            "macro_type":"standard",
            "member_id":3261,
            "last_modified":"2014-06-03 14:36:49",
            "creative_custom_request_templates":null
        }
    }
}            
{code}
```

### Delete a custom partner

```
{code}$ curl -b cookies -c cookies -X DELETE 'https://api.appnexus.com/creative-custom-request-partner?id=49'
{
    "response": {
        "status":"OK",
        ...
    }
}
{code}
```

## Related topics

- [Mediated Bid Service](mediated-bid-service.md)
- [Mediated Network Service](mediated-network-service.md)
- [Creative Custom Request Template Service](creative-custom-request-template-service.md)
- [Creative Custom Request Template Type Service](creative-custom-request-template-type-service.md)
- [Creative Template Service](creative-template-service.md)
- [Creative Service](creative-service.md)
