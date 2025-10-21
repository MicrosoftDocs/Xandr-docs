---
title: Microsoft Curate - Troubleshoot Microsoft Identity Platform login
description: In this article, find answers to some of the most common scenarios that might occur while using the Microsoft Identity Platform.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-curate
ms.author: shsrinivasan
---

# Microsoft Curate - Troubleshoot Microsoft Identity Platform login

This document outlines some scenarios where questions may arise in the minds of users while using Microsoft Identity Platform.

## I don't have a Microsoft Account

You can register for a free Microsoft Personal Account with any existing email you have access to. Go to [the link](https://account.microsoft.com/account) to register or manage your Microsoft Account.

If your company sets up Federated Sign-in for your corporate email domain, visit the following pages for more information:

- [Microsoft Entra ID](https://www.microsoft.com/security/business/identity-access/microsoft-entra-id)(formerly Azure Active Directory)
- [Single Sign On](/entra/identity/enterprise-apps/what-is-single-sign-on)

## Error: Email does not match any accounts after logging into Microsoft Advertising

Upon logging in, if you receive an error saying your email does not match any accounts, that means no user objects in the Microsoft Advertising Platform match the email or user principal name provided by the Microsoft Identity Platform. This requires updating the users registered in the Microsoft Advertising Platform to match the email address or user principal name that you signed into Microsoft.

You can contact the designated person with the role of **User Manager** in your seat to update the email ID of your user on your behalf. If you are not aware of the User Manager, you can contact your Microsoft Advertising Account Representative or Microsoft Advertising Support on our [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com).

## I can't access API with my Microsoft credentials

Currently Microsoft Advertising APIs do not support Microsoft credentials. To view the username and reset the password for the API, log in to one of the Microsoft Advertising products in your browser, and navigate to **Account Settings** from the top right navigation dropdown. On this page, you'll be able to see the accounts to which you have access and what the corresponding username is. You can trigger a password reset for each of the accounts here.

## Error after logging into Microsoft Advertising: email does not match any accounts and no access

For improved security, Microsoft Advertising discourages the use of shared credential or user accounts. When access is associated with a single person, it helps in easier access management and robust auditing.

Microsoft Advertising suggests updating the account's email address to that of an individual person with the Microsoft Advertising User Manager, or by contacting your Microsoft Advertising Account Representative or Microsoft Advertising Support on our [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com).

## I don't see all accounts I have access to in Seat Switcher or Account Settings page

This scenario signifies that the email or user principal name used to sign in to Microsoft does not match the user or account you are looking for. Troubleshooting of this issue requires updating the users registered in the Microsoft Advertising Platform to match the email address or user principal name that you use to sign into Microsoft.

You can contact the designated person with the role of **User Manager** in your seat to update the email ID of your user on your behalf. If you are not aware of the User Manager, you can contact your Microsoft Advertising Account Representative or Microsoft Advertising Support on our [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com).

## Microsoft Identity Platform says I must have an admin consent to permissions and won't let me sign in

Some organizations might require higher level of consent with their corporate sign in process with Microsoft Identity Platform. Please contact your IT support and request them to consent to the Microsoft Advertising Digital Platform requested permissions in Azure Active Directory Enterprise Applications.

They can provide consent either through the Azure Portal, or by attempting to sign in to a Microsoft Advertising product with their Azure Active Directory admin credentials.

## I'm having trouble signing into Microsoft

If it is a personal Microsoft Account and not a corporate managed account, please visit [this link](https://support.microsoft.com/en-us/account-billing/get-help-with-your-microsoft-account-ace6f3b3-e2d3-aeb1-6b96-d2e9e7e52133) for help.

If it is a corporate managed account, please contact your organization's IT support.
