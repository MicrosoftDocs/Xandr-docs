---
title: Microsoft Curate - Universal Pixel Basic Implementation
description: Learn how to implement the universal pixel at the basic level. The universal pixel can track page views and identify URLs. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-curate
ms.author: shsrinivasan
---

# Microsoft Curate - Universal pixel basic implementation

With the most basic implementation of the universal pixel, you can track page views and identify the URLs driving them. Setting up the basic implementation requires you to set up the Universal Pixel object in Curate, deploy the script code containing the pixel ID on your website, and check your pixel activity on the **Activity** tab in the **Universal Pixels** page.

## Create, deploy, and test the pixel

Configure your pixel code using the UI.

1. From the top menu bar, select **Audiences** \> **Universal Pixel**.
1. Select **New**.
1. Select an advertiser from the list.
1. Select **Track Your Website Activity** or **Track Your App Activity**.
1. Enter a name for your pixel in the **Name** field and **Save** to continue. The next screen displays the universal script code that you’ll deploy in the `<head>` tag on the advertiser website.
1. Decide what to do with your pixel code:
    - If you plan to deploy the universal script code on the website yourself, follow the instructions onscreen to copy and paste the code.
    - If you plan to have a web developer handle the code deployment, enter one or more email addresses and select **Send the installation instructions to a developer to install on your behalf**.
1. Select **Go to Analytics Screen**. Curate displays the **Universal Pixel** page. The **Activity** tab is selected by default, and shows activity for your URLs after your campaign has run for some time. This page also shows the pixel ID and UUID, as well as the time when the pixel last fired.

   Deploy the code on your website.

1. Deploy the universal pixel script code in the `<head>` tag of the advertiser website. Many advertisers use a tag manager to achieve this. If you need to access the script code after initial pixel creation, select the pencil icon next to the pixel name.

   Make sure your pixel is detecting activity.

1. After deploying the code, verify your pixel is active by checking the **Activity** tab.

## Related topics

- [Universal Pixel Code Structure](./universal-pixel-code-structure.md)
- [Report on Universal Pixels](./universal-pixel-reporting.md)
