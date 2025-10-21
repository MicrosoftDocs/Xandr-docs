---
title: Partner Single Sign-on Access
description: In this article, learn about Partner single sign-on and how it works.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Partner single sign-on access

> [!IMPORTANT]
> This feature is no longer available. To integrate your company's SSO with Microsoft Identity Platform and to access the Microsoft Advertising products, see [Microsoft Identity Platform Login](microsoft-identity-platform-login.md).

## What is partner single sign-on

Partner single sign-on allows users to use their own company/corporate Identity Provider (IDP) username and password to access Microsoft Advertising systems and tools. This service allows you full control over the authentication of your user accounts that can access Microsoft Monetize. Basically, Microsoft Advertising acts as the service provider for Microsoft Monetize. Microsoft Advertising clients act as Identity Providers (IDPs) and control usernames, passwords and other information used to identify, authenticate and authorize users for Microsoft Monetize.

> [!IMPORTANT]
> Partner single sign-on only applies to Microsoft Monetize at this time. Users who gain access via the application programming interface (API) will not be able to use Microsoft Advertising's SSO solution at this time.

## Why would I choose partner single sign-on

Partner SSO provides additional security and usability by providing:

- Auto creation of user accounts
- Permission control within your IDP
- Revocation of user access to Microsoft Advertising accounts via your own systems

## Prerequisites/caveats for onboarding

- Single sign-on is only supported at this time for Microsoft Monetize and for users not enabled for the API.
- Microsoft Advertising only supports single sign-on for one user account per IDP entity.
- It is currently possible to have Partner SSO users and non-partner SSO users under the same member.

## How do I get started

Contact your Account Manager or the [Microsoft Advertising Support Team](https://support.ads.microsoft.com), and inform them that you would like to sign up for single sign-on.
