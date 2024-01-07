---
title: Microsoft Monetize - Single Credential Login and Multi-Factor Authentication FAQ
description: The article addresses common inquiries regarding single credential login and Multi-Factor Authentication (MFA), providing answers to frequently asked questions on these topics.
ms.date: 10/28/2023
---

# Microsoft Monetize - Single credential login and multi-factor authentication FAQ

You can find answers to the most frequently asked questions about single credential login and MFA.

> [!NOTE]
>
> With consolidation of Xandr to Microsoft family, we have integrated the authentication process of the users (who are using Xandr products) to the Microsoft Identity Platform. The profound advantage of this integration is that users would be able use to access Xandr applications using the same sign-on methods to access other Microsoft products.
> Additionally, the integration to the Microsoft Identity Platform enables new and more secure methods of authentication, powered by Microsoft.
>
> For more details, visit [Microsoft Identity Platform Login](microsoft-identity-platform-login.md).

## Why is Xandr implementing single credential login and multi-factor authentication?

A number of long-standing pain points relating to how users access Xandr’s digital platform applications are being addressed. The issues were:

- Users must have a separate set of authentication credentials to access each of their user accounts. Therefore, they must create, remember and periodically reset multiple passwords.
- Users must sign in to each user account individually. Therefore, they must sign in each time they switch between user accounts/seats in order to transact on behalf of a different member.
- The more usernames and passwords a user has to remember, the more likely they are to write them down. This creates a security risk for Xandr and our clients.
- Xandr’s new Information Security Policies (XISP) require that all Xandr applications be protected by a second factor of authentication.
- Overall, we are simplifying how users manage their accounts.

## Can a user opt out of unified login?

No. It's a global functional update and it is being rolled out to all users.

## Can a client/user opt out of Multi-Factor Authentication (MFA)?

No. It's a global functional update and it is being rolled out to all users.

## What seat is assigned to your default account after they sign in, when they haven't selected a default account?

The user account under the first member in the list of members that have access to, sorted alphabetically.

## Can a user sign in with their old single account credentials?

No. Once a user has been entered in the new system, their previous credentials are defunct. When signing in, they will use their single credential and MFA authentication credentials to access all of their user accounts across all of the digital platform applications. They will no longer be able to access the individual user accounts directly using their individual sets of authentication credentials. If a user attempts to, they will be presented with an error message instructing them to use their new credentials.

## What are the password requirements for the single credential login and multi-factor authentication?

- At least 8 characters in length
- Contains 3 of the following 4 character types:
  - Lowercase letters (a-z)
  - Uppercase letters (A-Z)
  - Numbers (0-9)
  - Special Characters (for example, !@#$%^&\*)
- No more than 2 identical characters in a row (for example, "aaa" not allowed)

## When does the single credential login and multi-factor authentication password expire?

365 days after it was set or last changed.

## Will users be notified when the single credential login and multi-factor authentication password is about to expire?

Yes. They will receive a password expiry warning email 21 days and 5 days prior to expiry, and an expired notification email on expiry.

## How can a user switch out the MFA app they are using for a different one?

Product Support can reset the users MFA account via the single credential login tool. The user will be prompted to setup their MFA account again the next time they successfully sign in to a Xandr Digital Platform application with their username and password.

## Related topic

[Troubleshooting Multi-Factor Authentication (MFA)](troubleshooting-multi-factor-authentication-mfa.md)
