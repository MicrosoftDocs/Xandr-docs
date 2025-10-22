---
title: User Verification Service
description: Use the User Verification service to ensure that the accurate (paying) customer is logging into the App.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# User Verification service

App providers can use the User Verification service to confirm that the correct (paying) customer is signing in to the App. This confirmation takes place via two steps:

1. The API makes a `POST` call to generate a verification token when the user launches an app within. Verification tokens expire after two minutes for security purposes.
1. The app makes a `GET` call using the verification token that is sent by Xandr when the app is launched to retrieve the user's ID. Once the verification token is used to return a user ID, the token is deleted for security purposes.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | [https://api.appnexus.com/user-verification](https://api.appnexus.com/user-verification) | Create a new verification token. |
| `GET` | [https://api.appnexus.com/user-verification?user_token=USER_TOKEN](https://api.appnexus.com/user-verification?user_token=USER_TOKEN) | Retrieve the user ID associated with a verification token. |

## JSON fields

| Field | Type | Description |
|:---|:---|:---|
| `user_id` | int | The ID of the user that generated the `user_token` on `POST`. |
| `user_token` | string | The authentication token that can be used to retrieve a user's ID. |

## Examples

### Create a new verification token

```
$ curl -b cookies -c cookies -X POST 'https://api.adnxs.com/user-verification'
{
  "response": {
    "status": "OK",
    "user_token": "3e3088b48c901a6b26dc95e530bc5a8c96b8f7e4d6ba46cf"
  }
}
```

### Retrieve the user ID associated with a token

```
$ curl -b cookies -c cookies 'https://api.adnxs.com/user-verification?user_token=3e3088b48c901a6b26dc95e530bc5a8c96b8f7e4d6ba46cf'
{
  "response": {
    "status": "OK",
    "user_id": 110,
  }
}
```
