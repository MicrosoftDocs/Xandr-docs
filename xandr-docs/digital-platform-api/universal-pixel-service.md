---
title: Universal Pixel Service
description: Explore the Universal Pixel service, enabling access to one or more Universal Pixels and any associated audiences and conversions.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Universal Pixel service

The Universal Pixel Service is a set of REST API services that give you access to one or more Universal Pixels and any associated audiences and conversions.

## Universal Pixel service overview

The Universal Pixel provides insights into the interactions that users have with your website so you can easily segment these users, measure actions they take, and better target your ads. The Universal Pixel Service has three sets of endpoints:

- [Universal-Pixel REST API](#universal-pixel-rest-api) - To create, delete, view, and update a Universal Pixel.
- [Audience REST API](#audience-rest-api) - To create, delete, view, and update an audience.
- [Conversion REST API](#conversion-rest-api) - To create, delete, view, and update a conversion.

See below for [examples](#examples) of each Universal Pixel endpoint.

### Universal Pixel REST API (endpoint)

You can create a Universal Pixel using the **`/universal-pixel`** endpoint. Once a Universal Pixel is created, you can use the **`/universal-pixel`** endpoint to view it, update it, or delete it.

### Audience REST API (endpoint)

You can create a Universal Pixel audience using **`/universal-pixel/audience`** endpoint. Once an audience is created, you can use the **`/universal-pixel/audience`** endpoint to view it, updated it, or delete it.

### Conversion REST API (endpoint)

You create a Universal Pixel conversion using **`/universal-pixel/conversion`** endpoint. Once a conversion is created, you can use the **`/universal-pixel/conversion`** endpoint to view it, updated it, or delete it.

## Universal Pixel REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/universal-pixel/pixel](https://api.appnexus.com/universal-pixel/pixel) | View a list of Universal Pixels associated with a member or advertiser. |
| `POST` | [https://api.appnexus.com/universal-pixel/pixel](https://api.appnexus.com/universal-pixel/pixel) | Create a new Universal Pixel. |
| `GET` | [https://api.appnexus.com/universal-pixel/pixel/PIXEL_ID](https://api.appnexus.com/universal-pixel/pixel/PIXEL_ID) | View a Universal Pixel by ID. |
| `PUT` | [https://api.appnexus.com/universal-pixel/pixel/PIXEL_ID](https://api.appnexus.com/universal-pixel/pixel/PIXEL_ID) | Update a Universal Pixel by ID. |
| `DELETE` | [https://api.appnexus.com/universal-pixel/pixel/PIXEL_ID](https://api.appnexus.com/universal-pixel/pixel/PIXEL_ID) | Delete a Universal Pixel by ID. |
| `GET` | [https://api.appnexus.com/universal-pixel/pixel-uuid/PIXEL_UUID](https://api.appnexus.com/universal-pixel/pixel-uuid/PIXEL_UUID) | View a Universal Pixel by UUID. |

### View a list of Universal Pixels

#### Query fields

| Field | Type | Description |
|:---|:---|:---|
| `member_id` | integer | ID of a member associated with Universal Pixel for operation. |
| `advertiser_id` | integer | ID of an advertiser associated with Universal Pixel. |
| `sort` | string | Sort by field and direction:<br>- ID ascending = `id.asc`<br>- ID descending = `id.dsc`<br>**Default**: `id.asc` |
| `num_elements` | integer | Number of elements to return; **maximum** = `1000`, **minimum** = `1`, **default** = `1000`. |
| `start_element` | integer | Starting element (used for paging); **default** = `0`. |

#### JSON fields (response body)

| Field | Type | Description |
|:---|:---|:---|
| `data` | array | Array of Universal Pixel objects. |
| `id` | integer | Universal Pixel ID assigned by the API. |
| `name` | string | Name of the Universal Pixel. |
| `uuid` | string | Unique ID for the Universal Pixel assigned by the API. |
| `member_id` | integer | ID of member associated with Universal Pixel. |
| `advertiser_id` | integer | ID of advertiser associated with Universal Pixel. |
| `created_on` | string | Timestamp the Universal Pixel was created. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |
| `last_updated` | string | Timestamp when the Universal Pixel was last updated. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |

### Create a new Universal Pixel

#### Query fields for creating a new Universal Pixel

| Field | Type | Description |
|:---|:---|:---|
| `member_id` | integer | ID of a member associated with Universal Pixel for operation. |

#### JSON fields (request body) for creating a new Universal Pixel

| Field | Type | Description |
|:---|:---|:---|
| `name` | string | Name of the Universal Pixel. Minimum length of string is 1 and maximum is 100. This is a **required** field. |
| `advertiser_id` | integer | ID of advertiser associated with Universal Pixel. |

#### JSON fields (response body) for creating a new Universal Pixel

| Field | Type | Description |
|:---|:---|:---|
| `id` | integer | Universal Pixel ID assigned by the API. |
| `name` | string | Name of the Universal Pixel. |
| `uuid` | string | Unique ID for the Universal Pixel assigned by the API. |
| `member_id` | integer | ID of member associated with Universal Pixel. |
| `advertiser_id` | integer | ID of advertiser associated with Universal Pixel. |
| `created_on` | string | Timestamp the Universal Pixel was created. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |
| `last_updated` | string | Timestamp when the Universal Pixel was last updated. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |

### View a Universal Pixel by ID

#### Query fields for viewing a Universal Pixel

| Field | Type | Description |
|:---|:---|:---|
| `id` | integer | ID for the Universal Pixel assigned by the API for operation. |

#### JSON fields (response body) for viewing a Universal Pixel

| Field | Type | Description |
|:---|:---|:---|
| `id` | integer | Universal Pixel ID assigned by the API for operation. |
| `name` | string | Name of the Universal Pixel. |
| `uuid` | string | Unique ID for the Universal Pixel assigned by the API. |
| `member_id` | integer | ID of member associated with Universal Pixel. |
| `advertiser_id` | integer | ID of advertiser associated with Universal Pixel. |
| `created_on` | string | Timestamp the Universal Pixel was created. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |
| `last_updated` | string | Timestamp when the Universal Pixel was last updated. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |

### Update a Universal Pixel by ID

#### Query fields for updating a Universal Pixel

| Field | Type | Description |
|:---|:---|:---|
| `id` | integer | ID for the Universal Pixel assigned by the API for operation. |

#### JSON fields (request body) for updating a Universal Pixel

Any field which needs to be changed from existing value to new one. For example:

| Field | Type | Description |
|:---|:---|:---|
| `name` | string | Updated name of the Universal Pixel. This is a **required** field. |

### Delete a Universal Pixel by ID

#### Query fields for deleting a Universal Pixel

| Field | Type | Description |
|:---|:---|:---|
| `id` | integer | ID for the Universal Pixel assigned by the API which would be deleted. |

### View a Universal Pixel by UUID

#### Query fields for viewing a Universal Pixel by UUID

| Field | Type | Description |
|:---|:---|:---|
| `uuid` | integer | Unique ID for the Universal Pixel assigned by the API for operation. |

#### JSON fields (response body) for viewing a Universal Pixel by UUID

| Field | Type | Description |
|:---|:---|:---|
| `id` | integer | Universal Pixel ID assigned by the API for operation. |
| `name` | string | Name of the Universal Pixel. |
| `uuid` | string | Unique ID for the Universal Pixel assigned by the API. |
| `member_id` | integer | ID of member associated with Universal Pixel. |
| `advertiser_id` | integer | ID of advertiser associated with Universal Pixel. |
| `created_on` | string | Timestamp the Universal Pixel was created. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |
| `last_updated` | string | Timestamp when the Universal Pixel was last updated. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |

## Audience REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/universal-pixel/audience](https://api.appnexus.com/universal-pixel/audience) | View a list of audiences associated with a member or advertiser. |
| `POST` | [https://api.appnexus.com/universal-pixel/audience](https://api.appnexus.com/universal-pixel/audience) | Create a new audience. |
| `GET` | [https://api.appnexus.com/universal-pixel/audience/AUDIENCE_ID](https://api.appnexus.com/universal-pixel/audience/AUDIENCE_ID) | View an audience by ID. |
| `PUT` | [https://api.appnexus.com/universal-pixel/audience/AUDIENCE_ID](https://api.appnexus.com/universal-pixel/audience/AUDIENCE_ID) | Update an audience by ID. |
| `DELETE` | [https://api.appnexus.com/universal-pixel/audience/AUDIENCE_ID](https://api.appnexus.com/universal-pixel/audience/AUDIENCE_ID) | Delete an audience by ID. |

### View a list of audiences

#### Query fields for viewing a list of audiences

| Field | Type | Description |
|:---|:---|:---|
| `member_id` | integer | ID of a member associated with Universal Pixel for operation. |
| `advertiser_id` | integer | ID of an advertiser associated with Universal Pixel. |
| `sort` | string | Sort by field and direction:<br>- ID ascending = `id.asc`<br>- ID descending = `id.dsc`<br>**Default** = `id.asc` |
| `num_elements` | integer | Number of elements to return; **maximum** = `1000`, **minimum** = `1`, **default** = `1000`. |
| `start_element` | integer | Starting element (used for paging); **default** = `0`. |
| `universal_pixel_id` | integer | Universal Pixel ID to filter by. |
| `segment_id` | integer | Segment ID to filter by. |
| `search` | string | Search term. |

#### JSON fields (response body) for viewing a list of audiences

| Field | Type | Description |
|:---|:---|:---|
| `data` | array | Array of Audience objects. |
| `id` | integer | Audience ID assigned by the API. |
| `version_id` | integer | Version ID associated with the audience. |
| `universal_pixel_id` | integer | ID for the Universal Pixel to associate audience with. |
| `advertiser_id` | integer | ID of advertiser associated with the Audience. |
| `name` | string | Name of the Audience. |
| `user_ttl_minutes` | integer | TTL (Time To Live) in minutes for a user in this audience; **maximum** = `259200`, **minimum** = `0`, **default** = `43200`. |
| `segment_id` | integer | Segment ID to use to target this audience. |
| `rule` | object | Rule set for the audience. This field is an object and should contain an array of the rules that must be met to consider a fire of the Universal Pixel to be a conversion. For example, below [rule](#rule-for-the-audience) means the Universal Pixel fire must be on a website that has a domain that contains [microsoft.com](https://www.microsoft.com/), the event for the pixel fire is Purchase, and `item_id` is `123`. |
| `created_on` | string | Timestamp when audience was created. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |
| `published_on` | string | Timestamp when audience was published. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |

##### `rule` for the audience

```
"rule":{"and":[{"domain":{"contains":["microsoft.com"]}},{"event":{"equals":["Purchase"]}},
{"item_id":{"equals":["123"]}}],"pixel_uuid":"0b3758f1-cf0f-46c1-9957-00bd36f19ad0"},
```

### Create a new audience

#### Query fields for creating a new audience

| Field | Type | Description |
|:---|:---|:---|
| `member_id` | integer | ID of a member associated with Audience for operation. |

#### JSON fields (request body) for creating a new audience

| Field | Type | Description |
|:---|:---|:---|
| `name` | string | Name of the Audience. It is a **required** field. |
| `universal_pixel_id` | integer | ID for the Universal Pixel to associate audience with. It is a **required** field. |
| `user_ttl_minutes` | integer | TTL (Time To Live) in minutes for a user in this audience; **maximum** = `259200`, **minimum** = `0`, **default** = `43200`. |
| `rule` | object | Rule set for the audience. This field is a **required** field and an object. It should contain an array of the rules that must be met to consider a fire of the Universal Pixel to be a conversion. For example, below [rule](#rule-for-creating-a-new-audience-request-body) means the Universal Pixel fire must be on a website that has a domain that contains [microsoft.com](https://www.microsoft.com/), the event for the pixel fire is Purchase, and `item_id` is `123`. |

##### `rule` for creating a new audience (request body)

```
"rule":{"and":[{"domain":{"contains":["microsoft.com"]}},
{"event":{"equals":["Purchase"]}},{"item_id":{"equals":["123"]}}],
"pixel_uuid":"0b3758f1-cf0f-46c1-9957-00bd36f19ad0"},
```

#### JSON fields (response body) for creating a new audience

| Field | Type | Description |
|:---|:---|:---|
| `id` | integer | Audience ID assigned by the API. |
| `version_id` | integer | Version ID associated with the audience. |
| `universal_pixel_id` | integer | ID for the Universal Pixel associated audience with. |
| `name` | string | Name of the Audience. |
| `segment_id` | integer | Segment ID to use to target this audience. |
| `user_ttl_minutes` | integer | TTL (Time To Live) in minutes for a user in this audience; **maximum** = `259200`, **minimum** = `0`, **default** = `43200`. |
| `rule` | object | Rule set for the audience. This field is an object and contains an array of the rules that is met to consider a fire of the Universal Pixel to be a conversion. For example, below [rule](#rule-for-creating-a-new-audience-response-body) means the Universal Pixel fire is on a website that has a domain that contains [microsoft.com](https://www.microsoft.com/), the event for the pixel fire is Purchase, and `item_id` is `123`. |
| `created_on` | string | Timestamp when audience was created. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |
| `published_on` | string | Timestamp when audience was published. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |

##### `rule` for creating a new audience (response body)

```
"rule":{"and":[{"domain":{"contains":["microsoft.com"]}},
{"event":{"equals":["Purchase"]}},{"item_id":{"equals":["123"]}}],
"pixel_uuid":"0b3758f1-cf0f-46c1-9957-00bd36f19ad0"},
```

### View an audience by ID

#### Query fields for viewing an audience by ID

| Field | Type | Description |
|:---|:---|:---|
| `id` | integer | ID for the Audience assigned by the API. |

#### JSON fields (response body) for viewing an audience by ID

| Field | Type | Description |
|:---|:---|:---|
| `id` | integer | Audience ID assigned by the API. |
| `version_id` | integer | Version ID associated with the audience. |
| `universal_pixel_id` | integer | ID for the Universal Pixel to associate audience with. |
| `advertiser_id` | integer | ID of advertiser associated with the Audience. |
| `name` | string | Name of the Audience. |
| `user_ttl_minutes` | integer | TTL (Time To Live) in minutes for a user in this audience; **maximum** = `259200`, **minimum** = `0`, **default** = `43200`. |
| `segment_id` | integer | Segment ID to use to target this audience. |
| `rule` | object | Rule set for the audience. This field is an object and contains an array of the rules that must be met to consider a fire of the Universal Pixel to be a conversion. For example, below [rule](#rule-for-viewing-an-audience-by-id-response-body) means the Universal Pixel fire must be on a website that has a domain that contains [microsoft.com](https://www.microsoft.com/), the event for the pixel fire is Purchase, and `item_id` is `123`. |
| `created_on` | string | Timestamp when audience was created. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |
| `published_on` | string | Timestamp when audience was published. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |

##### `rule` for viewing an audience by ID (response body)

```
"rule":{"and":[{"domain":{"contains":["microsoft.com"]}},
{"event":{"equals":["Purchase"]}},{"item_id":{"equals":["123"]}}],
"pixel_uuid":"0b3758f1-cf0f-46c1-9957-00bd36f19ad0"},
```

### Update an audience by ID

#### Query fields for updating an audience by ID

| Field | Type | Description |
|:---|:---|:---|
| `id` | integer | ID for the Audience assigned by the API. |

#### JSON fields (request body) for updating an audience by ID

Any field which needs to be changed from existing value to new one. For example:

| Field | Type | Description |
|:---|:---|:---|
| `name` | string | Updated name of the Audience. This is a **required** field. |
| `rule` | object | Rule set for the audience. This is a **required** field and an object. It should contain an array of the rules that must be met to consider a fire of the Universal Pixel to be a conversion. For example, below [rule](#rule-for-updating-an-audience-by-id-request-body) means the Universal Pixel fire must be on a website that has a domain that contains [microsoft.com](https://www.microsoft.com/), the event for the pixel fire is Purchase, and `item_id` is `123`. |
| `user_ttl_minutes` | integer | TTL (Time To Live) in minutes for a user in this audience; **maximum** = `259200`, **minimum** = `0`, **default** = `43200`. |

##### `rule` for updating an audience by ID (request body)

```
"rule":{"and":[{"domain":{"contains":["microsoft.com"]}},
{"event":{"equals":["Purchase"]}},{"item_id":{"equals":["123"]}}],
"pixel_uuid":"0b3758f1-cf0f-46c1-9957-00bd36f19ad0"},
```

#### JSON fields (response body) for updating an audience by ID

| Field | Type | Description |
|:---|:---|:---|
| `id` | integer | Audience ID assigned by the API. |
| `version_id` | integer | Version ID associated with the audience. |
| `universal_pixel_id` | integer | ID for the Universal Pixel to associate audience with. |
| `advertiser_id` | integer | ID of advertiser associated with the Audience. |
| `name` | string | Name of the Audience. |
| `user_ttl_minutes` | integer | Minutes for this audience to exist; **maximum** = `259200`, **minimum** = `0`, **default** = `43200`. |
| `segment_id` | integer | Segment ID to use to target this audience. |
| `rule` | object | Rule set for the audience. This field is an object and contains an array of the rules that must be met to consider a fire of the Universal Pixel to be a conversion. For example, below [rule](#rule-for-updating-an-audience-by-id-response-body) means the Universal Pixel fire must be on a website that has a domain that contains [microsoft.com](https://www.microsoft.com/), the event for the pixel fire is Purchase, and `item_id` is `123`. |
| `created_on` | string | Timestamp when audience was created. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |
| `published_on` | string | Timestamp when audience was published. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |

##### `rule` for updating an audience by ID (response body)

```
"rule":{"and":[{"domain":{"contains":["microsoft.com"]}},
{"event":{"equals":["Purchase"]}},{"item_id":{"equals":["123"]}}],
"pixel_uuid":"0b3758f1-cf0f-46c1-9957-00bd36f19ad0"},
```

### Delete an audience by ID

#### Query fields for deleting an audience by ID

| Field | Type | Description |
|:---|:---|:---|
| `id` | integer | ID for the Audience assigned by the API which would be deleted. |

## Conversion REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | [https://api.appnexus.com/universal-pixel/conversion](https://api.appnexus.com/universal-pixel/conversion) | View a list of conversions associated with a member or advertiser. |
| `POST` | [https://api.appnexus.com/universal-pixel/conversion](https://api.appnexus.com/universal-pixel/conversion) | Create a new conversion. |
| `GET` | [https://api.appnexus.com/universal-pixel/conversion/CONVERSION_ID](https://api.appnexus.com/universal-pixel/conversion/CONVERSION_ID) | View a conversion by ID. |
| `PUT` | [https://api.appnexus.com/universal-pixel/conversion/CONVERSION_ID](https://api.appnexus.com/universal-pixel/conversion/CONVERSION_ID) | Update a conversion by ID. |
| `DELETE` | [https://api.appnexus.com/universal-pixel/conversion/CONVERSION_ID](https://api.appnexus.com/universal-pixel/conversion/CONVERSION_ID) | Delete a conversion by ID. |

### View a list of conversions

#### Query fields for viewing a list of conversions

| Field | Type | Description |
|:---|:---|:---|
| `member_id` | integer | ID of a member associated with conversions for operation. |
| `advertiser_id` | integer | ID of an advertiser associated with conversions. |
| `sort` | string | Sort by field and direction:<br>- ID ascending = `id.asc`<br>- ID descending = `id.dsc`<br>**Default** = `id.asc` |
| `num_elements` | integer | Number of elements to return; **maximum** = `1000`, **minimum** = `1`, **default** = `1000`. |
| `start_element` | integer | Starting element (used for paging). <br>**Default** = `0`. |
| `universal_pixel_id` | integer | Universal Pixel ID to filter by. |
| `conversion_pixel_id` | integer | ID of legacy conversion pixel. |
| `search` | string | Search term. |

#### JSON fields (response body) for viewing a list of conversions

| Field | Type | Description |
|:---|:---|:---|
| `data` | array | Array of conversion objects. |
| `id` | integer | Conversion ID assigned by the API. |
| `universal_pixel_id` | integer | ID for the Universal Pixel associated with this conversion. |
| `name` | string | Name of the conversion. |
| `conversion_pixel_id` | integer | ID of legacy conversion pixel. |
| `conversion_category_id` | integer | ID of the conversion event category. See the [values](#conversion_category_id-values) of `conversion_category_id`. |
| `conversion_category_custom` | string | Label of the custom conversion event category. This field is set to the string value of what category to include the conversion in.<br>**Note:**<br>This field is only set if `conversion_category_id` is `null`. |
| `count_type` | enum | Type of conversion count - `view`, `click`, or `hybrid`. |
| `min_minutes_per_conversion` | integer | The interval (in minutes) to allow a repeat conversion. Maximum value is `32767` (22 days).<br>- If set to `0`: Count all conversions.<br>- If set to `null` (default): Count one per user. |
| `post_click_value` | number | The value you attribute to a conversion after a click. |
| `post_click_expire_minutes` | number | The interval (in minutes) from impression time allowed for a click conversion to be counted as eligible. Maximum value is `43200` (30 days). If set to `0` or `null`, the maximum lookback window applies. |
| `post_view_value` | number | The value you attribute to a conversion after a view. |
| `post_view_expire_minutes` | number | The interval, in minutes, from the impression time within which a view conversion is eligible. The maximum value is **43,200 minutes (30 days)**. If set to `0` or `null`, the system applies the maximum lookback window. |
| `rule` | object | Rule set for the audience. This field is an object and contains an array of the rules that must be met to consider a fire of the Universal Pixel to be a conversion. For example, below [rule](#rule-for-viewing-a-list-of-conversions-response-body) means the Universal Pixel fire must be on a website that has a domain that contains [microsoft.com](https://www.microsoft.com/), the event for the pixel fire is Purchase, and `item_id` is `123`. |
| `created_on` | string | Timestamp when audience was created. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |
| `published_on` | string | Timestamp when audience was published. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |

##### `conversion_category_id` values

```
{ id: 1, title: ' Page view', event: 'PageView' },
{ id: 2, title: ' Landing page', event: 'LandingPage' },
{ id: 3, title: ' Item view', event: 'ItemView' },
{ id: 4, title: ' Add to cart', event: 'AddToCart' },
{ id: 5, title: ' Initiate checkout', event: 'InitiateCheckout' },
{ id: 6, title: ' Add payment info', event: 'AddPaymentInfo' },
{ id: 7, title: ' Purchase', event: 'Purchase' },
{ id: 8, title: ' Lead', event: 'Lead' },
{ id: null, title: ' Other' },
```

##### `rule` for viewing a list of conversions (response body)

```
"rule": {
"and": [
{
"domain":
{ "contains": [ "microsoft.com" ] }
},
{
"event":
{ "equals": [ "Purchase" ] }
},
{
"item_id":
{ "equals": [ "123" ] }
}
],
"pixel_uuid": "0b3758f1-cf0f-46c1-9957-00bd36f19ad0"
},
```

### Create a new conversion

#### Query fields for creating a new conversion

| Field | Type | Description |
|---|---|---|
| `member_id` | integer | ID of a member associated with Conversion for operation. |

#### JSON fields (request body) for creating a new conversion

| Field | Type | Description |
|:---|:---|:---|
| `universal_pixel_id` | integer | ID for the universal pixel with which this conversion is associated with. This is a **required** field. |
| `name` | string | Name of the conversion. This is a **required** field. |
| `conversion_category_id` | integer | ID of the conversion event category. See the [values](#conversion_category_id-values-for-creating-a-new-conversion-request-body) of `conversion_category_id`. |
| `conversion_category_custom` | string | Label of the custom conversion event category. This field is set to the string value of what category to include the conversion in.<br><br>**Note:** This field is only set if `conversion_category_id` is `null`. |
| `count_type` | enum | Type of conversion count - `view`, `click`, or `hybrid`. This is a **required** field. |
| `min_minutes_per_conversion` | integer | The interval (in minutes) to allow a repeat conversion. Maximum value is `32767` (22 days).<br>- If set to `0`: Count all conversions.<br>- If set to `null` (default): Count one per user. |
| `post_click_value` | number | The value you attribute to a conversion after a click. |
| `post_click_expire_minutes` | number | The interval (in minutes) from impression time allowed for a click conversion to be counted as eligible. Maximum value is `43200` (30 days). If set to `0` or `null`, the maximum lookback window applies. |
| `post_view_value` | number | The value you attribute to a conversion after a view. |
| `post_view_expire_minutes` | number | The interval, in minutes, from the impression time within which a view conversion is eligible. The maximum value is **43,200 minutes (30 days)**. If set to `0` or `null`, the system applies the maximum lookback window.|
| `rule` | object | Rule set for the audience. This is a **required** field and an object. It should contain an array of the rules that must be met to consider a fire of the Universal Pixel to be a conversion. For example, below [rule](#rule-for-creating-a-new-conversion-request-body) means the Universal Pixel fire must be on a website that has a domain that contains [microsoft.com](https://www.microsoft.com/), the event for the pixel fire is Purchase, and `item_id` is `123`. |

##### `conversion_category_id` values for creating a new conversion (request body)

```
{ id: 1, title: ' Page view', event: 'PageView' },
{ id: 2, title: ' Landing page', event: 'LandingPage' },
{ id: 3, title: ' Item view', event: 'ItemView' },
{ id: 4, title: ' Add to cart', event: 'AddToCart' },
{ id: 5, title: ' Initiate checkout', event: 'InitiateCheckout' },
{ id: 6, title: ' Add payment info', event: 'AddPaymentInfo' },
{ id: 7, title: ' Purchase', event: 'Purchase' },
{ id: 8, title: ' Lead', event: 'Lead' },
{ id: null, title: ' Other' },
```

##### `rule` for creating a new conversion (request body)

```
"rule": {
"and": [
{
"domain":
{ "contains": [ "microsoft.com" ] }
},
{
"event":
{ "equals": [ "Purchase" ] }
},
{
"item_id":
{ "equals": [ "123" ] }
}
],
"pixel_uuid": "0b3758f1-cf0f-46c1-9957-00bd36f19ad0"
},
```

#### JSON fields (response body) for creating a new conversion

| Field | Type | Description |
|:---|:---|:---|
| `id` | integer | Conversion ID assigned by the API. |
| `member_id` | integer | ID of a member associated with conversions for operation. |
| `version_id` | integer | Version for this conversion. |
| `universal_pixel_id` | integer | ID for the Universal Pixel associated with this conversion. |
| `name` | string | Name of the conversion. |
| `conversion_pixel_id` | integer | ID of legacy conversion pixel. |
| `conversion_category_id` | integer | ID of the conversion event category. See the [values](#conversion_category_id-values-for-creating-a-new-conversion) of `conversion_category_id`. |
| `conversion_category_custom` | string | Label of the custom conversion event category. This field is set to the string value of what category to include the conversion in.<br><br>**Warning:** This field is only set if `conversion_category_id` is `null`. |
| `count_type` | enum | Type of conversion count - `view`, `click`, or `hybrid`. |
| `min_minutes_per_conversion` | integer | The interval (in minutes) to allow a repeat conversion. Maximum value is `32767` (22 days).<br>- If set to `0`: Count all conversions.<br>- If set to `null` (default): Count one per user. |
| `post_click_value` | number | The value you attribute to a conversion after a click. |
| `post_click_expire_minutes` | number |The interval (in minutes) from impression time allowed for a click conversion to be counted as eligible. Maximum value is `43200` (30 days). If set to `0` or `null`, the maximum lookback window applies. |
| `post_view_value` | number | The value you attribute to a conversion after a view. |
| `post_view_expire_minutes` | number | The interval, in minutes, from the impression time within which a view conversion is eligible. The maximum value is **43,200 minutes (30 days)**. If set to `0` or `null`, the system applies the maximum lookback window. |
| `rule` | object | Rule set for the audience. This field is an object and contains an array of the rules that must be met to consider a fire of the Universal Pixel to be a conversion. For example, below [rule](#rule-for-creating-a-new-conversion-response-body) means the Universal Pixel fire must be on a website that has a domain that contains [microsoft.com](https://www.microsoft.com/), the event for the pixel fire is Purchase, and `item_id` is `123`.|
| `created_on` | string | Timestamp when audience was created. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |
| `published_on` | string | Timestamp when audience was published. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |

##### `conversion_category_id` values for creating a new conversion

```
{ id: 1, title: ' Page view', event: 'PageView' },
{ id: 2, title: ' Landing page', event: 'LandingPage' },
{ id: 3, title: ' Item view', event: 'ItemView' },
{ id: 4, title: ' Add to cart', event: 'AddToCart' },
{ id: 5, title: ' Initiate checkout', event: 'InitiateCheckout' },
{ id: 6, title: ' Add payment info', event: 'AddPaymentInfo' },
{ id: 7, title: ' Purchase', event: 'Purchase' },
{ id: 8, title: ' Lead', event: 'Lead' },
{ id: null, title: ' Other' },
```

##### `rule` for creating a new conversion (response body)

```
"rule": {
"and": [
{
"domain":
{ "contains": [ "microsoft.com" ] }
},
{
"event":
{ "equals": [ "Purchase" ] }
},
{
"item_id":
{ "equals": [ "123" ] }
}
],
"pixel_uuid": "0b3758f1-cf0f-46c1-9957-00bd36f19ad0"
},
```

### View a conversion by ID

#### Query fields for viewing a conversion by ID

| Field | Type | Description |
|:---|:---|:---|
| `id` | integer | ID for the Universal Pixel assigned by the API for operation. |

#### JSON fields (response body) for viewing a conversion by ID

| Field | Type | Description |
|:---|:---|:---|
| `id` | integer | Conversion ID assigned by the API. |
| `member_id` | integer | ID of a member associated with conversions for operation. |
| `version_id` | integer | Version for this conversion. |
| `universal_pixel_id` | integer | ID for the Universal Pixel associated with this conversion. |
| `name` | string | Name of the conversion. |
| `conversion_pixel_id` | integer | ID of legacy conversion pixel. |
| `conversion_category_id` | integer | ID of the conversion event category. See the [values](#conversion_category_id-values-for-viewing-a-conversion-by-id) of `conversion_category_id`. |
| `conversion_category_custom` | string | Label of the custom conversion event category. This field is set to the string value of what category to include the conversion in.<br><br>**Important:**<br>This field is only set if `conversion_category_id` is `null`. |
| `count_type` | enum | Type of conversion count - `view`, `click` or `hybrid`. |
| `min_minutes_per_conversion` | integer | The interval (in minutes) to allow a repeat conversion. Maximum value is `32767` (22 days).<br>- If set to `0`: Count all conversions.<br>- If set to `null` (default): Count one per user. |
| `post_click_value` | number | The value you attribute to a conversion after a click. |
| `post_click_expire_minutes` | number | The interval (in minutes) from impression time allowed for a click conversion to be counted as eligible. Maximum value is `43200` (30 days). If set to `0` or `null`, the maximum lookback window applies.|
| `post_view_value` | number | The value you attribute to a conversion after a view. |
| `post_view_expire_minutes` | number | The interval, in minutes, from the impression time within which a view conversion is eligible. The maximum value is **43,200 minutes (30 days)**. If set to `0` or `null`, the system applies the maximum lookback window. |
| `rule` | object | Rule set for the audience. This field is an object and contains an array of the rules that must be met to consider a fire of the Universal Pixel to be a conversion. For example, below [rule](#rule-for-viewing-a-conversion-by-id-response-body) means the Universal Pixel fire must be on a website that has a domain that contains [microsoft.com](https://www.microsoft.com/), the event for the pixel fire is Purchase, and `item_id` is `123`. |
| `created_on` | string | Timestamp when audience was created. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |
| `published_on` | string | Timestamp when audience was published. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |

##### `conversion_category_id` values for viewing a conversion by ID

```
{ id: 1, title: ' Page view', event: 'PageView' },
{ id: 2, title: ' Landing page', event: 'LandingPage' },
{ id: 3, title: ' Item view', event: 'ItemView' },
{ id: 4, title: ' Add to cart', event: 'AddToCart' },
{ id: 5, title: ' Initiate checkout', event: 'InitiateCheckout' },
{ id: 6, title: ' Add payment info', event: 'AddPaymentInfo' },
{ id: 7, title: ' Purchase', event: 'Purchase' },
{ id: 8, title: ' Lead', event: 'Lead' },
{ id: null, title: ' Other' },
```

##### `rule` for viewing a conversion by ID (response body)

```
"rule": {
"and": [
{
"domain":
{ "contains": [ "microsoft.com" ] }
},
{
"event":
{ "equals": [ "Purchase" ] }
},
{
"item_id":
{ "equals": [ "123" ] }
}
],
"pixel_uuid": "0b3758f1-cf0f-46c1-9957-00bd36f19ad0"
},
```

### Update a conversion by ID

#### Query fields for updating a conversion by ID

| Field | Type | Description |
|:---|:---|:---|
| `id` | integer | ID for the Conversion assigned by the API for operation. |

#### JSON fields (request body) for updating a conversion by ID

Any field which needs to be changed from existing value to new one. For example:

| Field | Type | Description |
|:---|:---|:---|
| `name` | string | Name of the conversion. |
| `conversion_category_id` | integer | ID of the conversion event category. See the [values](#conversion_category_id-values-for-updating-a-conversion-by-id) of `conversion_category_id`. |
| `conversion_category_custom` | string | Label of the custom conversion event category. This field is set to the string value of what category to include the conversion in.<br><br>**Warning:**<br>This field is only set if `conversion_category_id` is `null`. |
| `count_type` | enum | Type of conversion count - `view`, `click` or `hybrid`. This is a **required** field. |
| `min_minutes_per_conversion` | integer | The interval (in minutes) to allow a repeat conversion. Maximum value is `32767` (22 days).<br>- If set to `0`: Count all conversions.<br>- If set to `null` (default): Count one per user. |
| `post_click_value` | number | The value you attribute to a conversion after a click. |
| `post_click_expire_minutes` | number | The interval (in minutes) from impression time allowed for a click conversion to be counted as eligible. Maximum value is `43200` (30 days). If set to `0` or `null`, the maximum lookback window applies. |
| `post_view_value` | number | The value you attribute to a conversion after a view. |
| `post_view_expire_minutes` | number | The interval, in minutes, from the impression time within which a view conversion is eligible. The maximum value is **43,200 minutes (30 days)**. If set to `0` or `null`, the system applies the maximum lookback window. |
| `rule` | object | Rule set for the audience. This is a **required** field and an object. It should contain an array of the rules that must be met to consider a fire of the Universal Pixel to be a conversion. For example, below [rule](#rule-for-updating-a-conversion-by-id-request-body) means the Universal Pixel fire must be on a website that has a domain that contains [microsoft.com](https://www.microsoft.com/), the event for the pixel fire is Purchase, and `item_id` is `123`. |

##### `conversion_category_id` values for updating a conversion by ID

```
{ id: 1, title: ' Page view', event: 'PageView' },
{ id: 2, title: ' Landing page', event: 'LandingPage' },
{ id: 3, title: ' Item view', event: 'ItemView' },
{ id: 4, title: ' Add to cart', event: 'AddToCart' },
{ id: 5, title: ' Initiate checkout', event: 'InitiateCheckout' },
{ id: 6, title: ' Add payment info', event: 'AddPaymentInfo' },
{ id: 7, title: ' Purchase', event: 'Purchase' },
{ id: 8, title: ' Lead', event: 'Lead' },
{ id: null, title: ' Other' },
```

##### `rule` for updating a conversion by ID (request body)

```
"rule": {
"and": [
{
"domain":
{ "contains": [ "microsoft.com" ] }
},
{
"event":
{ "equals": [ "Purchase" ] }
},
{
"item_id":
{ "equals": [ "123" ] }
}
],
"pixel_uuid": "0b3758f1-cf0f-46c1-9957-00bd36f19ad0"
},
```

#### JSON fields (response body) for updating a conversion by ID

| Field | Type | Description |
|:---|:---|:---|
| `id` | integer | Conversion ID assigned by the API. |
| `member_id` | integer | ID of a member associated with conversions for operation. |
| `version_id` | integer | Version for this conversion. |
| `universal_pixel_id` | integer | ID for the Universal Pixel associated with this conversion. |
| `name` | string | Name of the conversion. |
| `conversion_pixel_id` | integer | ID of legacy conversion pixel. |
| `conversion_category_id` | integer | ID of the conversion event category. See the [values](#conversion_category_id-values-for-updating-a-conversion-by-id-response-body) of `conversion_category_id`. |
| `conversion_category_custom` | string | Label of the custom conversion event category. This field is set to the string value of what category to include the conversion in.<br><br>**Warning:** This field is only set if `conversion_category_id` is `null`. |
| `count_type` | enum | Type of conversion count - `view`, `click` or `hybrid`. |
| `min_minutes_per_conversion` | integer | The interval (in minutes) to allow a repeat conversion. Maximum value is `32767` (22 days).<br>- If set to `0`: count all conversions.<br>- If set to `null` (default): Count one per user. |
| `post_click_value` | number | The value you attribute to a conversion after a click. |
| `post_click_expire_minutes` | number | The interval (in minutes) from impression time allowed for a click conversion to be counted as eligible. Maximum value is `43200` (30 days). If set to `0` or `null`, the maximum lookback window applies. |
| `post_view_value` | number | The value you attribute to a conversion after a view. |
| `post_view_expire_minutes` | number | The interval, in minutes, from the impression time within which a view conversion is eligible. The maximum value is **43,200 minutes (30 days)**. If set to `0` or `null`, the system applies the maximum lookback window. |
| `rule` | object | Rule set for the audience. This field is an object and contains an array of the rules that must be met to consider a fire of the Universal Pixel to be a conversion. For example, below [rule](#rule-for-updating-a-conversion-by-id-response-body) means the Universal Pixel fire must be on a website that has a domain that contains [microsoft.com](https://www.microsoft.com/), the event for the pixel fire is Purchase, and `item_id` is `123`. |
| `created_on` | string | Timestamp when audience was created. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |
| `published_on` | string | Timestamp when audience was published. <br>**Format:** `YYYY-MM-DD HH:MM:SS` e.g., `2019-03-08 15:34:18`. |

##### `conversion_category_id` values for updating a conversion by ID (response body)

```
{ id: 1, title: ' Page view', event: 'PageView' },
{ id: 2, title: ' Landing page', event: 'LandingPage' },
{ id: 3, title: ' Item view', event: 'ItemView' },
{ id: 4, title: ' Add to cart', event: 'AddToCart' },
{ id: 5, title: ' Initiate checkout', event: 'InitiateCheckout' },
{ id: 6, title: ' Add payment info', event: 'AddPaymentInfo' },
{ id: 7, title: ' Purchase', event: 'Purchase' },
{ id: 8, title: ' Lead', event: 'Lead' },
{ id: null, title: ' Other' },
```

##### `rule` for updating a conversion by ID (response body)

```
"rule": {
"and": [
{
"domain":
{ "contains": [ "microsoft.com" ] }
},
{
"event":
{ "equals": [ "Purchase" ] }
},
{
"item_id":
{ "equals": [ "123" ] }
}
],
"pixel_uuid": "0b3758f1-cf0f-46c1-9957-00bd36f19ad0"
},
```

### Delete a conversion by ID

#### Query fields for deleting a conversion by ID

| Field | Type | Description |
|:---|:---|:---|
| `id` | integer | ID for the Universal Pixel assigned by the API which would be deleted. |

## Examples

### Get a list of Universal Pixels

```
$ curl -b cookies "https://api.appnexus.com/universal-pixel/pixel"
{
    "data": [{
        "id": 0,
        "name": "string",
        "uuid": "string",
        "member_id": 0,
        "advertiser_id": 0,
        "created_on": "2019-04-16T20:43:33.663Z",
        "last_modified": "2019-04-16T20:43:33.663Z"
    }],
    "meta": {
        "count": 0,
        "start_element": 0,
        "num_elements": 0,
        "sort": [
            "string"
        ]
    }
}
```

### Example: Create a new Universal Pixel

```
$ cat new-universal-pixel.json
 
{
    "name": "string",
    "advertiser_id": 0
}

$ curl -b cookies -d @new-universal-pixel.json -X POST https://api.appnexus.com/universal-pixel/pixel
{
  "id": 0,
  "name": "string",
  "uuid": "string",
  "member_id": 0,
  "advertiser_id": 0,
  "created_on": "2019-04-16T21:23:52.049Z",
  "last_modified": "2019-04-16T21:23:52.049Z"
}
 
```

### Example: View a Universal Pixel by ID

```
$ curl -b cookies "https://api.appnexus.com/universal-pixel/pixel/3"

response:
{
    "created_on": "2019-04-09T21:27:54.455Z",
    "id": 3,
    "last_modified": "2019-04-09T21:27:54.455Z",
    "member_id": 0,
    "name": "Production Pixel 1",
    "uuid": "b95be84e-d95b-4c88-8242-d9c6c026ed30"
}
```

### Example: Update a Universal Pixel by ID

```
 {
  "name": "string"
}
```

### Example: View a Universal Pixel by UUID

```
 $ curl -b cookies "https://api.appnexus.com/universal-pixel/pixel-uuid/239e941-0356-47bd-9f92-f46e46d34d16`
response:
{
    "advertiser_id": 4647027,
    "created_on": "2020-05-26T16:05:12.049Z",
    "id": 2716,
    "last_modified": "2020-05-26T16:05:12.049Z",
    "member_id": 1370,
    "name": "Test",
    "uuid": "7239e941-0356-47bd-9f92-f46e46d34d16"
}
```

### View a list of audiences associated with a member or advertiser

```
- member: curl -b cookies "https://api.appnexus.com/universal-pixel/audience?member_id=1111"
- advertiser: grab the Universal Pixel ID created under the advertiser and run:
 curl -b  cookies "https://api.appnexus.com/universal-pixel/audience?universal_pixel_id=2716" 
{
  "data": [
    {
      "id": 0,
      "version_id": 0,
      "universal_pixel_id": 0,
      "advertiser_id": 0,
      "name": "string",
      "segment_id": 0,
      "user_ttl_minutes": 0,
      "rule": {
        "and": [
            {
            "domain":
            { "contains": [ "microsoft.com" ] }
            },
            {
            "event":
            { "equals": [ "Purchase" ] }
            },
            {
            "item_id":
            { "equals": [ "123" ] }
            }
            ],
        "pixel_uuid": "0b3758f1-cf0f-46c1-9957-00bd36f19ad0"
        },
      "created_on": "2020-04-16T13:15:19.056Z",
      "published_on": "2020-04-16T13:15:19.057Z"
    }
  ],
  "meta": {
    "count": 0,
    "start_element": 0,
    "num_elements": 0,
    "sort": [
      "string"
    ]
  }
```

### Examples: Create a new audience

```
 $ cat new-audience.json
 
{
  "universal_pixel_id": 0,
  "name": "string",
  "user_ttl_minutes": 0,   
  "rule": {
        "and": [
            {
            "domain":
            { "contains": [ "microsoft.com" ] }
            },
            {
            "event":
            { "equals": [ "Purchase" ] }
            },
            {
            "item_id":
            { "equals": [ "123" ] }
            }
            ],
        "pixel_uuid": "0b3758f1-cf0f-46c1-9957-00bd36f19ad0"
        }
}

$ curl -b cookies -d @new-audience.json -X POST https://api.appnexus.com/universal-pixel/audience
{
  "id": 0,
  "version_id": 0,
  "universal_pixel_id": 0,
  "advertiser_id": 0,
  "name": "string",
  "segment_id": 0,
  "user_ttl_minutes": 0,
  "rule": {
        "and": [
            {
            "domain":
            { "contains": [ "microsoft.com" ] }
            },
            {
            "event":
            { "equals": [ "Purchase" ] }
            },
            {
            "item_id":
            { "equals": [ "123" ] }
            }
            ],
        "pixel_uuid": "0b3758f1-cf0f-46c1-9957-00bd36f19ad0"
        },
  "created_on": "2020-04-16T13:15:48.648Z",
  "published_on": "2020-04-16T13:15:48.648Z"
}
```

### Example: View an audience by ID

```
$ curl -b cookies "https://api.appnexus.com/universal-pixel/audience/10181"

response:
{
    "advertiser_id": 4443337,
    "created_on": "2020-06-09T15:47:26.578Z",
    "id": 11111,
    "name": "purchase_capture",
    "published_on": "2020-06-09T15:47:27.056Z",     
    "rule": {
        "and": [
            {
            "domain":
            { "contains": [ "microsoft.com" ] }
            },
            {
            "event":
            { "equals": [ "Purchase" ] }
            },
            {
            "item_id":
            { "equals": [ "123" ] }
            }
            ],
        "pixel_uuid": "0b3758f1-cf0f-46c1-9957-00bd36f19ad0"
        },     
    "segment_id": 22222227,
    "universal_pixel_id": 2222,
    "user_ttl_minutes": 43200,
    "version_id": 15000
} 
```

### Example: Update an audience by ID

```
$ cat update-audience.json 
{
  "name": "string",
  "user_ttl_minutes": 0,   
  "rule": {
        "and": [
            {
            "domain":
            { "contains": [ "microsoft.com" ] }
            },
            {
            "event":
            { "equals": [ "Purchase" ] }
            },
            {
            "item_id":
            { "equals": [ "123" ] }
            }
            ],
        "pixel_uuid": "0b3758f1-cf0f-46c1-9957-00bd36f19ad0"
        }, 
}

$ curl -b cookies -d @new-universal-pixel.json -X POST https://api.appnexus.com/universal-pixel/audience
{
  "id": 0,
  "version_id": 0,
  "universal_pixel_id": 0,
  "advertiser_id": 0,
  "name": "string",
  "segment_id": 0,
  "user_ttl_minutes": 0,
  "rule": {
        "and": [
            {
            "domain":
            { "contains": [ "microsoft.com" ] }
            },
            {
            "event":
            { "equals": [ "Purchase" ] }
            },
            {
            "item_id":
            { "equals": [ "123" ] }
            }
            ],
        "pixel_uuid": "0b3758f1-cf0f-46c1-9957-00bd36f19ad0"
        },
  "created_on": "2020-04-16T13:17:29.915Z",
  "published_on": "2020-04-16T13:17:29.915Z"
}
```

### View a list of conversions associated with a member or advertiser

```
- member: curl -b cookies "https://api.appnexus.com/universal-pixel/conversion?member_id=2222"
- advertiser: grab the Universal Pixel ID created under the advertiser and run:
 curl -b  cookies "https://api.appnexus.com/universal-pixel/conversion?universal_pixel_id=27777" 
{
  "data": [
    {
      "id": 0,
      "member_id": 0,
      "version_id": 0,
      "universal_pixel_id": 0,
      "name": "string",
      "conversion_pixel_id": 0,
      "conversion_category_id": 7,
      "conversion_category_custom": "string",
      "count_type": "hybrid",
      "min_minutes_per_conv": 0,
      "post_view_value": 0,
      "post_click_value": 0,
      "post_click_expire_minutes": 0,
      "post_view_expire_minutes": 0,       
      "rule": {
        "and": [
            {
            "domain":
            { "contains": [ "microsoft.com" ] }
            },
            {
            "event":
            { "equals": [ "Purchase" ] }
            },
            {
            "item_id":
            { "equals": [ "123" ] }
            }
            ],
        "pixel_uuid": "0b3758f1-cf0f-46c1-9957-00bd36f19ad0"
        },
      "published_on": "2020-04-16T13:20:02.601Z",
      "created_on": "2020-04-16T13:20:02.601Z"
    }
  ],
  "meta": {
    "count": 0,
    "start_element": 0,
    "num_elements": 0,
    "sort": [
      "string"
    ]
  }
```

### Example: Create a new conversion

```
 $ cat new-conversion.json 
{
  "universal_pixel_id": 0,
  "name": "string",
  "conversion_category_id": 2,
  "conversion_category_custom": "string",
  "count_type": "hybrid",
  "min_minutes_per_conv": 0,
  "post_view_value": 0,
  "post_click_value": 0,
  "post_click_expire_minutes": 0,
  "post_view_expire_minutes": 0,   
  "rule": {
        "and": [
            {
            "domain":
            { "contains": [ "microsoft.com" ] }
            },
            {
            "event":
            { "equals": [ "Purchase" ] }
            },
            {
            "item_id":
            { "equals": [ "123" ] }
            }
            ],
        "pixel_uuid": "0b3758f1-cf0f-46c1-9957-00bd36f19ad0"
        }
 }

$ curl -b cookies -d @new-conversion.json -X POST https://api.appnexus.com/universal-pixel/conversion

{
  "id": 0,
  "member_id": 0,
  "version_id": 0,
  "universal_pixel_id": 0,
  "name": "string",
  "conversion_pixel_id": 0,
  "conversion_category_id": 2,
  "conversion_category_custom": "string",
  "count_type": "hybrid",
  "min_minutes_per_conv": 0,
  "post_view_value": 0,
  "post_click_value": 0,
  "post_click_expire_minutes": 0,
  "post_view_expire_minutes": 0,   
  "rule": {
        "and": [
            {
            "domain":
            { "contains": [ "microsoft.com" ] }
            },
            {
            "event":
            { "equals": [ "Purchase" ] }
            },
            {
            "item_id":
            { "equals": [ "123" ] }
            }
            ],
        "pixel_uuid": "0b3758f1-cf0f-46c1-9957-00bd36f19ad0"
        },
  "published_on": "2020-04-16T13:20:24.931Z",
  "created_on": "2020-04-16T13:20:24.931Z"
}
```

### Example: View a conversion by ID

```
 $ curl -b cookies "https://api.appnexus.com/universal-pixel/conversion/4444"

response:
{
    "conversion_category_custom": null,
    "conversion_category_id": 7,
    "conversion_pixel_id": 1111111,
    "count_type": "hybrid",
    "created_on": "2020-05-29T21:52:08.388Z",
    "id": 4444,
    "min_minutes_per_conv": 0,
    "name": "Install",
    "post_click_expire_minutes": 20160,
    "post_click_value": null,
    "post_view_expire_minutes": 20160,
    "post_view_value": null,
    "published_on": "2020-05-29T21:52:09.093Z",     
    "rule": {
        "and": [
            {
            "domain":
            { "contains": [ "microsoft.com" ] }
            },
            {
            "event":
            { "equals": [ "Purchase" ] }
            },
            {
            "item_id":
            { "equals": [ "123" ] }
            }
            ],
        "pixel_uuid": "0b3758f1-cf0f-46c1-9957-00bd36f19ad0"
        },     
    "universal_pixel_id": 2222,
    "version_id": 4444
}
```

### Example: Update a conversion by ID

```
 $ cat update-conversion.json 
{
  "name": "string",
  "conversion_category_id": 7,
  "conversion_category_custom": "string",
  "count_type": "hybrid",
  "min_minutes_per_conv": 0,
  "post_view_value": 0,
  "post_click_value": 0,
  "post_click_expire_minutes": 0,
  "post_view_expire_minutes": 0,   
  "rule": {
        "and": [
            {
            "domain":
            { "contains": [ "microsoft.com" ] }
            },
            {
            "event":
            { "equals": [ "Purchase" ] }
            },
            {
            "item_id":
            { "equals": [ "123" ] }
            }
            ],
        "pixel_uuid": "0b3758f1-cf0f-46c1-9957-00bd36f19ad0"
        } 
}

$ curl -b cookies -d @update-conversion.json -X POST https://api.appnexus.com/universal-pixel/conversion

{
  "id": 0,
  "member_id": 0,
  "version_id": 0,
  "universal_pixel_id": 0,
  "name": "string",
  "conversion_pixel_id": 0,
  "conversion_category_id": 7,
  "conversion_category_custom": "string",
  "count_type": "hybrid",
  "min_minutes_per_conv": 0,
  "post_view_value": 0,
  "post_click_value": 0,
  "post_click_expire_minutes": 0,
  "post_view_expire_minutes": 0,   
  "rule": {
        "and": [
            {
            "domain":
            { "contains": [ "microsoft.com" ] }
            },
            {
            "event":
            { "equals": [ "Purchase" ] }
            },
            {
            "item_id":
            { "equals": [ "123" ] }
            }
            ],
        "pixel_uuid": "0b3758f1-cf0f-46c1-9957-00bd36f19ad0"
        },   
  "published_on": "2020-04-16T13:20:24.937Z",
  "created_on": "2020-04-16T13:20:24.937Z"
}
```
