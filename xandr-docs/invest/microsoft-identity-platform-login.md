---
title: Microsoft Invest - Identity Platform Login
description: In this article, explore an overview of authenticating users for Microsoft Advertising products using Microsoft Identity Platform.
ms.date: 10/28/2023
---

# Microsoft Invest - Identity Platform login

This document outlines an overview of authenticating users for Microsoft Advertising Products using Microsoft Identity Platform.

With consolidation of Microsoft Advertising to Microsoft family, we have integrated the authentication process of the users (who are using Microsoft Advertising products) to the Microsoft Identity Platform. The profound advantage of this integration is that users would be able use to access Microsoft Advertising applications using the same sign-on methods to access other Microsoft products. Additionally, the integration to the Microsoft Identity Platform enables new and more secure methods of authentication, powered by Microsoft.

## Benefits of signing in with Microsoft Identity Platform

**Improved Security:** The Microsoft Identity Platform brings modern security practices to the Microsoft Advertising platform.

**Single Sign On:** Organizations that integrate with the Microsoft Identity Platform to enable Single Sign On (SSO) with other Microsoft products will be benefited by this approach as the capabilities such as a corporate control of credentials, access rules, etc. will be applicable to Microsoft Advertising product logins also.

**Account Switcher:** Users with access to multiple accounts on the Microsoft Advertising Platform will be able to switch between different accounts seamlessly without being required to sign out and sign back in.

## Microsoft Advertising Platform support of Microsoft Identity Platform

Currently, following Microsoft Advertising products support authentication using the Microsoft Identity Platform:

- Microsoft Monetize
- Microsoft Invest
- Microsoft Curate
- Microsoft Advertising Customer Support Portal

Following Microsoft Advertising products are not supported on the Microsoft Identity Platform currently, but soon will be migrated:

- Digital Platform API
- Impression Bus API
- Yield Analytics
- Bidder Platform


Features that yet to be supported by Microsoft Advertising are:

- Automatic Provisioning of Users
- Account Linking between multiple email addresses

## Authentication options with the Microsoft Identity Platform

Microsoft Advertising's integration with the Microsoft Identity Platform allows users to authenticate with two options:

- Azure Active Directory supported SSO (Preferred Method)
- Personal Microsoft Accounts

### Azure Active Directory supported SSO (preferred method)

Microsoft Identity Platform enables organizations to authenticate their users to various cloud and on-premise solutions using the same set of credentials. Couple of Microsoft Advertising customers are already integrated and they can utilize the Microsoft Identity Platform SSO solution without any additional configuration. If you are yet to be integrated with Microsoft Identity Platform, you can learn more about Azure Active Directory and Single Sign On [here](https://www.microsoft.com/security/business/identity-access/azure-active-directory-single-sign-on).

### Personal Microsoft accounts

If you do not have an organization level integration with Azure Active Directory or the Microsoft Identity Platform, you can still use the Microsoft Identity Platform by registering your email address as a Microsoft Account, or creating a new account with Microsoft. For more details about this process, see [here](https://account.microsoft.com/account/Account).

## Prerequisites for signing in with the Microsoft Identity Platform

1. Have a Microsoft Identity Platform account
    - If you have corporate managed account which is used to login to other Microsoft products, this should already be configured.
    - If your corporate domain is not managed, you can register your email as a Microsoft Account [here](https://account.microsoft.com/account/Account) or from the sign in page.
1. Ensure that the email associated to your Microsoft Advertising platform account matches the user principal name or email used to login to Microsoft. Contact the designated person with the role of **User Manager** from your organization to do the needful by following the below mentioned steps:
    - Go to the **User Management** module in a Microsoft Advertising product.
    - Update the email IDs of users to match the user principal names or email IDs of the Microsoft Account or Azure Active Directory integration.

## Related topic

[Microsoft Identity Platform Login Troubleshooting](microsoft-identity-platform-login-troubleshooting.md)
