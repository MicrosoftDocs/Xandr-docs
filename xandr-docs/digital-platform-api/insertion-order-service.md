---
title: Digital Platform API - Insertion Order Service
description: Learn about the Insertion Order service, their JSON fields, and how it enables you to better organize, track, and allocate budget to your line items.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Insertion Order service

Insertion orders enable you to better organize, track, and allocate budget to your line items. Additionally, budget intervals (i.e., sets of flight dates each with their own pacing and budget) can be used on insertion orders, allowing you to represent available budget in a way that more accurately reflects your contract with an advertiser. Xandr suggests using insertion orders and budget intervals.

Insertion orders can be associated with one or more line items. A line item can belong to multiple insertion orders as long as the budget intervals on those insertion orders do not overlap.

> [!NOTE]
>
> - Insertion orders are enabled at the Advertiser level using the [Advertiser Service](advertiser-service.md) (the `use_insertion_orders` field in that service must be set to `"true"`).
> - Line items are created through the [Line Item Service - ALI](line-item-service---ali.md) (or [Line Item Service](line-item-service.md) for legacy line items).
>
> **Seamless insertion orders**
>
> There are two types of insertion orders:
>
> - **Seamless** – Seamless insertion order for line items that provide additional targeting and budgeting settings. The `budget_type` setting of Seamless insertion orders may restrict associated guaranteed delivery augmented line items (GDALI) and programmatic guaranteed line items (PGLI) that have conflicting settings. We recommend using seamless insertion orders with `budget_type` set to `"flexible"` for GDALIs and PGLIs so you can associate both impression-based and revenue-based line items to the same insertion order.
> - **Legacy** (non-seamless) – Legacy insertion order required for legacy guaranteed and non-guaranteed line items. Legacy insertion orders do not use the `budget_intervals` array and cannot be used with augmented line items (ALI), guaranteed delivery augmented line items (GDALI), and programmatic guaranteed line items (PGLI).
>
> The main differences in setup for each type of insertion order are as follows:
>
> - To create a **Seamless** insertion order, you must:
>
>   - Use the budget and pacing related fields and the `start_date` and `end_date` fields in the `budget_intervals` array to specify the dates during which the insertion order should run, what budget is available to it during those dates and how spending of the budget should be paced.
>   - Leave the `start_date` and `end_date` fields (and any budget or pacing related fields) on the main insertion order level set to `null` (default setting).
>   - Only associate seamless line items with seamless insertion orders. For instructions on how to create seamless line items, see [Line Item Service - ALI](line-item-service---ali.md).
>
> - To create a **Legacy** (non-seamless) insertion order, you must:
>   - Use the budget and pacing related fields and the `start_date` and `end_date` fields on the main insertion order object to specify the dates during which the insertion order should run, what budget is available to it during those dates, and how the spending of the budget should be paced.
>   - Ensure the `budget_intervals` field is set to `null`.
>   - Only associate non-seamless line items with non-seamless insertion orders. For instructions on how to create non-seamless line items, see [Line Item Service](line-item-service.md).
> [!IMPORTANT]
> Seamless insertion orders are the preferred model. You should use the seamless insertion order workflow when creating new insertion orders. You cannot convert a non-seamless insertion order to seamless or link non-seamless line items to seamless insertion orders.
>
> In the UI, API `budget_intervals` are referred to as "Billing Periods".
> [!NOTE]
> **Insertion Orders for Guaranteed Delivery Augmented Line Items (GDALI)**
>
> For an insertion order to be associated with a guaranteed delivery augmented line item (GDALI), the insertion order must:
>
> - Be a Seamless Insertion Order (legacy insertion orders are not compatible).
> - Have `budget_type` set to `"flexible"` or `"impression"`.
> - Not contain more than one `budget_intervals` array.
> - Have unlimited budget (set via the `budget_intervals` array).
>
> Insertion orders not matching the above may only be associated to non-guaranteed line items. The above settings are also required for programmatic guaranteed line items (PGLI). An insertion order with the above settings may also be associated to non-guaranteed line items.
>
> Associating a `profile_id` (e.g., frequency capping or setting additional targeting) on the insertion order object may result in unexpected forecasting or delivery for PGLIs and GDALIs. It is recommended not to use `profile_id` for insertion orders intended for the use with GDALIs.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/insertion-order?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/insertion-order?advertiser_id=ADVERTISER_ID)<br>(insertion order JSON) | Add a new insertion order. |
| `PUT` | [https://api.appnexus.com/insertion-order?id=INSERTIONORDER_ID&advertiser_id=ADVERTISER_ID](https://api.appnexus.com/insertion-order?id=INSERTIONORDER_ID&advertiser_id=ADVERTISER_ID)<br>(insertion order JSON) | Modify an existing insertion order. |
| `GET` | [https://api.appnexus.com/insertion-order?advertiser_id=ADVERTISER_ID](https://api.appnexus.com/insertion-order?advertiser_id=ADVERTISER_ID) | View all of the insertion orders for one of your advertisers. |
| `DELETE` | [https://api.appnexus.com/insertion-order?id=INSERTIONORDER_ID&advertiser_id=ADVERTISER_ID](https://api.appnexus.com/insertion-order?id=INSERTIONORDER_ID&advertiser_id=ADVERTISER_ID)<br><br>**Important:** Deleting an insertion order does not necessarily mean that associated line items will be deleted as the relationship between an insertion order and line item can be many to many. Also, deletion of an insertion order results in deletion of the associated budget intervals. | Delete an insertion order. |
| `GET` | [https://api.appnexus.com/insertion-order?id=INSERTIONORDER_ID](https://api.appnexus.com/insertion-order?id=INSERTIONORDER_ID) | View a specific insertion order for one of your advertisers. |
| `GET` | [https://api.appnexus.com/insertion-order?id=1,2,3](https://api.appnexus.com/insertion-order?id=1,2,3) | View multiple insertion orders by ID using a comma-separated list. |
| `GET` | [https://api.appnexus.com/insertion-order?search=SEARCH_TERM](https://api.appnexus.com/insertion-order?search=SEARCH_TERM) | Search for insertion orders with IDs or names containing certain characters. |
| `GET` | [https://api.appnexus.com/insertion-order/meta](https://api.appnexus.com/insertion-order/meta) | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the insertion order.<br>**Required On:** `PUT` |
| `name` | string | The name of the insertion order. (Maximum of 255 characters.)<br>**Required On:** `POST` |
| `code` | string | The custom code for the insertion order. The code may only contain alphanumeric characters, periods, underscores or dashes. The code you enter is not case-sensitive (upper- and lower-case characters are treated the same). No 2 objects at the same level (e.g., line items) can use the same code per advertiser. For example, 2 lines items cannot both use code "XYZ", but a single line item and its child campaign can.<br><br>**Note:** There may also be a custom code per budget interval. <br><br>For more details, see the [Budget Intervals](#budget-intervals) array below.<br>**Default:** `null` |
| `state` | enum | The state of the insertion order. <br>Possible values: `"active"` or `"inactive"`.<br>**Default:** `"active"` |
| `advertiser_id` | int | The ID of the advertiser.<br>**Required On:** `POST` |
| `start_date` | timestamp | The start date of the non-seamless insertion order. If you are creating a seamless insertion order, do not set this field.<br>**Default:** `null` (immediately) |
| `end_date` | timestamp | The end date of the non-seamless insertion order. If you are creating a seamless insertion order, do not set this field.<br>**Default:** `null` (indefinitely) |
| `remaining_days` | int | The number of days between today and the `end_date` for the insertion order. <br><br>**Note:** This will be `null` if the `start_date` is in the future or if either the `start_date` or `end_date` is not set.<br><br>**Read Only.** |
| `total_days` | int | The number of days between the `start_date` and `end_date` for the insertion order. <br><br>**Note:** This will be `null` if either the `start_date` or `end_date` is not set.<br><br>**Read Only.** |
| `last_modified` | timestamp | The time of the last modification to this campaign.<br>**Read Only.** |
| `timezone` | string | The timezone by which budget and spend are counted. For a list of acceptable timezone values, see [API Timezones](api-timezones.md).<br><br>**Note:** Any `PUT` calls to the `advertiser` service which include `set_child_timezone=true` in the query string will cause any timezone settings on the lower level objects (e.g., insertion orders, line items) to be overridden with the latest timezone value for that advertiser.<br><br>**Default:** `"EST5EDT"` or the advertiser's timezone. |
| `currency` | string | The currency assigned to the insertion order. For a full list of available currencies, use the read-only [Currency Service](currency-service.md). <br><br>**Note:** Once the insertion order has been created, the currency cannot be changed.<br><br>**Default:** Default currency of the advertiser. |
| `comments` | string | Comments about the insertion order. |
| `billing_code` | string | The billing code for the insertion order. This will only appear on invoices that are insertion order-specific (e.g., if you receive an invoice per insertion order). For details on invoices, see "Understanding Your Invoice" in the Finance documentation.<br>**Default:** `null` |
| `line_items` | array of objects | The line items which are associated with the insertion order. For more information, see [Line Items](#line-items) below.<br><br>**Note:** Seamless insertion orders may only be associated with seamless line items. Non-seamless insertions orders may only be associated with non-seamless line items. |
| `labels` | array of objects | The labels assigned to the insertion order. See [Labels](#labels) below. |
| `broker_fees` | array of objects | **Warning:** For augmented line items (ALIs):<br>Broker fees are deprecated for augmented line items. Create partner fees and apply them to the line item using the [Partner Fee Service](partner-fee-service.md).<br>For standard line items:<br> - Broker fees created on an insertion order only apply to standard line items. If you also use augmented line items, you will need to create and apply partner fees to ALIs using the [Partner Fee Service](partner-fee-service.md).<br> - Broker fees at the line item level override broker fees at the insertion order level.<br><br>The commissions that the network must pass to brokers when serving an ad. These commissions are deducted from the booked revenue (the amount the network receives from the advertiser) and are typically for brokering a relationship with the advertiser. They can either be a percentage of the revenue or a flat CPM. For more details, see [Broker Fees](#broker-fees) below. |
| `budget_intervals` | array of objects | **Note:** This array is only relevant to and required for seamless insertion orders (if the insertion order is non-seamless, leave this field set to `null`). <br><br>Budget intervals enable multiple date intervals to be attached to an insertion order, each with corresponding budget values. For more details, see [Budget Intervals](#budget-intervals) below.<br><br>**Note:**<br>If you use `budget_intervals`, the following fields should not be used on the top level insertion order object:<br> - `lifetime_pacing`<br> - `lifetime_budget`<br> - `lifetime_budget_imps`<br> - `enable_pacing`<br> - `lifetime_pacing_span`<br> - `allow_safety_pacing`<br> - `daily_budget`<br> - `daily_budget_imps`<br> - `lifetime_pacing_pct` |
| `budget_type` | enum | The budget type of the insertion order. <br>Values may be `'revenue'`, `'impression'`, or `'flexible'`.<br> - If this field is set to `'impression'` then both the `lifetime_budget` and `daily_budget` fields must be set to `null`.<br> - If this field is set to `'revenue'` then both the `lifetime_budget_imps` and `daily_budget_imps` fields must be set to `null`.<br> - This field must be set when all four budget fields in the `budget_intervals` array (`lifetime_budget`, `lifetime_budget_imps`, `daily_budget`, and `daily_budget_imps`) have been set to `null`.<br> - If this field is set to `'flexible'` then the `budget_intervals` array can only have one interval and all four budget fields in the `budget_intervals` array (`lifetime_budget`, `lifetime_budget_imps`, `daily_budget`, and `daily_budget_imps`) must be set to `null`. |
| `lifetime_pacing` | boolean | If `true`, the non-seamless insertion order will attempt to spend its overall lifetime budget evenly over the insertion order flight dates. If `true`:<br> - You must establish a `lifetime_budget` or `lifetime_budget_imps`.<br> - You must establish a `start_date` and `end_date`.<br> - You cannot set a `daily_budget`.<br> - You cannot set `enable_pacing` to `false`.<br><br>**Note:** Only applicable to non-seamless insertion orders.<br><br>**Default:** `null` |
| `lifetime_budget` | double | The lifetime budget in revenue. The revenue currency is defined by the `currency` field.<br><br>**Note:**<br>Only applicable to non-seamless insertion orders.<br><br>**Default:** `null` (unlimited) |
| `lifetime_budget_imps` | int | The lifetime budget in impressions. <br><br>**Note:** If you add line items to this insertion order, any spend already associated with those line items before they are added to the insertion order is NOT counted against the lifetime budget of the insertion order. Only spend that occurs while the line item is a child of the insertion order is counted. Only applicable to non-seamless insertion orders.<br><br>**Default:** `null` (unlimited) |
| `enable_pacing` | boolean | If `true`, then spending will be paced over the course of the day. Only applicable if there is a `daily_budget`.<br><br>**Note:** Only applicable to non-seamless insertion orders. |
| `lifetime_pacing_span` | int | In the event of an underspend event, this indicates the number of days across which the underspent amount will be distributed.<br><br>**Note:** Only applicable to non-seamless insertion orders.<br><br>**Default:** `null` (3 days) |
| `daily_budget` | double | The daily budget in revenue. The revenue currency is defined by the `currency` field.<br><br>**Note:** If you add line items to this insertion order, any impressions associated to those line items when they are added to the insertion order are NOT counted under the lifetime budget of the insertion order. Only impressions that occur while the line item is a child of the insertion order are counted. Only applicable to non-seamless insertion orders.<br><br>**Default:** `null` (unlimited) |
| `daily_budget_imps` | int | The daily budget in impressions.<br><br>**Note:**<br>Only applicable to non-seamless insertion orders.<br><br>**Default:** `null` (unlimited) |
| `lifetime_pacing_pct` | double | A double integer between (and including) 50 and 150, used to set pacing throughout the insertion order's lifetime. Possible values can be any double between 50 and 150 on the following scale:<br> - `50`: Pace behind schedule.<br> - `100`: Pace evenly.<br> - `150`: Pace ahead of schedule.<br><br>**Note:** Only applicable to non-seamless insertion orders.<br>**Alpha-Beta Notice**<br>This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change.<br><br>**Default:** `100` |
| `profile_id` | int | Specifies the ID of the profile attached to the seamless insertion order (i.e., must use budget_intervals). A profile can be used to define how inventory is targeted and/or how frequency capping is enforced (For details, see [Profile Service](profile-service.md)). A profile can also be set at the advertiser, line item, campaign, and creative levels. The most restrictive setting always takes precedence. |
| `stats` | object | The `stats` object has been **deprecated** (as of October 17, 2016). Use the [Report Service](report-service.md) to obtain statistical information instead. |
| `object_stats` | object | The number of total, active, and inactive line items under the insertion order. To include this object in a GET response, pass `object_stats=true` in the query string.<br>**Read Only.** |
| `viewability_standard_provider` | string | This field determines what standard to measure viewability against. For example, `iab`.<br><br>**Note:**<br>This field cannot be edited, and only appears on seamless insertion orders.<br><br>**Default:** `'iab'` |
| `is_running_political_ads` | boolean | Declares whether or not this insertion order contains political advertising (defined as advertising related to an election, ballot initiative, or political candidate, in the United States). If `true`, the `political_content` object is editable. If `true`, and if the insertion order targets a state with additional political reporting requirements, many fields in `political_content` object are required. For more information on state requirements, see [Political Advertising Policy Implementation](../monetize/political-advertising.md). For more information on the `political_content` object, see [Political Content](#political-content) below.<br>`is_running_political_ads` must be set to `true` on the [advertiser](advertiser-service.md) to be set to `true` on the insertion order. For more information, see the [Advertiser Service](advertiser-service.md).<br>**Default:** `0` `false` |
| `political_content` | object | Information about political advertising conducted with this insertion order. Political advertising must be enabled on the [advertiser](advertiser-service.md) and on this insertion order for this object to be editable. (That is, the field `is_running_political_ads` must be `true` on both the advertiser and the insertion order.)<br>For more information about this object, see [Political Content](#political-content) below. |

### Line items

Each object in the `line_items` array contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The numeric ID associated with this line item. <br>**Required On:** `POST` or `PUT`. |
| `line_item_type` | enum | The type associated with the child line item. Possible values are:<br> - `"standard_v1"`: Denotes that the child line item is a standard line item.<br> - `"standard_v2"`: Denotes that the child line item is an augmented line item.<br> - `"guaranteed"`: Denotes that the child line item is a guaranteed line item.<br> - `"performance"`: This line item type has been **deprecated**. |
| `name` | string | The name of the line item. |
| `code` | string | If you have chosen to associate an optional identifying name (a "code") with this line item, it will show up here. |
| `state` | string | Line items can be `"active"` or `"inactive"`. |
| `end_date` | date | The date when line items stop serving. |
| `start_date` | date | The date when line items start serving. |
| `timezone` | string | The timezone with which the line item is set to. This will affect the `start_date` and `end_date`. |

### Labels

You can use the read-only [Label Service](label-service.md) to view all possible labels for line items, advertisers, insertion orders, and publishers. This service also allows you to view the labels that have already been applied to your insertion order.

| Field | Type | Description |
|:---|:---|:---|
| `value` | string (100) | The value assigned to the label. For example, for the `"Sales Rep"` label, this could be a name such as `"Michael Sellers"`. |
| `id` | int | The ID of the label.<br>**Required On:** `POST` or `PUT`. |
| `name` | enum | The name of the label. Possible values:<br> - `"Trafficker"`<br> - `"Sales Rep"`<br> - `"Campaign Type"` |

### Broker fees

> [!WARNING]
> For augmented line items (ALIs):
>
> Broker fees are deprecated for augmented line items. Create partner fees and apply them to the line item using the [Partner Fee Service](partner-fee-service.md).
>
> For standard line items:
>
> - Broker fees created on an insertion order only apply to standard line items. If you also use augmented line items, you will need to create and apply partner fees to ALIs using the [Partner Fee Service](partner-fee-service.md).
> - Broker fees at the line item level override broker fees at the insertion order level.
> [!NOTE]
> The decimal position support for the broker fees in UI is for 1 place after the decimal. For example, if you set 16.67% as a broker fee in the Commissions section, after saving, the value would round off to 16.7%. However, there is no restriction on number of places after decimal if the Insertion Order service API is used to create the broker fee.

Each object in the `broker_fees` array contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `broker_id` | int | The ID of the broker. |
| `payment_type` | enum | Type of payment to the broker. Possible values:<br> - `"cpm"`<br> - `"revshare"` |
| `value` | double | The value of the payment, based on the payment type. |
| `description` | string (255) | The free-form description of the broker fee entry. |

### Budget intervals

> [!NOTE]
> This array is only used for seamless insertion orders.

Consider the following when using the `budget_interval` array:

- Budget intervals must contain a `start_date` and `end_date`.
- Date ranges (i.e., `start_date`, `end_date`) of different budget intervals on the same insertion order cannot overlap.
- Budget intervals must contain a `lifetime_budget` or `lifetime_budget_imps`.
- Budget intervals cannot be used if budget fields on the `insertion_order` object itself are set.
- Edits made to the budget interval (e.g., start or end dates) on the insertion order must be manually replicated on all child line items (using the `line-item` service).
  - For *standard* line items, use the `parent_interval_id` to link the line item to its parent insertion order. Budget interval dates will automatically be inherited by the line item once that association is made. See [Line Item Service](line-item-service.md).
  - For *augmented* line items (ALI), ensure that start and end dates of each budget interval fall within the dates of the parent insertion order's budget intervals. See [Line Item Service (Augmented)](line-item-service---ali.md).
- A maximum of 52 budget intervals may be created per insertion order.
- If you want the budget interval to have an unlimited budget, all 4 budget fields in the array (`lifetime_budget`, `lifetime_budget_imps`, `daily_budget`, and `daily_budget_imps`) must be set to `null`. This is only allowed if the `lifetime_pacing` field is set to `"false"`.

Each object in the `budget_intervals` array contains the following fields.

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The ID of the budget interval. |
| `start_date` | timestamp | The start date of the budget interval. Format must be YYYY-MM-DD hh:mm:ss (hh:mm:ss must be set to `00`). |
| `end_date` | timestamp | The end date of the budget interval. Format must be YYYY-MM-DD hh:mm:ss (hh:mm:ss must be set to `23:59:59`). If this field is set to `null`, then the insertion order's budget interval will run indefinitely. If you set this field to `'null'`:<br> - There may not be more than one object in the `budget_intervals` array (i.e., maximum of 1 budget interval).<br> - The `lifetime_pacing` field must set to `"false"`.<br> - The `"daily_budget"` field must be set to `null`. |
| `timezone` | string | The timezone by which budget and spend are counted. For a list of acceptable timezone values, see [API Timezones](api-timezones.md). The default value is `"EST5EDT"` or the advertiser's timezone. |
| `code` | string | The custom code for the budget interval. The code may only contain alphanumeric characters, periods, underscores or dashes. The code you enter is not case-sensitive (upper- and lower-case characters are treated the same). |
| `lifetime_budget` | double | The lifetime budget in revenue for the budget interval. The revenue currency is defined by the `currency` field on the `insertion_order` object.<br><br>**Note:** If you also set the `lifetime_budget_imps` field within this array, whichever budget is exhausted first will cause spending to stop. Best practice is to only set one of these fields. |
| `lifetime_budget_imps` | int | The lifetime budget in impressions for the budget interval.<br>**Note:** If you add line items to this insertion order, any spend already associated with those line items before they are added to the insertion order is not counted against the lifetime budget of the insertion order. Only spend that occurs while the line item is a child of the insertion order is counted.<br><br>This field defaults to `null` (unlimited).<br><br>**Note:**<br>If you also set the `lifetime_budget` field within this array, whichever budget is exhausted first will cause spending to stop. Best practice is to only set one of these fields. |
| `lifetime_pacing` | boolean | If `true`, the insertion order will attempt to pace the lifetime budget evenly over the budget interval. If `true`:<br> - You must establish a `lifetime_budget` or `lifetime_budget_imps`.<br> - You must establish a `start_date` and `end_date`.<br>You cannot set a `daily_budget`.<br> - You cannot set `enable_pacing` to `false`. |
| `daily_budget` | double | **Note:**<br>This field defaults to `null` (unlimited). Instead, use the line item to set this value.<br>If you also set the `daily_budget_imps` field within this array, whichever budget is exhausted first will cause spending to stop. Best practice is to only set one of these fields. |
| `daily_budget_imps` | int | **Note:** This field defaults to `null` (unlimited). Instead, use the line item to set this value.<br>If you also set the `daily_budget` field within this array, whichever budget is exhausted first will cause spending to stop. Best practice is to only set one of these fields. |
| `enable_pacing` | boolean | If `true`, then spending will be paced over the course of the day. Only applicable if there is a `daily_budget`. |
| `lifetime_pacing_pct` | double | **Note:**<br>Set this field to `100` (the default) and then use the line item to set lifetime pacing.<br><br>A double integer between (and including) 50 and 150, used to set pacing throughout a budget interval. Possible values can be any double between 50 and 150 on the following scale:<br> - `50`: Pace behind schedule.<br> - `100`: Pace evenly.<br> - `150`: Pace ahead of schedule. |

### Political content

This array will only be editable if:

- `is_running_political_ads` is true on the [Advertiser Service](advertiser-service.md).
- `is_running_political_ads` is true on the insertion order.

These fields must be filled out if you are using this insertion order for advertising related to an election, ballot initiative, or political candidate at the local or state level in the United States, or for advertising related to federal election or political candidate in Washington State. They are not required for political advertising at the federal level in other states.

> [!WARNING]
> We do not validate the required fields to make sure they're present when you create an insertion order, but **your creative for state or local political advertising** or **federal advertising that targets Washington State** will not serve if the fields are not filled out. Any update to the `political_content` object should include **all required fields** or ad serving may be disrupted.

| Field | Type | Description |
|:---|:---|:---|
| `billing_name` | string | The name of the person or organization that is purchasing ads on Xandr. This will be automatically filled out with the name of the Xandr [member](member-service.md).<br>**Read Only.** |
| `billing_address_1` | string(255) | The street address for the person or organization that is purchasing ads on Xandr.<br>Enter the contact details for the person or team who can best answer any questions about political advertising on this insertion order.<br>**Required.** |
| `billing_address_2` | string(255) | Optional additional line for the billing address for the person or organization that is purchasing ads on Xandr. |
| `billing_city` | string(100) | City of the billing address for the person or organization that is purchasing ads on Xandr.<br>**Required.** |
| `billing_region` | string(50) | State or region of the billing address for the person or organization that is purchasing ads on Xandr.<br>**Required.** |
| `billing_postal_code` | string(50) | ZIP or postal code of the billing address for the person or organization that is purchasing ads on Xandr.<br>**Required.** |
| `billing_country` | string(50) | Country of the billing address for the person or organization that is purchasing ads on Xandr.<br>**Required.** |
| `billing_phone_code` | string(10) | Country code for the phone number for the person or organization that is purchasing ads on Xandr.<br>**Required.** |
| `billing_phone` | string(50) | Contact phone number for the person or organization that is purchasing ads on Xandr.<br>**Required.** |
| `us_fecid` | string(50) | ID number assigned by the [U.S. Federal Election Committee](https://fec.gov/). |
| `organization_name` | string(100) | Name of the person, group, organization, or business that is advertising (the client that is paying you). For example, a candidate, an agency, or a political consultant.<br>**Required.** |
| `organization_address_1` | string(255) | Address of the person, group, organization, or business that is advertising. For example, a candidate, an agency, or a political consultant.<br>**Required.** |
| `organization_address_2` | string(255) | Optional second line for the address of the person, group, organization, or business that is advertising. |
| `organization_city` | string(100) | City in the address of the person, group, organization, or business that is advertising.<br>**Required.** |
| `organization_region` | string(50) | State or region in the address of the person, group, organization, or business that is advertising.<br>**Required.** |
| `organization_postal_code` | string(50) | ZIP or postal code of the person, group, organization, or business that is advertising.<br>**Required.** |
| `organization_country` | string(50) | Country of the person, group, organization, or business that is advertising.<br>**Required.** |
| `organization_phone_code` | string(10) | Country code for the phone number of the person, group, organization, or business that is advertising.<br>**Required.** |
| `organization_phone` | string(50) | Phone number of the person, group, organization, or business that is advertising.<br>**Required.** |
| `treasurer_name` | string(100) | Treasurer for the committee purchasing the ads, or the individual whose role would most closely fit that of a treasurer.<br>**Required.** |
| `payment_method_type` | enum(1) | How the political organization pays you. Options are:<br> - `"Direct Debit"`<br> - `"Check"`<br> - `"Credit Card"`<br> - `"Other"`. If this is selected, `payment_method_other` is required.<br>**Required.** |
| `political_objective` | string(255) | The candidate or ballot initiative that is supported or opposed.<br>This maps to the **Subject of Ads** field in the UI.<br>**Required.** |
| `payment_method_other` | string(50) | If `"4"` (Other) is selected for `payment_method_type`. Details of how you are being paid for political advertising.<br>**Required.** |
| `is_independent_expenditure_committee` | Boolean | Specifies whether any ads are being paid for by an independent expenditure committee: That is, a third party that spends money on political communications that expressly advocate the election or defeat of a clearly identified candidate and does not coordinate with a candidate, a candidate’s authorized committee, or an agent of the candidate.<br>**Required.** |
| `registration_form` | array | Required for NY and NJ when `is_independent_expenditure_committee` is `true`. New York State and New Jersey require copies of state registration forms from independent expenditure committees making purchases. Creatives won’t serve in New York State or New Jersey until the form is uploaded. Forms must be uploaded with the [Registration Form Service](registration-form-service.md) before their location can be specified in this array.<br>The array must be in the format:<br>`{"file_path": "PATH_AND_FILE_NAME_OF_THE_UPLOADED_FILE"}` |
| `is_ineligible` | Boolean | Notifies you whether all the required fields in the `political_content` array have been filled out (excluding `registration_form`) for political advertising at the state or local level. If the value is `true`, creatives will not serve. The value is recalculated whenever the insertion order is updated.<br><br>**Note:**<br>If `is_ineligible` is `false`, creatives may still be prohibited from serving, based on other factors such as whether the creative has passed audit or whether a registration form has been uploaded for ad buys in states which require it.<br><br>For more information on creative auditing, see "Creative Troubleshooting and FAQ" in the UI documentation.<br>**Read Only.** |
| `government_level` | enum | If `is_running_political_ads` is `true`. Permitted values are:<br> - `state or local`<br> - `federal`<br> - `both` (the default)<br>**Required.** |
| `is_accuracy_acknowledged` | Boolean | Specifies that the Xandr member has certified that the `political_content` information provided is accurate and up-to-date and that Xandr is relying on the accuracy of the information provided. If set to `0` (the default), creatives will not be allowed to serve.<br>**Required.** |

### Stats

> [!WARNING]
> The `stats` object has been **deprecated** (October 17, 2016). Instead, use the [Report Service](report-service.md) to obtain statistical information.

## Examples

### Add a new seamless insertion order with budget intervals

```
$ cat insertion-order.json
{
    "insertion-order": {
        "name": "My Insertion Order LH_EP",
        "budget_intervals": [

            {
                "start_date": "2030-10-10 00:00:00",
                "end_date": "2030-10-12 23:59:59",
                "daily_budget": null,
                "daily_budget_imps": 10,
                "enable_pacing": true,
                "lifetime_budget": null,
                "lifetime_budget_imps": 980,
                "lifetime_pacing": false
            },
            {
                "start_date": "2030-10-13 00:00:00",
                "end_date": "2030-10-18 23:59:59",
                "daily_budget": null,
                "daily_budget_imps": 10,
                "enable_pacing": true,
                "lifetime_budget": null,
                "lifetime_budget_imps": 6,
                "lifetime_pacing": false
            }
        ]
    }
}
$ curl -b cookies -X POST -d @insertion-order.json "https://api.appnexus.com/insertion-order?advertiser_id=11'

{
   "response": {
    "status": "OK",
    "count": 1,
    "start_element": 0,
    "num_elements": 100,
    "insertion-orders": [
        {
            "id": 45797,
            "name": "MyInsertionOrderLH_EP",
            "code": null,
            "state": "active",
            "advertiser_id": 64,
            "start_date": null,
            "end_date": null,
            "last_modified": "2015-03-1718: 41: 57",
            "timezone": "EST5EDT",
            "currency": "USD",
            "budget_type": null,            
            "comments": null,
            "billing_code": null,
            "line_items": null,
            "labels": null,
            "broker_fees": null,
            "budget_intervals": [
                {
                    "id": 684,
                    "start_date": "2030-10-10 00:00:00",
                    "end_date": "2030-10-12 23:59:59",
                    "parent_interval_id": null,
                    "lifetime_budget": null,
                    "lifetime_budget_imps": 980,
                    "lifetime_pacing": false,
                    "enable_pacing": false,
                    "daily_budget_imps": 10,
                    "daily_budget": null
                },
                {
                    "id": 685,
                    "start_date": "2030-10-13 00:00:00",
                    "end_date": "2030-10-18 23:59:59",
                    "parent_interval_id": null,
                    "lifetime_budget": null,
                    "lifetime_budget_imps": 6,
                    "lifetime_pacing": false,
                    "enable_pacing": false,
                    "daily_budget_imps": 10,
                    "daily_budget": null
                }
            ],
            "lifetime_pacing": null,
            "lifetime_budget": null,
            "lifetime_budget_imps": null,
            "enable_pacing": null,
            "lifetime_pacing_span": null,
            "allow_safety_pacing": null,
            "daily_budget": null,
            "daily_budget_imps": null
            }
        ]
    }
}
```

### Add a new seamless insertion order with flexible budget type

```
$ cat insertion-order.json
{
    "insertion-order": {
        "name": "Test-Seamless-IO-GDALI",
        "advertiser_id": "33514",
        "timezone": "UTC",
        "budget_type": "flexible",
        "budget_intervals": [{
            "start_date": "2022-11-01 00:00:00",
            "timezone": "UTC"
        }],
        "currency": "USD"
    }
}



curl -b cookies -X POST -d @insertion-order.json "https://api.appnexus.com/insertion-order?advertiser_id=33514&member_id=958"


{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 6784364,
        "start_element": 0,
        "num_elements": 100,
        "insertion-order": {
            "id": 6784364,
            "name": "Test-Seamless-IO-GDALI",
            "code": null,
            "state": "active",
            "advertiser_id": 33514,
            "profile_id": null,
            "member_id": 958,
            "start_date": null,
            "end_date": null,
            "remaining_days": null,
            "total_days": null,
            "last_modified": "2022-01-26 20:00:29",
            "timezone": "UTC",
            "currency": "USD",
            "comments": null,
            "budget_type": "flexible",
            "billing_code": null,
            "viewability_standard_provider": "iab",
            "is_running_political_ads": false,
            "line_items": null,
            "labels": null,
            "broker_fees": null,
            "budget_intervals": [{
                "id": 16134020,
                "object_id": 6784364,
                "object_type": "insertion_order",
                "start_date": "2022-11-01 00:00:00",
                "end_date": null,
                "timezone": "UTC",
                "code": null,
                "lifetime_budget": null,
                "lifetime_budget_imps": null,
                "daily_budget_imps": null,
                "daily_budget": null,
                "enable_pacing": false,
                "lifetime_pacing": false,
                "lifetime_pacing_pct": null,
                "daily_budget_imps_opt": null,
                "daily_budget_opt": null
            }],
            "tpas_details": null,
            "political_content": null,
            "lifetime_pacing": null,
            "lifetime_budget": null,
            "lifetime_budget_imps": null,
            "enable_pacing": null,
            "lifetime_pacing_span": null,
            "allow_safety_pacing": null,
            "daily_budget": null,
            "daily_budget_imps": null,
            "lifetime_pacing_pct": null
        }
    }
}
```

### Add a new non-seamless insertion order

```
$ cat insertion-order.json

{
    "insertion-order":{
        "name":"My Insertion Order"
    }
}

$ curl -b cookies -X POST -d @insertion-order.json "https://api.appnexus.com/insertion-order?advertiser_id=11"
 
{
    "response":{
        "status":"OK",
        "id":2
    }
}
```

### View all insertion orders for advertiser 11

```
$ curl -b cookies "https://api.appnexus.com/insertion-order?advertiser_id=11"

    "response":{
        "status":"OK",
        "count":2,
        "start_element":0,
        "num_elements":100,
        "insertion-orders":[
            {
                "id":1,
                "name":"TEST CPM IO",
                "code":null,
                "billing_code":"3az56",
                "state":"active",
                "advertiser_id":11,
                "start_date":"2010-07-01 00:00:00",
                "end_date":"2010-09-01 23:59:59",
                "last_modified":"2010-08-02 23:44:14",
                "timezone":"EST5EDT",
                "currency":"USD",
                "budget_type": null,                
                "comments":null,
                "users":null,
                "line_items":[
                    {
                        "id":5588,
                        "line_item_type": "standard_v1",
                        "name":"Test IO Line Item CPM",
                        "code":null,
                        "state":"active",
                        "start_date":null,
                        "end_date":null,
                        "timezone":"EST5EDT"
                    }
                ],
                "labels":null,
                "broker_fees":null,
                "lifetime_budget":null,
                "lifetime_budget_imps":1000,
                "daily_budget":null,
                "daily_budget_imps":100,
                "enable_pacing":true,
                "lifetime_pacing":false,
                "lifetime_pacing_span":null,
                "allow_safety_pacing":true
            },
            {
                "id":2,
                "name":"TEST CPM IO - Expired Flight Dates",
                "code":null,
                "billing_code":null,
                "state":"active",
                "advertiser_id":2396,
                "start_date":"2010-06-01 00:00:00",
                "end_date":"2010-06-30 23:59:59",
                "last_modified":"2010-07-30 01:29:28",
                "timezone":"EST5EDT",
                "currency":"USD",
                "budget_type": null,                
                "comments":null,
                "users":null,
                "line_items":[
                    {
                        "id":5588,
                        "line_item_type": "standard_v1",
                        "name":"Test IO Line Item CPM",
                        "code":null,
                        "state":"active",
                        "start_date":null,
                        "end_date":null,
                        "timezone":"EST5EDT"
                    }
                ],
                "labels":null,
                "broker_fees":null,
                "lifetime_budget":null,
                "lifetime_budget_imps":1000,
                "daily_budget":null,
                "daily_budget_imps":100,
                "enable_pacing":true,
                "lifetime_pacing":false,
                "lifetime_pacing_span":null,
                "allow_safety_pacing":true
            }
        ]
}
```

### Delete a budget interval (on a seamless insertion order)

> [!NOTE]
> The deletion of budget intervals on an insertion order will affect the underlying line items differently, depending on their type:
>
> - For non-ALI (augmented) line items: The deletion of budget intervals on the parent insertion order will automatically delete the relevant budget interval on the line item(s). Do not attempt to delete budget intervals from the line item object. Always use the parent insertion order to delete a budget interval.
> - For ALI line items: You cannot delete a budget interval on a parent insertion until you have first removed it from all of the underlying *augmented* line items associated with the insertion order. Since augmented line items may have more than one budget interval within a given budget interval on the parent insertion order, be sure to remove all budget intervals on the augmented line line item that fall within the insertion order budget interval you intend to remove. Once the budget interval(s) has been removed from the augmented line items, it can be removed from the insertion order.

```
//To delete a budget interval, both the "start_date" and "end_date" fields must be set to null.
$ cat delete-budget-interval
{
  "insertion-order": {
    "budget_intervals": [
      {
        "id": 79970,
        "start_date": null,
        "end_date": null
      }
    ]
  }
}
$ curl -b cookies -X PUT -d @delete-budget-interval "https://api.appnexus.com/insertion-order?id=357903"
{
  "response": {
    "status": "OK",
    "count": 1,
    "id": "357903",
    "start_element": 0,
    "num_elements": 100,
    "insertion-order": {
      "id": 357903,
      "name": "Seamless Insertion Order",
      "code": null,
      "state": "active",
      "advertiser_id": 1133550,
      "start_date": null,
      "end_date": null,
      "remaining_days": null,
      "total_days": null,
      "last_modified": "2016-07-26 21:33:34",
      "timezone": "America/Argentina/Buenos_Aires",
      "currency": "USD",
      "budget_type": null,
      "comments": null,
      "billing_code": null,
      "line_items": [
        {
          "id": 3188266,
          "line_item_type": "standard_v1",
          "name": "Seamless Line Item",
          "code": null,
          "state": "active",
          "start_date": null,
          "end_date": null,
          "timezone": "America/Argentina/Buenos_Aires"
        }
      ],
      "spend_protection_pixels": null,
      "labels": null,
      "broker_fees": null,
      "budget_intervals": [
        {
          "id": 79969,
          "object_id": 357903,
          "object_type": "insertion_order",
          "start_date": "2016-08-01 00:00:00",
          "end_date": "2016-08-31 23:59:59",
          "code": null,
          "timezone": "America/Argentina/Buenos_Aires",
          "lifetime_budget": 100,
          "lifetime_budget_imps": null,
          "lifetime_pacing": false,
          "enable_pacing": true,
          "daily_budget_imps": null,
          "daily_budget": null
        }
      ],
      "tpas_details": null,
      "lifetime_pacing": null,
      "lifetime_budget": null,
      "lifetime_budget_imps": null,
      "enable_pacing": null,
      "lifetime_pacing_span": null,
      "allow_safety_pacing": null,
      "daily_budget": null,
      "daily_budget_imps": null,
      "lifetime_pacing_pct": null
    },
    "dbg_info": {
      ...
    }
  }
}
```

### Modify a budget interval (on a seamless insertion order)

```
$ cat modify-budget-interval
{

  "insertion-order": {
    "budget_intervals": [
      {
        "id": 79969,
        "lifetime_budget": 100
      }
    ]
  }
}
$ curl -b cookies -X PUT -d @modify-budget-interval "https://api.appnexus.com/insertion-order?id=357903"
{
  "response": {
    "status": "OK",
    "count": 1,
    "id": "357903",
    "start_element": 0,
    "num_elements": 100,
    "insertion-order": {
      "id": 357903,
      "name": "Seamless Insertion Order",
      "code": null,
      "state": "active",
      "advertiser_id": 1133550,
      "start_date": null,
      "end_date": null,
      "remaining_days": null,
      "total_days": null,
      "last_modified": "2016-07-29 17:26:26",
      "timezone": "America/Argentina/Buenos_Aires",
      "currency": "USD",
      "budget_type": null,
      "comments": null,
      "billing_code": null,
      "line_items": null,
      "spend_protection_pixels": null,
      "labels": null,
      "broker_fees": null,
      "budget_intervals": [
        {
          "id": 79969,
          "object_id": 357903,
          "object_type": "insertion_order",
          "start_date": "2016-08-01 00:00:00",
          "end_date": "2016-08-31 23:59:59",
          "code": null,          
          "timezone": "America/Argentina/Buenos_Aires",
          "lifetime_budget": 100,
          "lifetime_budget_imps": null,
          "lifetime_pacing": false,
          "enable_pacing": true,
          "daily_budget_imps": null,
          "daily_budget": null
        }
      ],
      "tpas_details": null,
      "lifetime_pacing": null,
      "lifetime_budget": null,
      "lifetime_budget_imps": null,
      "enable_pacing": null,
      "lifetime_pacing_span": null,
      "allow_safety_pacing": null,
      "daily_budget": null,
      "daily_budget_imps": null,
      "lifetime_pacing_pct": null
    },
    "dbg_info": {
      ...
    }
  }
}
```

### Delete an insertion order

```
curl -b cookies -X DELETE "https://api.appnexus.com/insertion-order?id=5851054&advertiser_id=5413231"
```

```
{"response":
    {
        "status":"OK",
        "count":1,
        "start_element":null,
        "num_elements":null,
        "dbg_info":
            {
                "warnings":[],
                "version":"1.0.190",
                "output_term":"not_found"}
            }
    }
}
```

## Related topics

- [API Best Practices](api-best-practices.md)
- [API Semantics](api-semantics.md)
