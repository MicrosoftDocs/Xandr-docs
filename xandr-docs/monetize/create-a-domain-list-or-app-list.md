---
title: Create a Domain List or App List
description: In this article, find instructions on how to create a new domain list or app list.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Overview

> [!NOTE]
> Targeting lists are only available to Standard Line Items. For an overview of which targeting options are available to Standard versus Augmented Line items, see [Buy-Side Targeting](buy-side-targeting.md).

You can create a new domain list or app list by uploading a text file, or by entering domains or apps manually into Monetize. This page walks you through the process. For details about creating a list by duplicating an existing list, see [Explore Domain Lists or App Lists](explore-domain-lists-or-app-lists.md).

## Create a domain or app list

> [!NOTE]
> Domain targeting applies only to **Web** and **Mobile Web** impressions and does not apply to **Mobile App** impressions. If you have allowed your campaign to serve on mobile apps while targeting a domain list, the campaign will be unrestricted when buying mobile app inventory unless you have also applied App List targeting. To avoid serving on mobile app inventory, switch the **Apps Placements** toggle in your campaign's targeting profile to OFF.
1. Select **Admin** > **Inventory Lists** 
1. Click **New** 
1. In the **Create List** dialog, enter the **Name** and **Description** of the domain or app list.
1. In the **Add domains & app** section, either:
    1. Select **Copy and paste domains & apps** into the text area OR
    1. Select **Import from file**, and select text file to upload.
        > [!NOTE]
        > Excel files are not allowed.
1. Click **Create List** to target this domain or app list in a campaign.

> [!NOTE]
> - Domains and subdomains must be separated by a comma, space, or line break. See below for [examples for domains and subdomains formatting](#examples-for-domains-and-subdomains-formatting).
> - Wildcards (for example, `msn.*`) are not allowed in domain lists. However, a top-level domain (TLD) can be added to a domain list by entering it into the domain list text field without leading periods. For example, to block the `.fr` domain, add `fr` without the period to the list.
> - To restrict or include an entire TLD, enter that TLD in your list. Do not include the leading period "." For example, if you want to serve on any site in the `.de` TLD, you should add `de` (with no leading period) to your allowlist.
> - You can only target domains (`test4.com`) or sub-domains (`review.test4.com`); you can't target specific directories within domains. For example, targeting `test4.com/review` is not supported.
> - If you target a domain, it automatically targets all subdomains. For example, targeting `test4.com` automatically targets `review.test4.com.`
> - Domains which begin with `"www"` will have the `"www"` substring stripped out before being stored in our system. For example, `"www.example.org"` will be shortened to `"example.org"`.

<!--
1. Go to **Network** > **Inventory** > **Targeting Lists**.
1. Click **Create New** > **Domain List** OR select the **Domain Lists** tab and click **+ New**.
1. In the **New Domain List** dialog, enter the **Name** and **Description** of the domain list.
1. In the **Domains** section, either:
    - Select **Enter text** and copy and paste domains into the text area OR
    - Select **Upload a file**, click **Select File**, and select text file to upload.
        > [!NOTE]
        > Excel files are not allowed.
1. Click **Save**. To target this domain list in a campaign, see [Domain Targeting](domain-targeting.md).
-->



### Examples for domains and subdomains formatting

Examples of acceptable formatting include:

- ```
  test1.com,review.test2.com,test3.com
  ```

- ```
  test1.com review.test2.com test3.com
  ```

- ```
  test1.com
  review.test2.com
  test3.com
  ```

- ```
  test1.com,
  review.test2.com,
  test3.com
  ```
<!--
## Create an app list

1. Go to **Network** > **Inventory** > **Targeting Lists**.
1. Click **Create New** > **App List** OR select the **App Lists** tab and click **+ New**.
1. In the **New App List** dialog, enter the **Name** and **Description** of the app list.
1. In the **Apps** section, either:
    - Select **Enter text** and copy and paste app IDs into the text area OR
    - Select **Upload a file**, click **Select File**, and select text file with app IDs to upload.

      > [!NOTE]
      > The app IDs should be separated by commas or line breaks.

1. Click **Save**. To target this app list in a campaign, see [App Targeting](app-targeting.md).
-->

### App bundle ID (App ID)

An app bundle ID (or app ID) is just a unique identifier for a specific app. App IDs are defined differently depending on whether the app runs on iOS or Android:

- Every iOS app has a unique iTunes ID
- Every Android app has a unique Android Package Name

### How to find app IDs

To find the IDs for an Android or IOS app, find the app's detail page - the easiest way is to do a web search. The URL of the app store's detail page will show the app's ID.

For example, here are the detail pages for the "Candy Crush" app:

- Google Play: `https://play.google.com/store/apps/details?id=com.king.candycrushsaga`
  - ID: com.king.candycrushsaga
- iTunes: `https://itunes.apple.com/app/apple-store/id553834731`
  - ID: 553834731

### How to choose which apps to target

To identify specific mobile apps to target, we recommend targeting the region you're interested in, activating your campaign, and after a few days running the [Site Domain Performance](site-domain-performance.md) report, which will show you the apps that you've been reaching. You can then update your campaign targeting to include or exclude specific apps to meet your needs.

## Related topics

- [Domain Targeting](domain-targeting.md)
- [App Targeting](app-targeting.md)
- [Update a Domain List or App List](update-a-domain-list-or-app-list.md)
- [Explore Domain Lists or App Lists](explore-domain-lists-or-app-lists.md)
