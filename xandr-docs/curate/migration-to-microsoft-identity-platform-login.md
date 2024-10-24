---
title: Microsoft Curate - Migration to Microsoft Identity Platform Login
description: In this article, find step-by-step instructions on how to migrate the existing authentication process in Microsoft Advertising products to Microsoft Identity Platform.
ms.date : 10/28/2023
---

# Microsoft Curate - Migration to Microsoft Identity Platform login

This documentation provides step by step instructions on how to migrate existing authentication process in Microsoft Advertising products to Microsoft Identity Platform.

1. Go to the product login screen using the [Microsoft Curate Login url](https://curate.xandr.com/login).

1. Select the **Sign in with Microsoft** button.

    :::image type="content" source="media/a.png" alt-text="A screenshot of the Microsoft Curate login screen.":::

1. In the **Action Required: Create a Microsoft Account** screen, you can:

    - Select the **Create Microsoft Account** button and proceed.

    - Select the **Remind me tomorrow** to delay the migration process.

    > [!IMPORTANT]
    > This option to delay the migration is available till 16 June, 2023 and a countdown is displayed next to **Remind me tomorrow** to show how many days are remaining till then. Post June 16, you will only have the option to select **Create Microsoft Account**.

    :::image type="content" source="media/b.png" alt-text="A screenshot of the Action Required: Create a Microsoft Account screen.":::

1. In the **Sign in** page, enter Email ID associated with your Microsoft Advertising account login and select **Next**. If you have registered a different email ID for Microsoft products, ensure that the Microsoft Advertising platform account matches the email used to log in to Microsoft. If they do not match, contact the designated person with the role of **User Manager** from your organization to do the needful or you can raise a ticket on the [Microsoft Advertising Customer Support Portal](https://help.xandr.com/s/login/).

    :::image type="content" source="media/c.png" alt-text="A screenshot of the Microsoft sign in page.":::

    > [!NOTE]
    > If you do not have a Microsoft account, you can create one using the **Create one!** link in the page.

1. Enter the password and select **Sign in** to proceed.

    :::image type="content" source="media/d.png" alt-text="A screenshot of the password field on the Microsoft sign in page.":::

1. If your organization requires IT Admin approval to use the **Sign in with Microsoft** method to log into Microsoft Curate, then follow up with your organization's IT team.

1. If your organization has implemented Multi Factor Authention (MFA) process, you will be presented with MFA challenge. Use the [Microsoft Authenticator App](https://www.microsoft.com/en-in/security/mobile-authenticator-app) to do the needful and enter the One-time password code displayed in the app to login to your account.

1. Post successful authentication, you will be directed to the landing page of Microsoft Curate. This marks the succesful completion of the migration process. Going forward, when you log in to the application, you will be directed to sign in with Microsoft Identity Platform.
