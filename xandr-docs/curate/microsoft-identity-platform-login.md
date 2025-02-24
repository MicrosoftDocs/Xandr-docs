---
title: Microsoft Curate - Microsoft Identity Platform Login
description: In this article, learn about using the Microsoft Identity Platform to authenticate users for Microsoft Advertising Advertising Products.
ms.date : 10/28/2023
---

# Microsoft Curate - Microsoft Identity Platform login

This document outlines an overview of authenticating users for Microsoft Advertising Advertising Products using Microsoft Identity Platform.

With the consolidation of Microsoft Advertising to the Microsoft family, we have integrated the authentication process of the users (who are using Microsoft Advertising products) to the Microsoft Identity Platform. The profound advantage of this integration is that users would be able to access Microsoft Advertising applications using the same sign-on methods as for other Microsoft products. Additionally, the integration to the Microsoft Identity Platform enables new and more secure methods of authentication, powered by Microsoft.

## Benefits of signing in with Microsoft Identity Platform

**Improved Security** - The Microsoft Identity Platform brings modern security practices to the Microsoft Advertising platform.

**Single Sign On** - Organizations that integrate with the Microsoft Identity Platform to enable Single Sign On (SSO) with other Microsoft products will be benefited by this approach as capabilities such as corporate control of credentials, access rules, etc. will be applicable to Microsoft Advertising product logins also.

**Account Switcher** - Users with access to multiple accounts on the Microsoft Advertising Platform will be able to switch between different accounts seamlessly without being required to sign out and sign back in.

## Microsoft Advertising Platform supports Microsoft Identity Platform

Currently, the following Microsoft Advertising products support authentication using the Microsoft Identity Platform:

- Microsoft Monetize
- Microsoft Invest
- Microsoft Curate

The following Microsoft Advertising products are not supported on the Microsoft Identity Platform currently, but soon will be migrated:

- Digital Platform API
- Impression Bus API
- Yield Analytics
- Bidder Platform
- Microsoft Advertising Customer Support Portal

Features that are yet to be supported by Microsoft Advertising are:

- Automatic Provisioning of Users
- Account Linking between multiple email addresses

## Authentication options with Microsoft Identity Platform

Microsoft Advertising's integration with the Microsoft Identity Platform allows users to authenticate with two options:

- Microsoft Entra (formerly Azure Active Directory) supported SSO (Preferred Method)
- Personal Microsoft Accounts

### Microsoft Entra (formerly Azure Active Directory) supported SSO (Preferred Method)

Microsoft Identity Platform enables organizations to authenticate their users to various cloud and on-premise solutions using the same set of credentials. Some Microsoft Advertising customers are already integrated and they can utilize the Microsoft Identity Platform SSO solution without any additional configuration. If you are yet to be integrated with Microsoft Identity Platform, you can learn more about Microsoft Entra and Single Sign On [here](https://www.microsoft.com/en-us/security/business/identity-access/microsoft-entra-single-sign-on).

### Personal Microsoft accounts

If you do not have an organization level integration with Microsoft Entra (formerly Azure Active Directory) or the Microsoft Identity Platform, you can still use the Microsoft Identity Platform by registering your email address as a Microsoft Account, or creating a new account with Microsoft. For more details about this process, select [here](https://account.microsoft.com/account/Account).

## Prerequisites for signing in with Microsoft Identity Platform

- Have a Microsoft Identity Platform account
  - If you have a corporate managed account which is used to login to other Microsoft products, this should already be configured.
  - If your corporate domain is not managed, you can register your email as a Microsoft Account [here](https://account.microsoft.com/account/Account) or from the sign in page.

- Ensure that the email associated to your Microsoft Advertising platform account matches the user principal name or email used to login to Microsoft. Contact the designated person with the role of **User Manager** from your organization to do the needful by following the below mentioned steps:
  1. Go to the **User Management** module in a Microsoft Advertising product.
  1. Update the email IDs of users to match the user principal names or email IDs of the Microsoft Account or Microsoft Entra (formerly Azure Active Directory) integration.

## Related topic

[Troubleshoot Microsoft Identity Platform Login](microsoft-identity-platform-login-troubleshoot.md)
