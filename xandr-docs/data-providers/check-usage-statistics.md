---
title: Data Providers - Check Usage Statistics
description: The statistics are deduplicated per request made to the service. This page explains about the fields that can be set in the query string when making a call to the API to retrieve statistics.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-providers
ms.author: shsrinivasan
---


# Data Providers - Check usage statistics

> [!NOTE]
> This field or feature is part of functionality currently in either Alpha or Beta phase. It is therefore subject to change.

## REST API call

When making a call to the API to retrieve statistics, the following fields can be set in the query string:

- `agg` can be omitted in order to obtain an hourly/detailed report.
- `agg=true` can be used to obtain an aggregated report.
- `start` date should be set in the following format: `2015-11-01+01:00:00.`
- `end` date should be set in the following format: `2015-12-01+01:00:00.`
  
  ``` 
  curl -H "Authorization: hbapi:123456:9876abcd54321:nym2" -X GET "https://streaming-data.appnexus.com/rt-segment-processed?member_id=100&start=2014-05-22+00:00:00&end=2014-05-22+01:00:00"
  ```

The statistics are deduplicated per request made to the service. For example, if the same user is added to the same segment in three different requests, `num_valid_adds` and `num_valid_users` would show "3". When using `agg=true`, there will be one entry in the report property of the response. It will be an aggregation of all usage statistics in the date range that's specified. `error_log_lines` and `segment_log_lines` will be empty, and the processed hour will be for the last hour in the date range that's specified. However, if no date range is specified, the report will show the data from the last two weeks.

**Ex: Aggregated usage report**

``` 
{
    "response": {
        "report": {
            "error_log_lines": null,
            "match_rate": 87.7,
            "member_id": 123,
            "num_inactive_segments": 0,
            "num_invalid_segments": 0,
            "num_invalid_users": 25,
            "num_other_errors": 0,
            "num_unauth_segments": 0,
            "num_valid_adds": 181,
            "num_valid_removes": 2,
            "num_valid_users": 179,
            "processed_hour": "2015-11-08 01:00:00",
            "segment_log_lines": null
        },
        "status": "OK"
    }
}
```

**Ex: Hourly report**

``` 
{
    "response": {
        "report": [
            {
                "error_log_lines": "",
                "match_rate": 100.0,
                "member_id": 123,
                "num_inactive_segments": 0,
                "num_invalid_segments": 0,
                "num_invalid_users": 0,
                "num_other_errors": 0,
                "num_unauth_segments": 0,
                "num_valid_adds": 2,
                "num_valid_removes": 0,
                "num_valid_users": 1,
                "processed_hour": "2015-11-03 18:00:00",
                "segment_log_lines": "Valid users: 1580557697843484206
Valid segments (id, code, segment owner member id): (3737552, 'segment_3737552', 123), (3737547, 'segment_3737547', 123)
Valid additions (user id, segment id, expiration): (1580557697843484206, 3737552, 1440), (1580557697843484206, 3737547, 1440)"
            },
            {
                "error_log_lines": "Inactive users: 15805576978434842
Inactive segments (id, code, segment owner member id): (321456, 'segment_312456', 123)
Invalid segments (id, code, segment owner member id): (0, 'segment_654321', 123)
Unauthorized segments (id, code, segment owner member id): (0, 'segment_123456', 123)",
                "match_rate": 50.0,
                "member_id": 123,
                "num_inactive_segments": 1,
                "num_invalid_segments": 1,
                "num_invalid_users": 1,
                "num_other_errors": 0,
                "num_unauth_segments": 1,
                "num_valid_adds": 0,
                "num_valid_removes": 2,
                "num_valid_users": 1,
                "processed_hour": "2015-11-03 19:00:00",
                "segment_log_lines": "Valid users: 1580557697843484206
Valid segments (id, code, segment owner member id): (3737552, 'segment_3737552', 123), (3737547, 'segment_3737547', 123)
Valid removals (user id, segment id, expiration): (1580557697843484206, 3737552, -1), (1580557697843484206, 3737547, -1)"
            }
        ]
    }
}
```

## Report object JSON (for objects in report array)

| Field name | Description | Example value |
|--|--|--|
| `error_log_lines` | An updating 200 line sample of the errors that prevented the user and segment associations from being successful. | `"Inactive users: 15805576978434842 Inactive segments (id, code, segment owner member id): (321456, 'segment_312456', 123) Invalid segments (id, code, segment owner member id): (0, 'segment_654321', 123) Unauthorized segments (id, code, segment owner member id): (0, 'segment_123456', 123)"` |
| `match_rate` | The percentage of valid users uploaded (num_valid_users/(num_valid_users+num_invalid_users)). | 75.00 |
| `num_inactive_segments` | Total number of associations that failed due to attempting to access inactive segments. | 200 |
| `num_invalid_segments` | Total number of associations that failed due to attempting to access invalid segments. | 3 |
| `num_invalid_users` | Total number of users that were in requests, but do not exist on Xandr's platform. | 4000 |
| `num_other_errors` | Total number of failed calls for other reasons. | 0 |
| `num_unauth_segments` | Total number of associations that failed due to attempting to access unauthorized segments. | 500 |
| `num_valid_adds` | Total number of associations that were added (that is, user-segment pairs, expiration !=-1). | 98765432 |
| `num_valid_removes` | Total number of associations that were removed (that is, user-segment pairs with expiration = -1). | 98765432 |
| `num_valid_users` | Total number of valid users that were streamed through the service. This is NOT the number of unique users for the hour. | 124578 |
| `processed_hour` | Hour during which uploads went through. | `"2014-05-22 00:00:00"` |
| `segment_log_lines` | An updating 200 line sample of the segments and the number of valid associations for each. | `"Valid users: 1580557697843484206 Valid segments (id, code, segment owner member id): (3737552, 'segment_3737552', 123), (3737547, 'segment_3737547', 123) Valid additions (user id, segment id, expiration): (1580557697843484206, 3737552, 1440), (1580557697843484206, 3737547, 1440) Valid removals (user id, segment id, expiration): (1580557697843484206, 3737552, -1), (1580557697843484206, 3737547, -1)"` |

## Related topics

- [Streaming Server-Side Segmentation](../digital-platform-api/streaming-server-side-segmentation.md)
- [Instant Audience Service](../digital-platform-api/instant-audience-service.md)