---
title: Microsoft Monetize - Multi-Factor Authentication (MFA)
description: Explore Single Credential Login, Multi-Factor Authentication (MFA), and Microsoft Advertising integration for unified, secure access methods.
ms.date: 10/28/2023
---

# Microsoft Monetize - Multi-Factor Authentication (MFA)

This is an overview of single credential login and multi-factor authentication.

> [!NOTE]
> With consolidation of Microsoft Advertising to Microsoft family, we have integrated the authentication process of the users (who are using Microsoft Advertising products) to the Microsoft Identity Platform. The profound advantage of this integration is that users would be able use to access Microsoft Advertising applications using the same sign-on methods to access other Microsoft products.
> Additionally, the integration to the Microsoft Identity Platform enables new and more secure methods of authentication, powered by Microsoft.
>
> For more details, visit [Microsoft Identity Platform Login](microsoft-identity-platform-login.md).

Microsoft Advertising is changing the way users access their digital platform application user accounts via the user interfaces. As a result of the changes, users will use a single set of authentication credentials (email and password) to access all of their digital application user accounts. After they're signed in, they will seamlessly switch between their user accounts, using the **Member Switcher UI**, without having to log in to each one individually. At the same time, we are introducing a compulsory second factor of authentication (MFA) in the form of a one-time passcode (for example, Google Authenticator).

> [!NOTE]
> This is a one-time use code. You need to enter a new one-time use code every time that you try to authenticate.

You can use your existing API credentials for API access. The only change is that you need to reset your password when you log in to the user interface and go to your account.

> [!NOTE]
> Not all of our current accounts have been migrated into this new way of authenticating. This only applies to accounts who have already been migrated into the new system.

## Why is this change happening?

Overall, we are simplifying how users manage their accounts in order to address a number of long-standing pain points with how users access Microsoft Advertising’s digital platform applications. For example:

- Users needed a separate set of authentication credentials to access each of their user accounts. Therefore, they must create, remember and periodically reset multiple passwords.
- Users had to sign in to each user account individually. Therefore, they had to sign out and sign back in each time they switched between user accounts/seats in order to transact on behalf of a different member.
- The more usernames and passwords a user has to remember, the more likely they are to write them down. This created a security risk for Microsoft Advertising and our clients.

To make new accounts more secure, Microsoft Advertising’s new Information Security Policies (XISP) require all Microsoft Advertising applications be protected by a second authenication factor of authentication.

## What isn't changing?

This new authentication method only applies to users who access our applications via the UI. Users will continue accessing their API user accounts using their individual sets of authentication credentials. Changes to how users authenticate into their API accounts will be made to API access in the near future.

API access still relies on username and password.

## Related topics

- [Set Up Single Credential Login](set-up-single-credential-login.md)
- [Set Up Multi-Factor Authentication](set-up-multi-factor-authentication.md)
