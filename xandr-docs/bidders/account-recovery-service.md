---
title: Bidders - Account Recovery Service
description: In this article, learn how to reset your Xandr password or retrieve your Xandr username using the Account Recovery Service.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidders - Account recovery service

The Account Recovery Service allows you to reset your Xandr password or retrieve your Xandr username.

## Reset your password

If you cannot log in to Xandr's bidder API due to a forgotten password, follow the steps below to reset your password.

### Step 1. Create a JSON-formatted file including your username

```
$ cat reset_password_1
{
    "account-recovery": {
        "username" : "USERNAME"
    }
}
```

### Step 2. POST the file to the account recovery service

```
$ curl -X POST -d @reset_password_1 'https://api.adnxs.com/account-recovery'
{
    "response": {
        "status": "OK",
        "dbg_info": {
            ...
        }
    }
}
```

### Step 3. Check your email

The previous step triggers the system to send an email to the address associated with the username in the JSON-formatted file. The email includes the token that you will use in the next step.

> [!IMPORTANT]
> The token is valid for 16 hours.
> [!NOTE]
> If you don't receive an email, the username in the file may not be valid. Check the username for accuracy and try again. If you have forgotten your username, see [Retrieve Your Username](#retrieve-your-username) below.

### Step 4. Create a JSON-formatted file including your new password and token

```
$ cat reset_password_2
{
    "account-recovery": {
        "password": "NEW_PASSWORD",
        "token": "TOKEN_FROM_EMAIL"
    }
}
```

#### Guidelines for creating your password

When creating your password, please create a complex password with the following:

- 10 or more characters
- 64 or fewer characters
- At least one capital letter (A–Z)
- At least one lowercase letter (a–z)
- At least one digit (0–9)
- At least one special character (such as \#, $, ? %, &)

### Step 5. PUT the file to the account recovery service

This resets your password and sends a confirmation email to the address associated with your username. Once you receive the confirmation email, you can log in to the API with your username and new password. See [Authentication Service](authentication-service.md) for guidance.

```
$ curl -X PUT -d @reset_password_2 'https://api.adnxs.com/account-recovery'
{
    "response": {
        "status": "OK",
        "dbg_info": {
            ...
        }
    }
}
```

## Retrieve your username

If you cannot log in to the API due to a forgotten username, follow the steps below to retrieve your username.

### Step 1. Create a JSON-formatted file including your email address

```
$ cat retrieve_username
{
    "account-recovery": {
        "email" : "EMAIL_ADDRESS"
    }
}
```

### Step 2. POST the file to the account recovery service

```
$ curl -X POST -d @retrieve_username 'https://api.adnxs.com/account-recovery'
{
    "response": {
        "status": "OK",
        "dbg_info": {
            ... 
        }
    }
}
```

### Step 3. Check your email

The previous step triggers the system to send an email to the address specified in the file. The email includes the username(s) that are associated with the email address. Once you receive the email, you can log in to the API with your username and new password. See [Authentication Service](authentication-service.md) for guidance.

> [!NOTE]
> If you don't receive an email, the email address or host URL in the file may not be valid. Check the values for accuracy and try again.

## Related topics

- [Authentication Service](authentication-service.md)
- [User Service](user-service.md)
