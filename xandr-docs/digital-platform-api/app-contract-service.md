---
title: App Contract Service
description: Use the App Contract service to record or update client contracts. It can only be accessed by sales ops.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# App Contract service

> [!NOTE]
> This service is currently available to a limited set of clients and Microsoft employees only.

This is an admin-only service that allows Xandr personnel to record or update client contracts. It can only be accessed by sales ops.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/app-contract`<br>(app contract JSON) | Add a contract |
| `GET` | `https://api.appnexus.com/app-contract` | View all contracts |
| `GET` | `https://api.appnexus.com/app-contract?id=ID` | View a specific contract |
| `DELETE` | `https://api.appnexus.com/app-contract?id=ID` | Delete a contract |
| `GET` | `https://api.appnexus.com/app-contract/meta` | Find out which fields you can filter and sort by. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `id` | int | The unique ID associated with the app contract.<br>**Required On**: `PUT` and `DELETE`, in query string. |
| `plugin_id` | int | The plugin (app) to which this contract is associated.<br>**Required On**: `POST` |
| `terms` | int    | The number of days Xandr has between receipt of payment from a subscriber and the delivery of payment to the developer.<br>**Default**: `null` |
| `revshare_pct`  | double | The shared revenue percentage.<br>**Default**: `0.00` |
| `log_level_data_fee` | double | The fee charged for the use of log-level data.<br>**Default**: `null` |
| `start_date` | timestamp | The start date of the app contract.<br>**Required On**: `POST` |
| `end_date` | timestamp | The end date of the app contract.<br>**Default**: `null`  |
| `active` | boolean | Indicates whether this contract is currently in effect.<br>**Default**: `true` |

## Validations

- The `plugin_id` must be a valid one from the plugin service.
- The `terms` must be between `0` and `(2^31)-1`.
- The `revshare_pct` must be between `0.00` and `100.00`.
- The `log_level_data_fee` must be of scale 2 and between `0.00` and `999999999.99`.
- Both the `start_date` and `end_date` must be valid time stamps (i.e., `2013-01-01 00:00:00`).
- The `end_date` must be greater or equal to the `start_date`.
- Only one (1) active app contract per `plugin_id` is allowed.
