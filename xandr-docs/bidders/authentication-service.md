---
title: Impression Bus API authentication
description: In this article, learn about the authentication service with an example.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Impression Bus API authentication

Before you use Impression Bus API, you need to use your username and password to get an authorization token. To get the token, make a `POST` request to `https://api.adnxs.com/auth` with a JSON file containing your auth credentials.

This returns a JSON response with the token. You then have two options:

- put the token in the header in future requests as Authorization: TOKEN or
- put it in a cookie using the method discussed below **(recommended)**.

If you do not have a username and password, contact your Xandr account representative.

> [!NOTE]
> For an explanation of the errors that you may encounter during and after authentication, see the **Errors** section in [API Semantics](api-semantics.md).

## Time frame

When you authenticate, you receive an authorization token that remains active for 2 hours following your most recent call. It is best practice to re-authenticate only after you receive the `"NOAUTH"``error_id` in your call responses. If you follow this practice, the restriction above should have no impact on your implementation.

In addition, the service adds a 24-hour hard expiry. When an API session reaches the 24 hour mark, that session expires, regardless of when the most recent API call was made. The current behavior, in which a session expires after two hours of inactivity on the part of the client, remains unchanged. Programs that follow the guidelines in [API Best Practices](api-best-practices.md) should not be affected.

## How to authenticate
### Step 1: Create autnetication JSON

Create a JSON-formatted text file with your username and password. Below, we have used the `cat` command to show the output of an example file.

```
$ cat auth
{
 "auth":
  {
    "username" : "USERNAME",
    "password" : "PASSWORD"
  }
}
```

### Step 2: POST the request

Make a POST request using the `"auth"` file. The authorization request both sets a session cookie (`IBAPI_SESSID`) and returns a token in JSON. Note that we used the "verbose" parameter in the below example.

```
curl -v -X POST --data-binary @auth https://api.adnxs.com/auth
< HTTP/1.1 200 OK
< Date: Fri, 22 Aug 2008 12:12:13 GMT
< Set-Cookie: IBAPI_SESSID=622cee5f8c99c81e87614e9efc63eddb; path=/
< Content-Length: 58
< Content-Type: text/html
<
{
    "response": {
        "token": "622cee5f8c99c81e87614e9efc63eddb"
    }
}
```

### STEP 3: Using the token for API calls

The token can now be used to make a request from the API:

```
$ curl -H "Authorization: 622cee5f8c99c81e87614e9efc63eddb" https://api.adnxs.com/member
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

Alternatively, we can use the cookie. This is the recommended method and the notation we use in our examples. Here is an example using the Member Service.

```
$ curl -b cookies -c cookies -X POST -d @auth "https://api.adnxs.com/auth"
{
    "response": {
        "token": "622cee5f8c99c81e87614e9efc63eddb"
    }
}
$ curl -b cookies https://api.adnxs.com/member
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
## Authentication frequency

After authenticating, your token remains valid for 2 hours. You do not need to re-authenticate within this time.
> [!NOTE]
> If you do re-authenticate, be aware of the following limitation:
>
> 1. The API permits you to authenticate successfully 10 times per 5-minute period.
> 1. Any subsequent authentication attempts within those 5 minutes will result in an error.
> [!TIP]
> It is best practice to listen for the "NOAUTH" `error_id` in your call responses and re-authenticate only after receiving it.
