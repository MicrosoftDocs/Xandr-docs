---
title: Yield Analytics API - Authentication Process
description: This page walks you through the authentication process for the Yield Analytics API.
ms.date: 02/11/2026
ms.service: publisher-monetization
ms.subservice: yield-analytics-api
ms.author: shsrinivasan
---

# Yield Analytics API - Authentication process

This page walks you through the authentication process:

- Authentication is required before accessing any API services. The IMF APIs expose application data securely and are available only to authenticated users over secure transport protocols. 
- Before calling any IMF API endpoints, you must authenticate using your platform username and password through the authentication service at: `https://api.appnexus.com/auth`.
- A successful authentication request returns an authorization token that is valid for two hours. This token can then be used to make requests to all endpoints under: `https://api.appnexus.com/imf`.
- Re-authentication is not required while the token remains valid. 
- For convenience, we recommend storing the authorization token in a cookie by using the `-b cookies -c cookies` options in your authentication request. This ensures the token is automatically included in all subsequent API calls. 

> [!NOTE]
> The authentication username and password are the same credentials used for the Digital Platform API and/or Microsoft Monetize. 

 
> [!TIP] 
> If you have forgotten your username or password, you can use the Account Recovery Service to retrieve your username or create a new password.


## Step 1. Create a JSON-formatted file including your username and password

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

The request returns a token that remains valid for 2 hours. We suggest using `"-b cookies -c cookies"` in the POST request to store the token in a cookie. 


```
$ curl -b cookies -c cookies -X POST -d @auth 'https://api.appnexus.com/auth'
{
    "response": {
        "status": "OK",
        "token": "h3vlp0122344",
        "dbg_info": {
            ...
        }
    }
}
```

## Step 3. Use the token when making calls to IMF API services  

The issued token can then be used to access all endpoints available under the host endpoint `api.appnexus.com/imf`. 

```
$ curl -b cookies -c cookies 'https://api.appnexus.com/imf/api/v1/rest/data/aliasFunctions'
{
    "response": {
        "aliasFunctions": [
            {
                "name": "ACTIVE_CUSTOM_PRODUCTS",
                "inputs": [
                "ARRAY"
                ]
            },
        ...
        ]
    }
}
```

Alternately, if you didn't store the token in a cookie, you can put the token in the request header as `"Authorization: TOKEN"`.

```
$ curl -H "Authorization: h3vlp0122344" 'https://api.appnexus.com/imf/api/v1/rest/data/aliasFunctions' 
{
    "response": {
        "aliasFunctions": [
            {
                "name": "ACTIVE_CUSTOM_PRODUCTS",
                "inputs": [
                "ARRAY"
                ]
            },
        ...
        ]
    }
}
```

## Authentication frequency

After authenticating, your token remains valid for 2 hours. You do not need to re-authenticate within this time. If you do re-authenticate, please note the following limitation:
- The API permits you to authenticate successfully 10 times per 5-minute period. 
- Any subsequent authentication attempts within those 5 minutes will result in an error.

> [!TIP]
> It is best practice to listen for the `"NOAUTH"` `error_id` in your call responses and re-authenticate only after receiving it.

## Related topics

- [Account Recovery Service](../digital-platform-api/account-recovery-service.md)
- [API Best Practices](../digital-platform-api/api-best-practices.md)
- [API Usage Constraints](../digital-platform-api/api-usage-constraints.md)
- [API Semantics](../digital-platform-api/api-semantics.md)