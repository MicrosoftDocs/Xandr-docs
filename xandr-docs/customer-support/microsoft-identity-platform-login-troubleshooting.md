---
<<<<<<< HEAD
title: Customer Support Portal - Microsoft Identity Platform Login Troubleshooting
description: In this article, explore the different scenarios in which users might have questions while setting up the Microsoft Identity Platform login account.
ms.date: 11/11/2024
=======
title: Customer Support Portal - Troubleshhot Microsoft Identity Platform Login description: In this article, explore the different scenarios in which users might have questions while setting up the Microsoft Identity Platform login account.
ms.date: 11/12/2024
>>>>>>> 4164210b (BG-Epic-7984896-cs-part2-Br2-PR)
ms.author: shsrinivasan
---

# Customer Support Portal - Troubleshoot Microsoft Identity Platform login

This document outlines some scenarios where questions may arise in the minds of users while using Microsoft Identity Platform.

## I don't have a Microsoft account

You can register for a free Microsoft Personal Account with any existing email you have access to. Go to this [link](https://account.microsoft.com/account) to register or manage your Microsoft Account.

If you company sets up Federated Sign-in for your corporate email domain, visit the following pages for more information:

- [Microsoft Entra (formerly Azure Active Directory)](https://azure.microsoft.com/products/active-directory)
- [Single Sign On](/azure/active-directory/manage-apps/what-is-single-sign-on)

## After logging into a Microsoft Advertising product, I receive an error saying my email does not match any accounts and I don't have access

Upon logging in, if you receive an error saying your email does not match any accounts, that means no user objects in the Microsoft Advertising platform match the email or user principle name provided by the Microsoft Identity Platform. This requires updating the users registered in the Microsoft Advertising platform to match the email address or user principle name that you signed into Microsoft.

You can contact the designated person with the role of **User Manager** in your seat to update the email ID of your user on your behalf. If you are not aware of the User Manager, you can contact your Microsoft Advertising Account Representative or Microsoft Advertising Support <!-- at [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com).-->

## I can't access the API with my Microsoft credentials

Currently Microsoft Advertising APIs do not support Microsoft credentials. To view the username and reset the password for the API, login to one of the Microsoft Advertising products in your browser, and navigate to **Account Settings** from the top right navigation dropdown. On this page, you'll be able to see the accounts to which you have access and what is the corresponding username. You can trigger a password reset for each of the accounts here.

## The email associated with my user is a distribution list and cannot be signed into through my corporate identity provider

For improved security, Microsoft Advertising discourages the use of shared credential or user accounts. When access is associated with a single person, it helps in easier access management and robust auditing.

## I don't see all the accounts I have access to in the Seat Switcher or Account Settings page

This scenario signifies that the email or user principal name used to sign in to Microsoft does not match the user or account you are looking for. Troubleshooting of this issue requires updating the users registered in the Microsoft Advertising platform to match the email address or user principle name that you use to sign into Microsoft.

## Microsoft Identity Platform says I must have an admin consent to permissions and won't let me sign in

Some organizations might require higher level of consent with their corporate sign in process with Microsoft Identity Platform. Contact your IT support, and request them to consent to the Microsoft Advertising Digital Platform requested permissions in Azure Active Directory Enterprise Applications.

They can provide consent either through the Azure Portal, or by attempting to sign in to a Microsoft Advertising product with their Azure Active Directory admin credentials.

## I'm having trouble signing into Microsoft

If it is a personal Microsoft Account, and not a corporate managed account, visit this [link](https://support.microsoft.com/en-us/account-billing/get-help-with-your-microsoft-account-ace6f3b3-e2d3-aeb1-6b96-d2e9e7e52133) for help.

If it is a corporate managed account, contact your organization's IT support.
