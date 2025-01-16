---
title: Data Science Toolkit - Bonsai Language Features
description: Explore Bonsai Language features used for assessing impressions in your custom models with syntax explanations and usage examples.
ms.custom: data-science
ms.date: 10/28/2023
---

# Data Science Toolkit - Bonsai language features

This page lists the Bonsai Language features that you can use to evaluate impressions as part of your custom model logic. For each feature, we explain the syntax and provide an example to demonstrate usage.

> [!NOTE]
>
> - Bids that are negative or zero (0) are not supported unless explicitly specified in the feature description. Do not use these expressions or unexpected results may occur. It is best to specify `no_bid` explicitly using [Smart Leaves](bonsai-smart-leaves.md).
> - The bids calculated by the model are always expressed in the currency set on the advertiser, even if you have specified a different currency for the campaign.

## Simple features

### Country

Evaluate impressions based on the user's country or region.

**Keyword**: `country`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: Country ID or code, such as `233` or `"US"`. Use the [Country Service](../digital-platform-api/country-service.md) to retrieve these IDs or codes.

**Example**:

```
if country = "US":
5
elif country = 70:
3
else:
0.1
```

### Video content targeting

Evaluate impressions based on the user's video content inventory.

**Keyword**: `video_duration, video_delivery_type, video_genre, video_program_type, video_rating, video_network`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**:

**Example**:

```
if any video_duration in (1,2), video_delivery_type in (1,2):
value: 0.050000
elif every video_genre in (1,2,3), video_rating =1:
value: 0.060000
elif every video_network in (1,3), video_genre in (1,2):
value: 0.0700000
elif not video_network =2:
value: 0.01
```

### Region

Evaluate impressions based on the user's geographic region.

**Keyword**: `region`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: Region ID or country/region code combination, such as `"US:NY"`. Use the [Region Service](../digital-platform-api/region-service.md) to retrieve these IDs and codes.

**Example**:

```
if region = 123:
5
elif region = "US:NJ":
3
else:
0.1
```

### City

Evaluate impressions based on the user's city.

**Keyword**: `city`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: City ID or country/region/city code combination, such as `"US:NY:New York"`. Use the [City Service](../digital-platform-api/city-service.md) to retrieve these IDs and codes.

**Example**:

```
if city = 162:
5
elif city = "US:MA:Boston":
3
else:
0.1
```

### DMA

Evaluate impressions based on the user's DMA (designated market area).

**Keyword**: `dma`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: DMA ID, such as `602` (for Chicago metro area). Use the [City Service](../digital-platform-api/city-service.md) to retrieve DMA IDs.

**Example**:

```
if dma = 602:
5
elif dma = 603:
3
else:
0.1
```

### Postal code

Evaluate impressions based on the user's postal code. Postal code is available only for some mobile impressions and impressions from external supply partners.

**Keyword**: `postal_code`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: Postal code ID (an integer) or country/postal code combination (a string such as `"CA:J0K 1B0"` or `"US:10010"`). Includes US zip codes.
Use the Postal Code Service (documented in the [Profile Service](../digital-platform-api/profile-service.md)) to retrieve postal code IDs.

**Example**:

```
if postal_code in ("CA:J0k 1B0", "US:10010"):
5
elif postal_code = 1367515:
3
else:
0.1
```

### Postal code list

Evaluate impressions based on the user's postal code list.

**Keyword**: `postal_code_list[ID]`

**Operator**: None for presence, not for absence.

**Value**: None

**Example**:

```
elif postal_code_list[120]:
value: 1
```

### Deal list

Evaluate impressions based on the user's deal list.

**Keyword**: `deal_list[ID]`

**Operator**: None for presence, not for absence.

**Value**: None

**Example**:

```
elif deal_list[4107]:
value: 2
```

### Size

Evaluate impressions based on placement size. Note that in case `promo_sizes` are passed in the ad call, the evaluation will be performed using the primary size only.

**Keyword**: `size`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: String representing placement dimensions, formatted as `"WIDTHxHEIGHT"`.

**Example**:

```
if size = "300x250":
5
elif size = "250x250":
3
else:
0.1
```

### Day of week

Evaluate impressions based on specific days of the week.

**Keyword**: `user_day`

**Operator**: Any

**Value**: Day of the week. Possible values: `0` - `6`, where `0` is Sunday and `6` is Saturday.

**Example**:

```
if user_day in (1,2,3,4,5):
5
else:
0.1
```

### Hour of day

Evaluate impressions based on specific hours of the day.

**Keyword**: `user_hour`

**Operator**: Any

**Value**: Hour of the day, in the user's timezone. Possible values: `0` - `23`, where `0` is midnight and `23` is 11 pm.

**Example**:

```
if user_hour in (18,19,20,21,22,23):
5
elif user_hour in (14,15,16,17):
4
else:
2
```

### Operating system family

Evaluate impressions based on the user's operating system.

**Keyword**: `os_family`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: Operating System Family ID or name, such as `2` or `"Android"`. Use the [Operating System Family Service](../digital-platform-api/operating-system-family-service.md) to retrieve these IDs and names.

**Example**:

```
if os_family = 2:
5
elif os_family = "Apple iOS":
4
else:
0.2
```

### Operating system version

Evaluate impressions based on the specific version of the user's operating system.

> [!NOTE]
> For the `os_extended` feature, a look up table result of 0 is considered equal to missing.

**Keyword**: `os_extended`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: Operating System Extended ID, such as 81 for `"10.8 Mountain Lion"`. Use the [Operating System Extended Service](../digital-platform-api/operating-system-extended-service.md) to retrieve these IDs.

> [!NOTE]
> Operating system ID is listed as `operating_system` in log-level data.

**Example**:

```
if os_extended = 81:
5
elif os_extended = 82:
4
else:
0.2
```

### Browser

Evaluate impressions based on the user's browser.

> [!NOTE]
> For the `browser` feature, a look up table result of 0 is considered equal to missing.

**Keyword**: `browser`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: Browser ID or name, such as `8` or `"Chrome (all versions)"`. Use the [Browser Service](../digital-platform-api/browser-service.md) to retrieve these IDs and names.

**Example**:

```
if browser = 8:
3
elif browser = "Safari (all versions)":
2.5
else:
0.2
```

### Browser language

Evaluate impressions based on the browser language.

> [!NOTE]
> For the `language` feature, a look up table result of 0 is considered equal to missing.

**Keyword**: `language`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: Language ID. Use the [Language Service](../digital-platform-api/language-service.md) to retrieve these IDs.

**Example**:

```
if language = 1:
3
elif language = 0:
1
else:
0
```

### Gender

Evaluate impressions based on the user's gender. Note that gender is available only in cases where the publisher passes it in the ad call. For more information on ad calls, see "Placement Tag Parameters" in documentation.

**Keyword**: `user_gender`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: Gender of the user. Possible values:

- `"female"`
- `"male"`
- `"unknown"`

**Example**:

```
if user_gender in (male, female):
5
else:
2
```

### Domain

Evaluate impressions based on domain.

**Keyword**: `domain`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: String representing a top-level domain name, such as `"food.com"` or `"books"`.

**Example**:

```
if domain = "food.com":
3
elif domain = "books.com":
2.5
else:
0.2
```

### IP address

Evaluates impressions based on IP address.

> [!NOTE]
> Customers in countries or regions that conform to GDPR regulations should be aware that when targeting IP addresses or IP ranges, either in your line item, Bonsai tree, or logistic regression model, there is a possibility the address may be truncated. For details on this process, see our [Service Policies](../policies-regulations/index.yml).

**Keyword**: `ip_address`

**Operator**: `in`

**Value**: String representing any valid IP address, including subnet notation. For example, the range `(192.168.0.1, 10.0.0.0/24)` indicates IP addresses 192.168.0.1 and 10.0.0.0-10.0.0.255.

**Example**:

```
if ip_address in (192.168.0.1, 10.0.0.0/24):
5
else:
1
```

### Fold position

Evaluate impressions based on specific placement positions relative to the fold of the page.

**Keyword**: `position`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: Fold position. Possible values:

- `0 or "unknown"` - Use these values to target placements where the fold position is unknown.
- `1 or "above"` - Use these values to target placements above the fold.
- `2 or "below"` - Use these values to target placements below the fold.

**Example**:

```
if position = "above":
3
elif position = 2:
1
else:
0
```

### Placement

Evaluate impressions based on specific placements.

**Keyword**: `placement`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: Placement ID.

> [!NOTE]
> Placement ID is listed as `tag_id` in log-level data.

**Example**:

```
if placement = 300:
5
elif placement = 301:
4.5
else:
0.2
```

### Placement group

Evaluate impressions based on specific placements groups.

**Keyword**: `placement_group`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: Placement group ID.

> [!NOTE]
> Placement group ID is listed as `site_id` in log-level data.

**Example**:

```
if placement_group = 155:
5
elif placement_group = 156:
4.50
else:
0.2
```

### Publisher

Evaluate impressions based on specific publishers.

**Keyword**: `publisher`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: Publisher ID.

> [!NOTE]
> Publisher ID is listed as `publisher_id` in log-level data.

**Example**:

```
if publisher = 1300:
5
elif publisher = 1301:
4.50
else:
0.2
```

### Seller member

Evaluate impressions based on specific seller members.

**Keyword**: `seller_member_id`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: Member ID of the seller.

**Example**:

```
if any seller_member_id = 100, seller_member_id = 175:
4
elif any seller_member_id = 500, seller_member_id = 501:
3.50
else:
0.2
```

### Supply type

Evaluate impressions based on specific types of supply.

**Keyword**: `supply_type`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: Supply type ID or name. Possible values:

- `0 or "web"` - Use either of these values to target standard web sites.
- `1  or "mobile_web"` - Use either of these values to target web sites optimized for browsers on mobile tablets and phones.
- `2  or "mobile_app"` - Use either of these values to target apps installed on mobile tablets and phones.

**Example**:

```
if supply_type = "web":
4
elif supply_type = "mobile_web":
3
elif supply_type = 2:
2
else:
0.2
```

### Device type

Evaluate impressions based on specific types of physical devices.

**Keyword**: `device_type`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: Device type name. Possible values:

- `"pc & other devices"` - Use this value to target desktops and laptops.
- `"phone"` - Use this value to target mobile phones.
- `"tablet"` - Use this value to target mobile tablets.

**Example**:

```
if device_type = "pc & other devices":
5
elif device_type = "tablet":
4
elif device_type = "phone":
3.50
else:
0
```

### Device model

Evaluate impressions based on specific models of physical devices.

**Keyword**: `device_model`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: Device model ID. Use the [Device Model Service](../digital-platform-api/device-model-service.md) to retrieve these IDs.

> [!NOTE]
> Device model ID is listed as `device_id` in log-level data.

**Example**:

```
if device_model = 46:
5
elif device_model = 47:
4.75
elif device_model = 48:
3.50
else:
0
```

### Carrier

Evaluate impressions based on specific mobile carriers.

**Keyword**: `carrier`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: Mobile carrier ID or name, such as `14` or `"Verizon"`. Use the [Carrier Service](../digital-platform-api/carrier-service.md) to retrieve these IDs and names.

**Example**:

```
if carrier = 14:
4
elif carrier = "Sprint":
3.50
else:
0.2
```

### Mobile app

Evaluate impressions based on specific mobile apps.

**Keyword**: `mobile_app`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: Mobile app ID or names. Use [Mobile App Service](../digital-platform-api/mobile-app-service.md) to retrieve these IDs or names.

**Example**:

```
if mobile_app = 1:
5
elif mobile_app = 2:
3.5
elif mobile_app = "Candy Crush Saga":
2
else:
0.2
```

### Mobile app instance

Evaluate impressions based on specific mobile app installations.

**Keyword**: `mobile_app_instance`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: Mobile app instance ID. Use [Mobile App Instance Service](../digital-platform-api/mobile-app-instance-service.md) to retrieve these IDs.

**Example**:

```
if mobile_app_instance = 1:
5
elif mobile_app_instance = 2:
3.5
elif mobile_app_instance = 3:
2
else:
0.2
```

### Mobile app bundle

Evaluate impressions based on specific mobile app bundles.

**Keyword**: `mobile_app_bundle`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: Mobile app bundle ID. Use [Mobile App Instance Service](../digital-platform-api/mobile-app-instance-service.md) to retrieve these IDs.

**Example**:

```
if mobile_app_bundle in ("553834731", "com.king.candycrushsaga"):
5
else:
0.2
```

### Cookie age

Evaluate impressions based on how long, in minutes, the user has had a Xandr cookie.

**Keyword**: `cookie_age`

**Operator**: Any

**Value**: Positive integer representing the number of minutes that the user has had a Xandr cookie.
This value can be absent, which indicates that the user does not have a Xandr cookie.

**Example**:

```
if cookie_age > 30:
2
else:
0.2
```

### Predicted IAB viewability rate

(Previously known as "Estimated IAB Viewability Rate".) Evaluate web display impressions by how likely they are to be measured as viewable by the IAB standard, as determined by Xandr optimization.

**Keyword**: `predicted_iab_view_rate`

**Alias (deprecated)**: `estimated_iab_viewthrough_rate`

**Operator**: Any

**Value**: Decimal number between `0` and `1`, representing a percentage.

**Example**:

```
if predicted_iab_view_rate = 1:
5
elif predicted_iab_view_rate >= 0.75:
3.5
elif predicted_iab_view_rate >= 0.50:
2
else:
0
```

### Predicted IAB viewability rate over total

Evaluate web display impressions by how likely they are to be measured as viewable, over the total number of impressions (viewed / total impressions), by the IAB standard, as determined by Xandr optimization.

**Keyword**: `predicted_iab_view_rate_over_total`

**Operator**: Any

**Value**: Decimal number between `0` and `1`, representing a percentage.

**Example**:

```
if predicted_iab_view_rate_over_total = 1:
5
elif predicted_iab_view_rate_over_total >= 0.75:
3.5
elif predicted_iab_view_rate_over_total >= 0.50:
2
else:
0
```

### Predicted IAB video viewability rate

Evaluate web video impressions by how likely they are to be measured as viewable by the IAB standard, as determined by Xandr optimization.

**Keyword**: `predicted_iab_video_view_rate`

**Operator**: Any

**Value**: Decimal number between `0` and `1`, representing a percentage.

**Example**:

```
if predicted_iab_video_view_rate = 1:
5
elif predicted_iab_video_view_rate >= 0.75:
3.5
elif predicted_iab_video_view_rate >= 0.50:
2
else:
0
```

### Predicted IAB video viewability rate over total

Evaluate web video impressions by how likely they are to be measured as viewable over the total number of impressions (viewed / measured impressions) by the custom definition of 100% pixels viewable for at least 1 second, as determined by Xandr optimization.

**Keyword**: `predicted_iab_video_view_rate_over_total`

**Operator**: Any

**Value**: Decimal number between `0` and `1`, representing a percentage.

**Example**:

```
if predicted_100pv1s_display_view_rate = 1:
5
elif predicted_100pv1s_display_view_rate >= 0.75:
3.5
elif predicted_100pv1s_display_view_rate >= 0.50:
2
else:
0
```

### Predicted display viewability rate (100% view, one second duration)

Evaluate display video impressions by how likely they are to be measured as viewable (viewed / measured impressions) by the custom definition of 100% pixels viewable for at least 1 second, as determined by Xandr optimization.

**Keyword**: `predicted_100pv1s_display_view_rate`

**Operator**: Any

**Value**: Decimal number between `0` and `1`, representing a percentage.

**Example**:

```
if predicted_100pv50pd_video_view_rate = 1:
5
elif predicted_100pv50pd_video_view_rate >= 0.75:
3.5
elif predicted_100pv50pd_video_view_rate >= 0.50:
2
else:
0
```

### Predicted display viewability rate over total (100% view, one second duration)

Evaluate web display impressions by how likely they are to be measured as viewable  (viewed / total impressions) by the custom definition of 100% pixels viewable for at least 1 second, as determined by Xandr optimization.

**Keyword**: `predicted_100pv1s_display_view_rate_over_total`

**Operator**: Any

**Value**: Decimal number between `0` and `1`, representing a percentage.

**Example**:

```
if predicted_100pv1s_display_view_rate_over_total = 1:
5
elif predicted_100pv1s_display_view_rate_over_total >= 0.75:
3.5
elif predicted_100pv1s_display_view_rate_over_total >= 0.50:
2
else:
0
```

### Predicted video viewability rate (100% view, 50% duration, sound on)

Evaluate web video impressions by how likely they are to be measured as viewable (viewed/measured impressions) where a "view" is defined as an ad which is 100% visible and has played for at least 50% of its duration, with the sound on. Likelihood is determined by Xandr optimization.

**Keyword**: `predicted_100pv50pd_video_view_rate`

**Operator**: Any

**Value**: Decimal number between `0` and `1`, representing a percentage.

**Example**:

```
if predicted_100pv50pd_video_view_rate = 1:
5
elif predicted_100pv50pd_video_view_rate >= 0.75:
3.5
elif predicted_100pv50pd_video_view_rate >= 0.50:
2
else:
0
```

### Predicted video viewability rate over total (100% view, 50% duration, sound on)

Evaluate web video impressions by how likely they are to be measured as viewable, over total number of impressions (viewed/total impressions), where a "view" is defined as an ad which is 100% visible and has played for at least 50% of its duration, with the sound on. Likelihood is determined by Xandr optimization.

**Keyword**: `predicted_100pv50pd_video_view_rate_over_total`

**Operator**: Any

**Value**: Decimal number between `0` and `1`, representing a percentage.

**Example**:

```
if predicted_100pv50pd_video_view_rate_over_total = 1:
5
elif predicted_100pv50pd_video_view_rate_over_total >= 0.75:
3.5
elif predicted_100pv50pd_video_view_rate_over_total >= 0.50:
2
else:
0
```

### Predicted video completion rate

Evaluate web video impressions by how likely they are to be completed, as determined by Xandr optimization.

**Keyword**: `predicted_video_completion_rate`

**Alias (Deprecated)**: `estimated_video_completion_rate`

**Operator**: Any

**Value**: Decimal number between `0` and `1`, representing a percentage. `0` represents non-video inventory.

**Example**:

```
if predicted_video_completion_rate = 1:
5
elif predicted_video_completion_rate >= 0.75:
3.5
elif predicted_video_completion_rate >= 0.50:
2
else:
0
```

### Xandr intended audience

Evaluates impressions based on their intended audience as determined by the Xandr platform audit.

**Keyword**: `appnexus_intended_audience`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: `"general"`, `"children"`, `"young_adult"`, or `"mature"`.

**Example**:

```
if appnexus_intended_audience = "mature":
1
else:
0
```

### Seller intended audience

Evaluates impressions based on their intended audience as determined by self-audit. For more information, see "Inventory Self-Classification" in documentation and [Profile Service](../digital-platform-api/profile-service.md).

**Keyword**: `seller_intended_audience`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: `"general"`, `"children"`, `"young_adult"`, or `"mature"`.

**Example**:

```
if appnexus_intended_audience = "general":
1
else:
0
```

### Xandr audited status

Evaluates whether inventory has been audited by Xandr.

**Keyword**: `appnexus_audited`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`.

**Value**: `true` or `false`

**Example**:

```
if appnexus_audited = true:
1.0
else:
0.0
```

### Self-audited status

Evaluates whether inventory has been audited by the publisher.

**Keyword**: `self_audited`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`.

**Value**: `true` or `false`

**Example**:

```
if self_audited = true:
1.0
else:
0.0
```

### User group

Evaluates whether the user belongs to a randomly-assigned group. Each Xandr user has a persistent user group from 0 to 999. You may want to use the user group to test various strategies in parallel and compare their performance. Different tests should partition the thousand user groups differently; otherwise, concurrent tests will interact with each other and it will be difficult to interpret results. For more information, see [Test and Control Targeting](../monetize/test-and-control-targeting.md) in documentation.

**Keyword**: `user_group`

**Operator**: Any

**Value**: Integer between `0` and `999`.

**Example**:

```
if user_group <= 249:
1.0
elif user_group <= 499:
2.0
elif user_group <= 749:
3.0
elif user_group <= 999:
4.0
else:
0.0
```

### Campaign month frequency (system admins only)

Evaluate impressions based on the number of impressions seen by a user for the current campaign in the current month.

**Keyword**: `campaign_month_frequency`

**Operator**: `=<`, `<=`, `presence/absence`, `in`, `comparison`, `not`, and `range`.

**Value**: Positive integer representing the number of impressions seen by a user for the current campaign in the current calendar. `0` indicates no frequency information is available (the user has not seen this object in the current calendar).

**Example**:

```
if campaign_month_frequency < 2 :
5
else :
0.1
```

### Line item month frequency

Evaluate impressions based on the number of impressions seen by a user for the current line item in the current month.  

**Keyword**: `line_item_month_frequency`

**Operator**: `=<`, `<=`, `presence/absence`, `in`, `comparison`, `not`, and `range`.

**Value**: Positive integer representing the number of impressions seen by a user for the current line item in the current month. `0` indicates no frequency information is available (the user has not seen a creative relating to this object on the current month).

**Example**:

```
if line_item_month_frequency < 2:
5
else:
0.1
```

### Advertiser month frequency

Evaluate impressions based on the number of ads seen by a user on the current month.

**Keyword**: `advertiser_month_frequency`

**Operator**: `=<`, `<=`, `presence/absence`, `in`, `comparison`, `not`, and `range`.

**Value**: Positive integer representing the number of ads seen by a user on the current month. `0` indicates no frequency information is available (the user has not seen this object on the current month).

**Example**:

```
if advertiser_month_frequency < 2:
5
else:
0.1
```

### Campaign hour frequency

Evaluate impressions based on the number of ads seen by a user on the current hour.

**Keyword**: `campaign_hour_frequency`

**Operator**: `=<`, `<=`, `presence/absence`, `in`, `comparison`, `not`, and `range`.

**Value**: Positive integer representing the number of ads seen by a user on the current hour. `0` indicates no frequency information is available (the user has not seen this object on the current hour).

**Example**:

```
if campaign_hour_frequency < 2:
5
else:
0.1
```

### Line item hour frequency

Evaluate impressions based on the number of ads seen by a user on the current hour.

**Keyword**: `line_item_hour_frequency`

**Operator**: `=<`, `<=`, `presence/absence`, `in`, `comparison`, `not`, and `range`.

**Value**: Positive integer representing the number of ads seen by a user on the current hour. `0` indicates no frequency information is available (the user has not seen this object on the current hour).

**Example**:

```
if line_item_hour_frequency < 2:
5
else:
0.1
```

### Advertiser hour frequency

Evaluate impressions based on the number of ads seen by a user on the current hour.

**Keyword**: `advertiser_hour_frequency`

**Operator**: `=<`, `<=`, `presence/absence`, `in`, `comparison`, `not`, and `range`.

**Value**: Positive integer representing the number of ads seen by a user on the current hour. `0` indicates no frequency information is available (the user has not seen this object on the current hour).

**Example**:

```
if advertiser_hour_frequency < 2:
2
else:
0.1
```

### Campaign week frequency (system admins only)

Evaluate impressions based on the number of ads seen by a user on the current week, starting on Sunday.

**Keyword**: `campaign_week_frequency`

**Operator**: `=<`, `<=`, `presence/absence`, `in`, `comparison`, `not`, and `range`.

**Value**: Positive integer representing the number of ads seen by a user on the current week. `0` indicates no frequency information is available (the user has not seen this object on the current week).

**Example**:

```
if campaign_week_frequency < 2 :
5
else :
0.1
```

### Line item week frequency

Evaluate impressions based on the number of ads seen by a user on the current week, starting on Sunday.  

**Keyword**: `line_item_week_frequency`

**Operator**: `=<`, `<=`, `presence/absence`, `in`, `comparison`, `not`, and `range`.

**Value**: Positive integer representing the number of ads seen by a user on the current week. `0` indicates no frequency information is available (the user has not seen this object on the current week).

**Example**:

```
if line_item_week_frequency < 2:
5
else:
0.1
```

### Advertiser week frequency

Evaluate impressions based on the number of ads seen by a user on the current week, beginning on Sunday.  

**Keyword**: `advertiser_week_frequency`

**Operator**: `=<`, `<=`, `presence/absence`, `in`, `comparison`, `not`, and `range`.

**Value**: Positive integer representing the number of ads seen by a user on the current week. `0` indicates no frequency information is available (the user has not seen this object on the current week).

**Example**:

```
if advertiser_week_frequency < 2:
5
else:
0.1
```

### Campaign day frequency (system admins only)

Evaluate impressions based on the number of ads seen by a user on the current day.

**Keyword**: `campaign_day_frequency`

**Operator**: `=<`, `<=`, `presence/absence`, `in`, `comparison`, `not`, and `range`.

**Value**: Positive integer representing the number of ads seen by a user on the current day. `0` indicates no frequency information is available (the user has not seen this object on the current day).

**Example**:

```
if campaign_day_frequency < 2 :
5
else :
0.1
```

### Campaign recency (system admins only)

Evaluate whether recency data is available for a user, and, if available, the number of minutes since a user has seen an ad.

**Keyword**: `campaign_recency`

**Operator**: `=<`, `<=`, `presence/absence`, `in`, `comparison`, `not`, and `range`.

**Value**: A positive integer indicating the number of minutes since a user has seen an impression, rounded down. 59 seconds will evaluate to `0`, 61 seconds will evaluate to 1. `0` means the impression was seen very recently. `Null` means no recency data is available (the user has not seen this impression before).

**Example**:

```
if campaign_recency < 2 :
2
else :
0.1
```

### Line item recency

Evaluate whether recency data is available for a user, and, if available, the number of minutes since a user has seen an ad.

**Keyword**: `line_item_recency`

**Operator**: `=<`, `<=`, `presence/absence`, `in`, `comparison`, `not`, and `range`.

**Value**: A positive integer indicating the number of minutes since a user has seen an impression, rounded down. 59 seconds will evaluate to `0`, 61 seconds will evaluate to 1. `0` means the impression was seen very recently. `Null` means no recency data is available (the user has not seen this impression before).

**Example**:

```
if line_item_recency < 2:
5
else:
0.1
```

### Advertiser recency

Evaluate whether recency data is available for a user, and, if available, the number of minutes since a user has seen an ad.

**Keyword**: `advertiser_recency`

**Operator**: `=<`, `<=`, `presence/absence`, `in`, `comparison`, `not`, and `range`.

**Value**: A positive integer indicating the number of minutes since a user has seen an impression, rounded down. 59 seconds will evaluate to `0`, 61 seconds will evaluate to 1. `0` means the impression was seen very recently. `Null` means no recency data is available (the user has not seen this impression before).

**Example**:

```
if advertiser_recency < 2:
5
else:
0.1
```

### Creative

Evaluate impressions based on creative.

**Keyword**: `creative`

**Operator**: Any

**Value**: String representing creative ID (must be an integer).

**Example**:

```
if creative=12345:
5
else:
0.1
```

### Creative size

Evaluate impressions based on creative size.

**Keyword**: `creative_size`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`. To test for multiple values, use `in`.

**Value**: String representing creative dimensions, formatted as `"WIDTHxHEIGHT"`.

**Example**:

```
if creative_size = "300x250":
5
elif creative_size = "250x250":
3
else:
0.1
```

### Deal ID

Evaluate impressions based on Deal ID.  

**Keyword**: `deal_id`

**Operator**: Any except `range`.

**Value**: String representing deal ID as an integer.

**Example**:

```
if deal_id in (12345,98765):
1.0
else:
0.1
```

### Random1, Random2, Random 3

Evaluate impressions based on a randomizing variable between `0` and `1`. When used, this parameter adds some randomness to the Bonsai algorithm.

**Keyword**: `random1`, `random2`, `random3`

**Operator**: Any. To test for multiple values, use `in`.

**Value**: A value between `0` and `1`, formatted as a decimal up to 6 decimal places.

**Example**:

```
if random1 > 0.8:
1.0
elif random1 range (0.4, 0.8):
2.0
else:
0.1
```

### Inventory URL ID

Evaluate impressions based on the Inventory URL ID\* which maps to an inventory URL.

**Keyword**: `inventory_url_id`

**Operator**: Any except `<`, `>`, `<=`, `>=`, and `range`.

**Value**: Inventory URL ID (an integer).

**Example**:

```
if inventory_url_id=12345:
5
else:
0.1
```

\* Only available on Augmented Line Items

## Compound features

The simple features above let you evaluate a single aspect of the impression (country/region, cookie age, mobile app, etc.). The compound [Segment](#segment) and [Frequency/Recency](#frequencyrecency) features are more nuanced; they let you evaluate multiple attributes of these features, such as the age of a segment or the segment value.

### Segment

- [Segment Presence/Absence](#segment-presenceabsence)
- [Segment Age](#segment-age)
- [Segment Value](#segment-value)

#### Segment presence/absence

Evaluate impressions based on the presence of the user in a first-party or third-party segment.

**Keyword**: `segment[ID]` where `ID` is the segment ID. Use [Segment Service](../digital-platform-api/segment-service.md) to retrieve segment IDs.

**Attribute**: None

**Operator**: None for presence, `not` for absence.

**Value**: None

**Example**:

```
if any segment[12345], segment[23456], segment[34567]:
5
elif any segment[76543], segment[65432], segment[54321]:
3
elif not segment[9999]:
1
else:
0.2
```

#### Segment age

Evaluate impressions based on the minutes since the user was added to a first-party or third-party segment.

> [!NOTE]
> If the user is not in the segment, this feature evaluates to `False`.

**Keyword**: `segment[ID]` where `ID` is the segment ID. Use [Segment Service](../digital-platform-api/segment-service.md) to retrieve segment IDs.

**Attribute**: `.age`

**Operator**: `<` , `>` , or `=`

**Value**: Positive integer representing the minutes since the user was added to the segment.

**Example**:

```
if segment[12345].age < 5:
2
else:
0.2
```

#### Segment value

Evaluate impressions based on a user-defined value. The value may be passed in a number of ways, for example, through the Batch Segment Service or a first-party or third-party segment query string. For more information on passing values through segment query strings, see [Segment Pixels Advanced](../invest/segment-pixels-advanced.md) in documentation.

> [!NOTE]
> If the user is not in the segment, this feature evaluates to `False`.

**Keyword**: `segment[ID]` where `ID` is the segment ID. Use [Segment Service](../digital-platform-api/segment-service.md) to retrieve segment IDs.

**Attribute**: `.value`

**Operator**: `<`, `>`, or `=`

**Value**: Non-zero, positive integer representing the user-defined value.

**Example**:

```
if segment[12345].value = 5:
2
else:
0.2
```

### Frequency/Recency

- [Frequency Presence/Absence](#frequency-presenceabsence)
- [Lifetime Frequency](#lifetime-frequency)
- [Daily Frequency](#daily-frequency)
- [Recency Presence/Absence and Data](#recency-presenceabsence-and-data)

#### Frequency presence/absence

Evaluate whether or not frequency data is available for the user. This can be determined for all ads under an advertiser, line item, or
campaign.

**Keyword**: `frequency`

**Attribute**: `OBJECT[ID].` where `OBJECT` is `advertiser`, `line_item`, or `campaign`, and `ID` is the object ID. Use the [Advertiser Service](../digital-platform-api/advertiser-service.md), [Line Item Service](../digital-platform-api/line-item-service.md), or [Campaign Service](../digital-platform-api/campaign-service.md) to retrieve IDs.

**Operator**: `<` , `>` , or `=`

**Value**: `0` indicates that the user has never seen an impression for this object; a positive integer indicates that frequency information is available.

> [!NOTE]
> Unlike recency, frequency data is never null. If a user has never seen an impression for this object, frequency is `0`.

**Example**:

```
if line_item[15].frequency > 0:
2
elif campaign[20].frequency > 0:
1.5
elif campaign[23].frequency > 0:
1
else:
0.1
```

#### Lifetime frequency

Evaluate impressions based on the number of ads seen by a user over the lifetime of an advertiser, line item, or campaign.  

**Keyword**: `lifetime_frequency`

**Attribute**: `OBJECT[ID].` where `OBJECT` is `advertiser`, `line_item`, or `campaign`, or `creative`, and `ID` is the object ID. Use the [Advertiser Service](../digital-platform-api/advertiser-service.md), [Line Item Service](../digital-platform-api/line-item-service.md), or [Campaign Service](../digital-platform-api/campaign-service.md) to retrieve IDs.

**Operator**: `=<`, `<=`, `presence/absence`, `in`, `comparison`, `not`, and `range`.

**Value**: Positive integer representing the number of ads seen by a user over the lifetime of the object. `0` indicates no frequency information is available (the user has never seen this object).

**Example**:

```
if campaign[20].lifetime_frequency < 2:
5
elif advertiser[12].lifetime_frequency < 10:
4
elif advertiser[12].lifetime_frequency < 20:
2
else:
0.1
```

#### Daily frequency

Evaluate impressions based on the number of impressions seen by a user on the current day. This can be determined for an advertiser, line item, or campaign.  

**Keyword**: `day_frequency`

**Attribute**: `OBJECT[ID].` where `OBJECT` is `advertiser`, `line_item`, or `campaign`, and `ID` is the object ID. Use the [Advertiser Service](../digital-platform-api/advertiser-service.md), [Line Item Service](../digital-platform-api/line-item-service.md), or [Campaign Service](../digital-platform-api/campaign-service.md) to retrieve IDs.

**Operator**: `=<`, `<=`, `presence/absence`, `in`, `comparison`, `not`, and `range`.

**Value**: Positive integer representing the number of ads seen by a user on the current day. `0` indicates no frequency information is available (the user has not seen this object on the current day).

**Example**:

```
if campaign[20].day_frequency < 2:
5
elif advertiser[12].day_frequency < 10:
4
elif advertiser[12].day_frequency < 20:
2
else:
0.1
```

#### Recency presence/absence and data

Evaluates whether recency data is available for a user, and, if available, the number of minutes since a user has seen an ad. This can be determined for a user for all ads under an advertiser, line item, or campaign.

**Keyword**: `recency`

**Attribute**: `OBJECT[ID].` where `OBJECT` is `advertiser`, `line_item`, or `campaign`, and `ID` is the object ID. Use the [Advertiser Service](../digital-platform-api/advertiser-service.md), [Line Item Service](../digital-platform-api/line-item-service.md), or [Campaign Service](../digital-platform-api/campaign-service.md) to retrieve IDs.

**Operator**: `=<`, `<=`, `presence/absence`, `in`, `comparison`, `not`, and `range`.

**Value**: A positive integer indicating the number of minutes since a user has seen an impression, rounded down. 59 seconds will evaluate to `0`, 61 seconds will evaluate to 1. `0` means the impression was seen very recently. `Null` means no recency data is available (the user has not seen this impression before).

**Example**:

```
if not advertiser.recency:
0.1
elif advertiser[3].recency > 60:
1
else:
0.2
```

### Examples of compound feature syntax using multiple attributes

#### Example of multiple segment attributes

```
# This tree determines a bid price as follows:
# 1. If the user is in segment 3 and has a value greater than 1 or has been in the segment for 5 minutes, bid $1.
# 2. Otherwise, bid $2.
if any segment[3].value > 1, segment[3].age = 5:
    1.0
else:
    2.0  
```

#### Example of recency/frequency syntax with multiple attributes

```
# This tree determines a bid price as follows:
# 1. If there's no recency data for this user related to ads in line item 3, bid $1.
# 2. If the user has seen an ad in line item 3 more than 5 minutes ago and the user has seen an ad in campaign 2 less than four times today, bid $3.
#3. If the user has seen an ad in line item 1 more than 5 times ever or more than 4 times today, or if the user has seen an ad in advertiser 2 more than 4 times today, bid $0.50.
#4. Otherwise, bid nothing.
if not line_item[3].recency: 
        1
elif every line_item[3].recency > 5, campaign[2].day_frequency < 4: 
        3 
elif any line_item[1].lifetime_frequency > 5, line_item[1].day_frequency > 4, advertiser[2].day_frequency > 4: 
        0.50 
else: 
        0  
```

#### Example of multiple compound attributes

```
# This tree determines a bid price as follows:
# 1. If this user is in segment 3 and has a value greater than 1 or has been in the segment for 5 minutes, bid $1.
# 2. If the user has seen an ad in line item 3 more than 5 minutes ago and an ad in campaign 2 less than four times today, bid $3.
# 3. If the user has seen an ad in line item 1 more than 5 times ever or more than 4 times today, or if the user has seen an ad in advertiser 2 more than 4 times today, bid $0.50.
# 4. Otherwise, bid nothing.
if any segment[3].value > 1, segment[3].age = 5:
    1
elif every line_item[3].recency > 5, campaign[2].day_frequency < 4: 
        3 
elif any line_item[1].lifetime_frequency > 5, line_item[1].day_frequency > 4, advertiser[2].day_frequency > 4: 
        0.50 
else: 
        0  
```
