---
title: Microsoft Invest - Migration to Microsoft Identity Platform Login
description: In this article, explore detailed step-by-step instructions on how to migrate an existing authentication process to the Microsoft Identity Platform.
ms.date: 10/28/2023
---

# Microsoft Invest - Migration to Microsoft Identity Platform login

This documentation provides step by step guide on how to migrate existing authentication process in Microsoft Advertising products to Microsoft Identity Platform.

1. Go to product login screen using [Microsoft Invest Login url](https://invest.xandr.com/login).

1. Select **Sign in with Microsoft** button.

    :::image type="content" source="media/sign-in-screen.png" alt-text="Screenshot of Microsoft Invest sign in window.":::

1. In **Action Required: Create a Microsoft Account** screen, you can:

    - Select **Create Microsoft Account** button and proceed.

    - Select **Remind me tomorrow** to delay the migration process.

      > [!NOTE]
      > This option to delay the migration is available till 16 June, 2023 and a countdown is displayed next to **Remind me tomorrow** to show how many days are remaining till then. Post June 16, you will have the option to select **Create Microsoft Account** only.

      :::image type="content" source="media/account-creation.png" alt-text="Screenshot of action required window.":::

1. In the **Sign In page**, enter Email ID associated with your Microsoft Advertising account login and select **Next**. If you have registered a different email ID for Microsoft products, ensure that Microsoft Advertising platform account matches the email used to login to Microsoft. If they do not match, contact the designated person with the role of User Manager from your organization to do the needful or you can raise a ticket in [Microsoft Advertising Support portal](https://help.xandr.com/).

     :::image type="content" source="media/sign-in-page.png" alt-text="Screenshot of Microsoft sign in window.":::

     > [!NOTE]
     > If you do not have a Microsoft account, you can create using **Create one!** link in the page.

1. Enter the password and select **Sign in** to proceed.

     :::image type="content" source="media/sign-in-password.png" alt-text="Screenshot of password window.":::

1. If your organization requires IT Admin approval to use the **Sign in with Microsoft** method to log into Microsoft Invest, then follow up with your organization's IT team.

1. If your organization has implemented Multi Factor Authention (MFA) process, you will be presented with MFA challenge. Use [Microsoft Authenticator App](https://www.microsoft.com/en-in/security/mobile-authenticator-app) to do the needful and enter the One-time password code displayed in the app to login to your account.

1. Post successful authentication, you will be directed to the landing page of the Microsoft Invest. This marks the succesful completion of the migration process. Going forward, when you logs in to the application, you will be directed to sign in with Microsoft Identity Platform.
