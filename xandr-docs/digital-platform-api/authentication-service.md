---
title: Digital Platform API - Authentication Process
description: In this article, find information about the Authentication service and step-by-step instructions for the authentication process. 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Authentication process

Before you can make calls to any of the Digital Platform API services or reports, you must use your username and password to get an authorization token. The token remains active for 2 hours, during which you do not need to re-authenticate. Furthermore, there is a 24-hour hard expiry. When an API session reaches the 24 hour mark, regardless of when the most recent API call was made, that session will expire.

This page walks you through the authentication process.

> [!NOTE]
>
> - For an explanation of the errors that you may encounter during and after authentication, see [Error Messages](api-semantics.md#error-messages).
> - If your username and password do not grant you access to the API, please refer to the [API Onboarding Process](api-onboarding-process.md) or contact your Xandr representative.
> - If you have forgotten your username or password, you can use the [Account Recovery Service](account-recovery-service.md) to retrieve your username or create a new password.

## Step 1. Create a JSON file including your username and password

Below, we have used the `cat` command to show the output of the file.

```
$ cat auth
{
    "auth": {
        "username" : "USERNAME",
        "password" : "PASSWORD"
    }
}
```

### Guidelines for creating your password

When creating your password, please create a complex password with the following:

- 10 or more characters
- 64 or fewer characters
- At least one capital letter (A–Z)
- At least one lowercase letter (a–z)
- At least one digit (0–9)
- At least one special character (such as #, $, ? %, &)

## Step 2. `POST` the file to the authentication service

The request returns a token that remains valid for the 2 hours following your most recent call to the API. We suggest using "`-b cookies -c cookies`" in the `POST` request to store the token in a cookie.

```
$ curl -b cookies -c cookies -X POST -d @auth 'https://api.appnexus.com/auth'
{
    "response": {
        "status": "OK",
        "token": "h20hbtptiv3vlp1rkm3ve1qig0",
        "dbg_info": {
            ...
        }
    }
}
```

## Step 3. Use the token when making calls to API services and reports

In the example below, we call the [Member Service](member-service.md) and authenticate using the token stored in the cookie.

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/member'
{
    "response": {
        "members": [
            {
                "id": "1",
                "name": "Car company c\/o Ad Agency",
                "active": "1",
                "bidder_id": "2"
            }
        ]
    }
}
```

Alternately, if you didn't store the token in a cookie, you can put the token in the request header as `"Authorization: TOKEN"`.

```
$ curl -H "Authorization: 622cee5f8c99c81e87614e9efc63eddb" 'https://api.appnexus.com/member'
{
    "response": {
        "members": [
            {
                "id": "1",
                "name": "Member 1",
                "active": "1",
                "bidder_id": "2"
            }
        ]
    }
}
```

> [!NOTE]
> For added security, it's also possible to authenticate using JSON Web Tokens. See [Token-Based API Authentication](token-based-api-authentication.md) for more information.

## Authentication frequency

After authenticating, your token remains valid for 2 hours. You do not need to re-authenticate within this time. If you do re-authenticate, please note the following limitation:
The API permits you to authenticate successfully 10 times per 5-minute period. Any subsequent authentication attempts within those 5 minutes will result in an error.

> [!TIP]
> It is best practice to listen for the `"NOAUTH"` `error_id` in your call responses and re-authenticate only after receiving it.

## Related topics

- [Account Recovery Service](account-recovery-service.md)
- [API Best Practices](api-best-practices.md)
- [API Usage Constraints](api-usage-constraints.md)
- [API Semantics](api-semantics.md)
