---
title: Digital Platform API - Account Recovery Service
description: In this article, learn about the Account Recovery service and step-by-step instructions on how to reset your acoount password or retrieve your username.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Account Recovery service

The Account Recovery Service allows you to [reset your Xandr password](#reset-your-password) or [retrieve your username](#retrieve-your-username).

## Reset your password

If you cannot log in to the API due to a forgotten password, follow the steps below to reset your password.

- [Step 1: Create a JSON-formatted file (password reset)](#step-1-create-a-json-formatted-file-password-reset)
- [Step 2: POST the file (password reset)](#step-2-post-the-file-password-reset)
- [Step 3: Check your email (password reset)](#step-3-check-your-email-password-reset)
- [Step 4: Create a password and token file (password reset)](#step-4-create-a-password-and-token-file-password-reset)
- [Step 5: PUT the file (password reset)](#step-5-put-the-file-password-reset)

### Step 1: Create a JSON-formatted file (password reset)

Include your username.

```
$ cat reset_password_1
{
    "account-recovery": {
        "username" : "USERNAME"
    }
}
```

### Step 2: `POST` the file (password reset)

`POST` the file to the account recovery service.

```
$ curl -X POST -d @reset_password_1 'https://api.appnexus.com/account-recovery'
{
    "response": {
        "status": "OK",
        "dbg_info": {
            ...
        }
    }
}
```

### Step 3: Check your email (password reset)

The previous step triggers the system to send an email to the address associated with the username in the JSON-formatted file. The email includes the token that you will use in the next step.

> [!NOTE]
> The token is valid for 16 hours.
>
> If you don't receive an email, the username in the file may not be valid. Check the username for accuracy and try again. If you have forgotten your username, see [Retrieve your username](#retrieve-your-username) below.

### Step 4: Create a password and token file (password reset)

Create a JSON-formatted file including your user name, your new password, and the token received in your email.

```
$ cat reset_password_2
{
    "account-recovery": {
        "username": "USERNAME",
        "password": "NEW_PASSWORD",
        "token": "TOKEN_FROM_EMAIL"
    }
}
```

#### Guidelines for creating your password

When creating your password, create a complex password with the following:

- 10 or more characters.
- 64 or fewer characters.
- At least one capital letter (A–Z).
- At least one lowercase letter (a–z).
- At least one digit (0–9).
- At least one special character (such as \#, $, ?, %, &).

### Step 5: `PUT` the file (password reset)

`PUT` the file to the account recovery service.

This resets your password and sends a confirmation email to the address associated with your username. Once you receive the confirmation email, you can log in to the API with your username and new password. For guidance, see [Authentication Service](authentication-service.md).

```
$ curl -X PUT -d @reset_password_2 'https://api.appnexus.com/account-recovery'
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

If you cannot log in to the API due to a forgotten username, follow the steps below to retrieve your username.

- [Step 1: Create a JSON-formatted file (retrieve username)](#step-1-create-a-json-formatted-file-retrieve-username)
- [Step 2: POST the file (retrieve username)](#step-2-post-the-file-retrieve-username)
- [Step 3: Check your email (retrieve username)](#step-3-check-your-email-retrieve-username)

### Step 1: Create a JSON-formatted file (retrieve username)

Include your email address.

```
$ cat retrieve_username
{
    "account-recovery": {
        "email" : "EMAIL_ADDRESS"
    }
    }
```

### Step 2: `POST` the file (retrieve username)

`POST` the file to the account recovery service.

```
$ curl -X POST -d @retrieve_username 'https://api.appnexus.com/account-recovery'
{
    "response": {
        "status": "OK",
        "dbg_info": {
            ... 
        }
    }
    }
```

### Step 3: Check your email (retrieve username)

The previous step triggers the system to send an email to the address specified in the file. The email includes the username(s) that are associated with the email address. Once you receive the email, you can log in to the API with your username and new password. For guidance, see [Authentication Service](authentication-service.md).

> [!NOTE]
> If you don't receive an email, the email address or host URL in the file may not be valid. Check the values for accuracy and try again.

## Related topics

- [Authentication Service](authentication-service.md)
- [User Service](user-service.md)
