---
title: Microsoft Monetize - Set Up multi-factor authentication
description: Explore setting up Multi-Factor Authentication (MFA) with instructions on using Auth0 Guardian or Google Authenticator for enhanced security.
ms.date: 10/28/2023
---

# Microsoft Monetize - Set up multi-factor authentication

This will guide you through the multi-factor authentication set up process.

When signing in for the first time, you will be directed through the process for setting up your Multi-Factor Authentication (MFA) account. You will receive a notification to **Download Auth0 Guardian for free**. There will be two primary selections (App Store for Apple and Google Play), and one alternative selection (Google Authenticator) available. You can select any of them.

> [!NOTE]
> If you have already downloaded one of the two choices of primary selections, click **I've already downloaded it** verbiage to alert the system.

This task explains how to set up your MFA account.

1. Once you download any of the selections mentioned above, a QR code is displayed. Scan this QR code with Google Authenticator, or a similar app.

   If you have trouble scanning, there is a placeholder available to enter your passcode. You also have the option of using Guardian.

1. A recovery code screen is displayed. In the event that you need to log in without your device, you will need this recovery code. Note this code, and keep it somewhere safe.
1. Click the arrow **\>** to continue.

   A notification is displayed that you have successfully set up multi-factor authentication.

1. When you log in to the application, enter your email address and password and click **Next**.
1. If using Google Authenticator, open your MFA application to access the one-time six digit code. Enter this six-digit code to authenticate and log in.

      > [!NOTE]
      > You will have a limited amount of time to enter this code as after a certain time period it expires.
      > This is a one-time use code. You need to enter a new code every time when you try to authenticate.

1. If using Auth0 Guardian, open your MFA application to access your notifications to accept the MFA challenge. You will not need any authentication code like Google Authenticator as Auth0 Guardian creates a push notification that you need to acknowledge to proceed.

You can use your MFA credentials to log in to your digital application user accounts now. Post login, you can switch between your user accounts following the steps described in [Switching Between User Accounts](switching-between-user-accounts.md).

## Related topics

- [Troubleshooting Multi-Factor Authentication (MFA)](troubleshooting-multi-factor-authentication-mfa.md)
- [Single Credential Login and Multi-Factor Authentication FAQ](single-credential-login-and-multi-factor-authentication-faq.md)
