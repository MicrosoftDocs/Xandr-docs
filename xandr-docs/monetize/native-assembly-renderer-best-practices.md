---
title: Native Assembly Renderer Best Practices
description: Explore how Edit code toggle stores HTML, CSS, and JavaScript for native assembly. Changes auto-reflect in the Preview window.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Native assembly renderer best practices

The **Edit code** toggle stores the HTML, CSS, and Javascript code associated with the native assembly. Any changes made on the **Edit code** toggle will automatically be reflected in the **Preview** window.

Here's a list of tips and important notes related to the **Edit code** that you should keep in mind:

- If you removed any of the existing standard and custom creative asset specifications on the **Setup** tab, the HTML code on the **Edit code** toggle won't automatically reflect this change, so manually remove the corresponding HTML and/or placeholders from the **HTML** text box on the **Edit code** toggle.
- Ensure that the `[%impressionTrackers%]` object placeholder appears in the **HTML** field or **Javascript** field on the **Edit code** toggle. If it doesn't, you'll have to manually add it so that impression trackers can be tracked. If your renderer or website uses another impression tracking method, you don’t have to add the `[%impressionTrackers%]` object placeholder to the **HTML** field or Javascript field. However, when saving your native assembly, a warning dialog will appear where you can select the **I will manage my impression trackers from my own website** checkbox, which gives you the ability to save the native assembly without adding the `[%impressionTrackers%]` object placeholder.
- Adding `<script>` tags directly in the **HTML** text box won't work. You must use the designated **Javascript** text box to write js code. The **Javascript** text box doesn't require the user to use **HTML** `<script>` tags.
- Following [IAB's standard for video creatives](https://www.iab.com/wp-content/uploads/2017/08/IABNewAdPortfolio_FINAL_2017.pdf#page=20), by default, native videos will play when the user clicks the play button. If you want the video to play automatically with the audio muted, remove the `//` from these commented lines under `function vidCallback()` in the **Javascript** text box on the **Edit code** toggle:
  
  ```
  //initialPlayback: 'auto',
  //initialAudio: 'off'
  ```

## Related topic

[Configuring a Native Assembly](configuring-a-native-assembly.md)
