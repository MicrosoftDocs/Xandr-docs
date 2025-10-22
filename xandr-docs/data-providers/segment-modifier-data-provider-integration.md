---
title: Segment Modifier Data Provider Integration
description: In this article, learn how to do a server-side integration for a segment modifier.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-providers
ms.author: shsrinivasan
---

# Segment modifier data provider integration

In order to take full advantage of Segment Modifier's capabilities, it can be useful to do a server-side integration.

Server-side integrations allow for near-realtime updates to modifier values. This can be useful if your model requires a fast response time or is updated frequently. Additionally, you can tailor your modifier based on the attributes available via the macros listed in [Real Time Data Integration Instructions](real-time-data-integration-instructions.md).

1. Build an application in the Xandr cloud. The application should respond to an HTTP request with a line-delimited list of segment codes and their corresponding segment values. For example, if your application is located at DNS location `test-location.nym1`, we can send you an HTTP request like the following:

    ```
    test-location.nym1?an_user_id=123
    ```

    where `an_user_id=123` corresponds to the Xandr ID for user 123. (For more information, see [User ID Mapping](../supply-partners/user-id-mapping.md).)

1. Send a response from your application with a list of segment codes and values such as:

    ```
    CS_MODIFIER_001:9000
    CS_MODIFIER_002:8000
    ```

    where the code and value are separated by a colon and correspond to the audience segment and modifier amount, respectively.

1. Using [Campaign Service](../digital-platform-api/campaign-service.md) API, set the modifier segment ID such that it corresponds to the segment codes being returned by your web service.

## Related topic

[Segment Modifier](segment-modifier.md)
