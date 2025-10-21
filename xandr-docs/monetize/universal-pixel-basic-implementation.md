---
title: Microsoft Monetize - Universal Pixel Basic Implementation
description: In this article, learn how to set up the most basic implementation of the universal pixel to track page views and identify the URLs driving them.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Universal Pixel basic implementation

With the most basic implementation of the universal pixel, you can track page views and identify the URLs driving them. Setting up the basic implementation requires you to set up the Universal Pixel object in Monetize, deploy the script code containing the pixel ID on your website, and check your pixel activity on the **Activity** tab in the **Universal Pixels** page.

To create, deploy, and test the pixel:

- [Configure your pixel code using the UI](#configure-your-pixel-code-using-the-ui).
- [Deploy the code on your website](#deploy-the-code-on-your-website).
- [Make sure your pixel is detecting activity](#make-sure-your-pixel-is-detecting-activity).

## Configure your pixel code using the UI

1. From the top menu bar, click **Advertisers** > **Universal Pixel** and select the associated advertiser
1. Click **Track Your Website Activity** or **Track Your App Activity**.
1. Type a name for your pixel in the **Name** field and **Save** to continue.

    The next screen displays the universal script code that you’ll deploy in the `<head>` tag on the advertiser website.

1. Decide what to do with your pixel code:
    - If you plan to deploy the universal script code on the website yourself, follow the instructions on-screen to copy and paste the code.
    - If you plan to have a web developer handle the code deployment, enter one or more email addresses and click **Send the installation instructions to a developer to install on your behalf**.
1. Click **Go to Analytics** Screen.

    Monetize displays the **Universal Pixel** page. The **Activity** tab is selected by default, and shows activity for your URLs after your campaign has run for some time. This page also shows the pixel ID and UUID, as well as the time when the pixel last fired.

## Deploy the code on your website

Deploy the universal pixel script code in the `<head>` tag of the advertiser website. Many advertisers use a tag manager to achieve this.

If you need to access the script code after initial pixel creation, click the pencil icon next to the pixel name.

## Make sure your pixel is detecting activity

After deploying the code, verify your pixel is active by checking the **Activity** tab.

## Related topics

- [Universal Pixel Code Structure](universal-pixel-code-structure.md)
- [Universal Pixel Reporting](universal-pixel-reporting.md)
