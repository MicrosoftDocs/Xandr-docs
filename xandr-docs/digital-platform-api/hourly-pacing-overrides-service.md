---
title: Hourly Pacing Overrides Service
description: Use the Hourly Pacing Overrides service to customize your line item's budget distribution within a day.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Hourly Pacing Overrides service

The Hourly Pacing Overrides Service is used to customize your line item's budget distribution within a day. This can be set for specific days of the week or specific dates. Through this API service, you can create an individual pacing strategy (custom spend curve) to define and alter line item pacing for a particular date or day of the week. You can also create multiple pacing strategies through this API service to further customize pacing for multiple dates or days of the week.

## RETS API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `GET` | `https://api.appnexus.com/pacing-strategy?line_item_id=LINE_ITEM_ID_1,LINE_ITEM_ID_2` | View pacing strategies for one or more line items. |
| `PUT` |`https://api.appnexus.com/pacing-strategy?line_item_id=LINE_ITEM_ID` | Add a pacing strategy for a single line item. |
| `PUT` | `https://api.appnexus.com/pacing-strategy?line_item_id=LINE_ITEM_ID` | Modify an existing pacing strategy. |
| `DELETE` | `https://api.appnexus.com/pacing-strategy?line_item_id=LINE_ITEM_ID&when=WHEN` | Delete a pacing strategy. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `line_item_id` | int | The ID of the line item. <br>**Required On**: `GET`, `PUT`, and `DELETE`. |
| `pacing_strategies` | array of objects | The pacing strategies associated with the line item. The `pacing_strategies` object array is defined in the table below. <br>**Required On**: `PUT` |

### Pacing strategies

The `pacing_strategies` object is used to define a customized pacing strategy for your line item. You're able to customize pacing within a single day and within a single hour.

| Field | Type | Description |
|:---|:---|:---|
| `pacing_weights` | object | Fields in this object determine how much to spend per hour for custom strategies. Weights are defined as a proportion of the line item's daily budget. Twenty-four fields are available, one for each hour of the day. Possible hourly weight values are between 0 to 100, and the weight allocations across all hours **must** equal 100. See [example](#example-for-pacing_weights).<br><br>**Default**: `null`<br>**Required On**: `PUT` |
| `strategy_type` | string | Indicates how the line item paces within a single day. Possible values are:<br> - `asap`: Spend your daily budget as fast as possible.<br> - `custom`: Define the amount you want to spend per hour using weights. **Note**: Weights are defined as a proportion of the line item's daily budget.<br>- `intelligent`: Optimally spend your daily budget based on Xandr market dynamics.<br><br>If Daypart Targets (see `daypart_targets` in [Profile Service](./profile-service.md)) are set on the line item profile, your pacing strategy will automatically adapt to the eligible hours.<br><br>**Default**: N/A<br>**Required On**: `PUT` |
| `when` | string | When the pacing strategy should be active. Possible values are:<br> - `always`<br>A single day of the week: `sunday`, `monday`, `tuesday`, `wednesday`, `thursday`, `friday`, or `saturday`.<br>A single date (`"YYYY-MM-DD"`, **for example**: `"2019-09-01"`).<br><br>**Default**: N/A<br>**Required On**: `PUT` |

#### Example for `pacing_weights`

```
[
{
"line_item_id": 13827815,
"pacing_strategies": [
{
"strategy_type": "custom",
"when": "2021-01-22",
"pacing_weights": {
"0": 1.67,
"1": 1.33,
"2": 1.21,
"3": 1.25,
"4": 1.57,
"5": 2.33,
"6": 3.18,
"7": 4.05,
"8": 4.76,
"9": 5,
"10": 5.22,
"11": 4.95,
"12": 5.09,
"13": 5.12,
"14": 5.23,
"15": 5.26,
"16": 5.67,
"17": 5.99,
"18": 5.92,
"19": 6.26,
"20": 6.58,
"21": 5.69,
"22": 4,
"23": 2.67
}
}
]
}
]
```

### File upload method

You may also read or write pacing strategies using a .csv file.

> [!NOTE]
> Excel automatically formats dates as MM/DD/YYYY. When writing values to the .csv file's **when** column, the Pacing Strategy Service expects dates in the YYYY-MM-DD format.

| line_item_id | strategy_type | when | hour | weight |
|:---|:---|:---|:---|:---|
| 1234567 | intelligent | always |  |  |
| 2931292 | intelligent | always |  |  |
| 2931292 | custom | 2019-09-01 | 0 | 33.3 |
| 2931292 | custom | 2019-09-01 | 1 | 33.35 |
| 2931292 | custom | 2019-09-01 | 2 | 33.35 |
| 8123952 | asap | always |  |  |
| 8123952 | custom | monday | 0 | 33.35 |
| 8123952 | custom | monday | 1 | 33.35 |
| 8123952 | custom | monday | 2 | 33.3 |

## Examples

### View a line item's pacing strategy details

```
$ curl -b cookies -c cookies -X GET -H 'Accept: application/json' "https://api.appnexus.com/pacing-strategy?line_item_id=1234567"
 
 
[
    {
        "line_item_id": 1234567,
        "pacing_strategies": [
            {
                "strategy_type": "intelligent",
                "when": "always"
            }
        ]
    }
]
```

### View multiple line items' pacing strategy details

```
$ curl -b cookies -c cookies -X GET -H 'Accept: application/json' "https://api.appnexus.com/pacing-strategy?line_item_id=1234567,2345678"
 
 
[
    {
        "line_item_id": 1234567,
        "pacing_strategies": [
            {
                "strategy_type": "intelligent",
                "when": "always"
            }
        ]
    },
    {
        "line_item_id": 2345678,
        "pacing_strategies": [
            {
                "strategy_type": "intelligent",
                "when": "always"
            },
            {
                "strategy_type": "custom",
                "when": "2019-12-30",
                "pacing_weights": {
                    "0": 1.67,
                    "1": 1.33,
                    "2": 1.21,
                    "3": 1.25,
                    "4": 1.57,
                    "5": 2.33,
                    "6": 3.18,
                    "7": 4.05,
                    "8": 4.76,
                    "9": 5,
                    "10": 5.22,
                    "11": 4.95,
                    "12": 5.09,
                    "13": 5.12,
                    "14": 5.23,
                    "15": 5.26,
                    "16": 5.67,
                    "17": 5.99,
                    "18": 5.92,
                    "19": 6.26,
                    "20": 6.58,
                    "21": 5.69,
                    "22": 4,
                    "23": 2.67
                }
            }
        ]
    }
]
```

### Always deliver ASAP

```
$ cat always_asap.json
[
  {
    "line_item_id": 1234567,
    "pacing_strategies": [
      {
        "strategy_type": "asap",
        "when": "always"
      }
    ]
  }
]
 
 
$ curl -b cookies -c cookies -X PUT -H 'Content-Type: application/json' -d @always_asap.json "https://api.appnexus.com/pacing-strategy?line_item_id=1234567"
```

### Use a custom pacing strategy on a single date

```
$ cat custom_date.json

[{
    "line_item_id": 1234567,
    "pacing_strategies": [{
        "strategy_type": "custom",
        "when": "2019-12-15",
        "pacing_weights": {
            "0": 1.67,
            "1": 1.33,
            "2": 1.21,
            "3": 1.25,
            "4": 1.57,
            "5": 2.33,
            "6": 3.18,
            "7": 4.05,
            "8": 4.76,
            "9": 5,
            "10": 5.22,
            "11": 4.95,
            "12": 5.09,
            "13": 5.12,
            "14": 5.23,
            "15": 5.26,
            "16": 5.67,
            "17": 5.99,
            "18": 5.92,
            "19": 6.26,
            "20": 6.58,
            "21": 5.69,
            "22": 4,
            "23": 2.67
        }
    }]
}]
 $ curl -b cookies -c cookies -X PUT -H 'Content-Type: application/json' -d @custom_date.json "https://api.appnexus.com/pacing-strategy?line_item_id=1234567"
```

### Use a custom pacing strategy on a particular day of the week

```
$ cat custom_dow.json

[{
    "line_item_id": 1234567,
    "pacing_strategies": [{
        "strategy_type": "custom",
        "when": "tuesday",
        "pacing_weights": {
            "0": 1.67,
            "1": 1.33,
            "2": 1.21,
            "3": 1.25,
            "4": 1.57,
            "5": 2.33,
            "6": 3.18,
            "7": 4.05,
            "8": 4.76,
            "9": 5,
            "10": 5.22,
            "11": 4.95,
            "12": 5.09,
            "13": 5.12,
            "14": 5.23,
            "15": 5.26,
            "16": 5.67,
            "17": 5.99,
            "18": 5.92,
            "19": 6.26,
            "20": 6.58,
            "21": 5.69,
            "22": 4,
            "23": 2.67
        }
    }]
}]
 
$ curl -b cookies -c cookies -X PUT -H 'Content-Type: application/json' -d @custom_dow.json "https://api.appnexus.com/pacing-strategy?line_item_id=1234567"
```

### Deliver ASAP on a particular day of the week

```
$ cat asap_date.json
[
 {
    "line_item_id": 1234567,
    "pacing_strategies": [
      {
        "strategy_type": "asap",
        "when": "2019-12-15"
      }
    ]
  }
]
 
 
$ curl -b cookies -c cookies -X PUT -H 'Content-Type: application/json' -d @asap_date.json "https://api.appnexus.com/pacing-strategy?line_item_id=1234567"
(no JSON response, just HTTP 200 OK)
```

### Define multiple pacing strategies for multiple line items

```
$ cat multiple_strategies.json

[{
        "line_item_id": 1234567,
        "pacing_strategies": [{
                "strategy_type": "asap",
                "when": "2019-12-31"
            },
            {
                "strategy_type": "custom",
                "when": "monday",
                "pacing_weights": {
                    "0": 1.67,
                    "1": 1.33,
                    "2": 1.21,
                    "3": 1.25,
                    "4": 1.57,
                    "5": 2.33,
                    "6": 3.18,
                    "7": 4.05,
                    "8": 4.76,
                    "9": 5,
                    "10": 5.22,
                    "11": 4.95,
                    "12": 5.09,
                    "13": 5.12,
                    "14": 5.23,
                    "15": 5.26,
                    "16": 5.67,
                    "17": 5.99,
                    "18": 5.92,
                    "19": 6.26,
                    "20": 6.58,
                    "21": 5.69,
                    "22": 4,
                    "23": 2.67
                }
            }
        ]
    },
    {
        "line_item_id": 2345678,
        "pacing_strategies": [{
                "strategy_type": "asap",
                "when": "always"
            },
            {
                "strategy_type": "custom",
                "when": "2019-12-31",
                "pacing_weights": {
                    "0": 1.67,
                    "1": 1.33,
                    "2": 1.21,
                    "3": 1.25,
                    "4": 1.57,
                    "5": 2.33,
                    "6": 3.18,
                    "7": 4.05,
                    "8": 4.76,
                    "9": 5,
                    "10": 5.22,
                    "11": 4.95,
                    "12": 5.09,
                    "13": 5.12,
                    "14": 5.23,
                    "15": 5.26,
                    "16": 5.67,
                    "17": 5.99,
                    "18": 5.92,
                    "19": 6.26,
                    "20": 6.58,
                    "21": 5.69,
                    "22": 4,
                    "23": 2.67
                }
            }
        ]
    }
]
 
$ curl -b cookies -c cookies -X PUT -H 'Content-Type: application/json' -d @multiple_strategies.json "https://api.appnexus.com/pacing-strategy?line_item_id=1234567&line_item_id=2345678"
```

### Define multiple pacing strategies for multiple line items using a `.csv` file

```
$ cat custom_spend_strategies.csv
line_item_id,strategy_type,when,hour,weight
1234567,asap,monday,,
1234567,custom,2022-12-25,0,4
1234567,custom,2022-12-25,1,4
1234567,custom,2022-12-25,2,4
1234567,custom,2022-12-25,3,4
1234567,custom,2022-12-25,4,4
1234567,custom,2022-12-25,5,5
1234567,custom,2022-12-25,6,4
1234567,custom,2022-12-25,7,4
1234567,custom,2022-12-25,8,4
1234567,custom,2022-12-25,9,4
1234567,custom,2022-12-25,10,4
1234567,custom,2022-12-25,11,5
1234567,custom,2022-12-25,12,4
1234567,custom,2022-12-25,13,4
1234567,custom,2022-12-25,14,4
1234567,custom,2022-12-25,15,4
1234567,custom,2022-12-25,16,4
1234567,custom,2022-12-25,17,5
1234567,custom,2022-12-25,18,4
1234567,custom,2022-12-25,19,4
1234567,custom,2022-12-25,20,4
1234567,custom,2022-12-25,21,4
1234567,custom,2022-12-25,22,4
1234567,custom,2022-12-25,23,5
2345678,asap,always,,
2345678,custom,2022-12-25,0,0
2345678,custom,2022-12-25,1,0
2345678,custom,2022-12-25,2,0
2345678,custom,2022-12-25,3,0
2345678,custom,2022-12-25,4,9
2345678,custom,2022-12-25,5,4
2345678,custom,2022-12-25,6,4
2345678,custom,2022-12-25,7,4
2345678,custom,2022-12-25,8,4
2345678,custom,2022-12-25,9,9
2345678,custom,2022-12-25,10,4
2345678,custom,2022-12-25,11,4
2345678,custom,2022-12-25,12,4
2345678,custom,2022-12-25,13,4
2345678,custom,2022-12-25,14,9
2345678,custom,2022-12-25,15,4
2345678,custom,2022-12-25,16,4
2345678,custom,2022-12-25,17,4
2345678,custom,2022-12-25,18,4
2345678,custom,2022-12-25,19,9
2345678,custom,2022-12-25,20,4
2345678,custom,2022-12-25,21,4
2345678,custom,2022-12-25,22,4
2345678,custom,2022-12-25,23,4
 
$ curl -b cookies -c cookies -X PUT -H 'Content-Type: text/csv' -H 'Accept: application/json' --data-binary '@custom_spend_strategies.csv' 'https://api.appnexus.com/pacing-strategy/upload-csv'
```

### Delete a line item's pacing strategy

```
$ curl -b cookies -c cookies -X DELETE -H 'Accept: application/json' "https://api.appnexus.com/pacing-strategy?line_item_id=1234567&when=always"

{
    "line_item_id": 1234567,
    "pacing_strategies": [
    {
        "strategy_type": "asap",
        "when": "always"
    }
  ]
}

$ curl -b cookies -c cookies -X DELETE -H 'Accept: application/json' "https://api.appnexus.com/pacing-strategy?line_item_id=1234567&when=2019-12-31"

{
    "line_item_id": 1234567,
    "pacing_strategies": [{
        "strategy_type": "custom",
        "when": "2019-12-31",
        "pacing_weights": {
            "0": 1.67,
            "1": 1.33,
            "2": 1.21,
            "3": 1.25,
            "4": 1.57,
            "5": 2.33,
            "6": 3.18,
            "7": 4.05,
            "8": 4.76,
            "9": 5,
            "10": 5.22,
            "11": 4.95,
            "12": 5.09,
            "13": 5.12,
            "14": 5.23,
            "15": 5.26,
            "16": 5.67,
            "17": 5.99,
            "18": 5.92,
            "19": 6.26,
            "20": 6.58,
            "21": 5.69,
            "22": 4,
            "23": 2.67
        }
    }]
}
```

## Related topics

- [API Best Practices](./api-best-practices.md)
- [API Semantics](./api-semantics.md)
- [Line Item (ALI) Service](./line-item-service---ali.md)
- [Insertion Order Service](./insertion-order-service.md)
