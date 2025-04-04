---
title: Microsoft Invest - Video Targeting
description: This article provides instructions for targeting video inventory based on the position, playback method, and player width.
ms.date: 10/28/2023
---

# Microsoft Invest - Video targeting

You can target video inventory based on the playback method, player size, and position.

> [!NOTE]
> Video content targeting requires content metadata integration. Please contact your Microsoft account manager for enablement. If you are not integrated with video content metadata, values passed in content object fields will not be transmitted to DSP partners.

In the **Viewability & Environment Targeting** section of a line item, select the pencil icon next to **Video Player**.

You can target video creatives in any or all of the following ways:

- [Microsoft Invest - Video targeting](#microsoft-invest---video-targeting)
  - [Target video inventory by position or context](#target-video-inventory-by-position-or-context)
  - [Target video inventory by playback method](#target-video-inventory-by-playback-method)
  - [Target video inventory by player width](#target-video-inventory-by-player-width)

> [!NOTE]
> You should avoid using both VAST creatives and in-banner or interstitial video creatives within the same video campaign. An in-banner or interstitial video creative will not serve when you target by position. Setting any of the three video targeting parameters (i.e., **Playback Method**, **Player Size**, or **Position**) will restrict inventory to only those that satisfy the specified parameters and thus significantly limit your delivery potential.
>
> By default, you will target all playback methods, player sizes and roll positions. However, you can narrow your targeting.

## Target video inventory by position or context

The options available to target inventory by position, also called context:

- **Instream** - Video ads are embedded within a video player.
  - **Pre-roll** - Inventory that hosts video creatives that play before the user selected video of choice.
  - **Mid-roll** - Inventory that hosts video creatives that play in the middle of the user selected video of choice.
  - **Post-roll** - Inventory that hosts video creatives that play after the user selected video of choice.
  - **No roll position defined** - Target inventory where no position information has been provided.
- **Interstitial** - Inventory that covers the entire screen or a portion of it and remains visible at all times while displayed (cannot be scrolled out of view).
- **In-article** - Inventory that dynamically loads and plays between paragraphs of editorial content, presenting a standalone branded message.
- **In-banner** - Inventory within a web banner, using the banner space to deliver a video experience instead of static or rich media formats. It relies on existing display ad inventory for its delivery.
- **In-feed** - Inventory placed within content, social, or product feeds.

## Target video inventory by playback method

You can target inventory that accepts creatives with the following playback methods:

- **Auto-play, sound on** - Video creative starts playing with sound on as soon as the page loads.
- **Auto-play, sound off** - Video creative starts playing with sound off as soon as the page loads. Sound comes on when the user clicks on the creative.
- **Auto-play, sound unknown** - Video creative starts playing as soon as the page loads, but no sound information is specified.
- **Click-to-play** - Video creative is static on the page till the user clicks to play.
- **Mouse-over** - Video starts playing when the user moves the mouse over the creative.
- **No playback method provided** - Target inventory where no initiation method information is provided (e.g., YouTube inventory).

> [!NOTE]
>
> - For maximum delivery and reach, we recommend that you include **No initiation method provided** in your targeting since some inventory (such as Google Ad Manager) is not classified.
> - Playback method targeting is not available for Google Ad Manager (181).

## Target video inventory by player width

Player inventory is available across all supply types (web, mobile web, and mobile app). The following player sizes are available to target:

- **Large -** primarily large-format web inventory (minimum width of 640 pixels)
- **Medium -** includes most smartphone player inventory for mobile apps (minimum width of 320 pixels, maximum width of 639 pixels)
- **Small -** primarily in-banner inventory (maximum width of 319 pixels)
- **No player width provided**

> [!TIP]
> For maximum delivery and reach, we recommend that you include **No player width provided** in your targeting, because some inventory (such as Google Ad Manager) is not classified.

You can either select the graphic to make a selection or select the appropriate checkbox.
