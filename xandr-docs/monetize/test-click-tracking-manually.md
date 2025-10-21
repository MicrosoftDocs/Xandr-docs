---
title: Microsoft Monetize - Test Click Tracking Manually
description: In this article, learn how to manually test click tracking.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Test click tracking manually

You can manually test click tracking if strange creative behavior or UI issues cause the click tracking test within the UI to be unreliable.

> [!TIP]
> **Developer tools:** Familiarize yourself with Chrome developer tools (under **More Tools**, go to **Developer tools**) which will show you elements of the page and network calls.
> [!NOTE]
> Ensure the macros are in place by taking a quick look at your code to confirm that `${CLICK_URL}` or `${CLICK_URL_ENC}` appears.

1. Preview the creative by accessing the `https://creative-preview-an.com/cached/creative/insert creative id here` webpage.

    Insert the appropriate creative ID to the end of the URL replacing "`insert creative id here`". For example: `https://creative-preview-an.com/cached/creative/196745`.

1. Then **right click** > **Inspect** > **Network** tab.

1. Click on the **Settings** (gear icon) in the top right of dev tools.

1. Enable the **"Auto-open DevTools for popups"**, under **Preferences** > **Global**.

1. Click on the **Creative**.

1. The landing page will open and the dev tools should automatically open in the new tab.

1. Search for "**click**" in the **Network** tab.

1. You should see a call similar to the following: `https://nym1-ib.adnxs.com/click2?`. The creative will start tracking clicks.

    > [!NOTE]
    > If you see this above call only once after clicking the creative, then your creative's click tracking is working properly. The call should only occur once per click. If the call appears more than once, then your creative is experiencing a click-tracking problem that gives it an artificially higher CTR.

## Related topic

[Click Tracking](click-tracking.md)
