---
title: Microsoft Curate - Dynamic Consent Updates for Universal Pixel
description: Learn to implement dynamic consent updates for Universal Pixel in Google Tag Manager using JavaScript triggers and event-driven interactions.
ms.date: 03/04/2025
ms.author: shsrinivasan
---

# Microsoft Curate -  Dynamic consent updates for Universal Pixel

The following steps and code snippets illustrate how you can dynamically update the consent state based on user interactions using JavaScript functions and event listeners such as `onclick` triggers.  

Note that these are not the only ways to achieve this, and your specific setup may require a different approach.

## Example 1: Control Universal Pixel Fires with Google Tag Manager’s consent requirement

> [!IMPORTANT]
> This approach may prevent Universal pixel from measuring events in the absence of consent. Universal pixel can be loaded on pages with the applicable consent settings to avoid the use of personal data without consent.

See [Example 3](#example-3-update-consent-modes-using-custom-events) for more details.

If you use a [consent management platform (CMP) that supports Google’s Consent Mode](https://support.google.com/tagmanager/answer/10718549?hl=en#consent-initialization-trigger) feature, you may choose to fire Microsoft’s Universal pixel only when a user has granted consent for specific purposes.

### Add consent signal to UP tag

1. Go to **Tags** > **New**.  
1. Select **Tag Configuration**.  
1. Select **Custom HTML**.  
1. Copy and paste the following JavaScript code, replacing `REPLACE_WITH_UP_PIXEL_ID` with your Tag ID:  

    ```html

    <script>
    !function(e,i){if(!e.pixie){var n=e.pixie=function(e,i,a){n.actionQueue.push({action:e,actionValue:i,params:a})};n.actionQueue=[];var a=i.createElement("script");a.async=!0,a.src="//acdn.adnxs.com/dmp/up/pixie.js";var t=i.getElementsByTagName("head")[0];t.insertBefore(a,t.firstChild)}}(window,document);
    pixie('consent', 'default', { 'ad_storage': 'granted' });
    pixie('init', 'REPLACE_WITH_UP_PIXEL_ID');
    pixie('event', 'PageView');
    
    </script>
    <noscript><img width="1" height="1" style="display:none;" src="https://ib.adnxs.com/pixie?pi=REPLACE_WITH_UP_PIXEL_ID&e=PageView&script=0&consent=1" /></noscript>

    ```

1. Select **Triggering** and choose **All pages**.  
1. Save the template.  

### Edit Universal Event Tracker consent settings

1. Go to **Tags** in GTM and select the tag you created.  
1. Choose **Tag Configuration** and edit the existing tag.  
1. Expand **Advanced Settings**.  
1. Expand the **Consent Settings** section.  
1. Select **Require additional consent for tag to fire**.  
1. Select the necessary purposes, such as `ad_storage`.  
1. Save your changes.  

:::image type="content" source="media\up-custom-html.png" alt-text="Screenshot that explains Universal Event Tracker consent settings.":::


> [!NOTE]
> This setting ensures that Universal pixel only measures events when users grant consent for `ad_storage` via your CMP provider.

## Test and Debug

- **Preview Mode in GTM:** Use GTM’s preview mode to test triggers and tags.  
- **Check the browser console:** Open the browser console to verify that consent updates are being pushed correctly.  

By following these steps, you can dynamically update consent settings based on user interactions, ensuring compliance and a user-friendly experience.  

## Example 2: Update Consent Modes using Triggers for button clicks

### Create User Interaction Triggers in GTM

You need to create triggers in GTM that fire when users interact with your consent banner (e.g., click "Yes" or "No").

#### Click trigger for "Yes"

1. Go to **Triggers** in GTM and create a new trigger.  
1. Select **Click - All Elements**.  
1. Choose **Some Clicks**.  
1. Select **Choose Built-In Variable** and select **Click ID**.  
1. Define the condition using the consent prompt button ID.  
1. Name the trigger (e.g., `Consent Granted Click`).  

#### Click trigger for "No"

Repeat the steps above for the **No** button, naming it `Consent Denied Click`.

#### Example consent banner HTML

```html
<div id="consent-banner">  
  <p>We use cookies to improve your experience. Do you accept?</p>  
  <button id="consent-yes">Yes</button>  
  <button id="consent-no">No</button>  
</div>  
```

#### Example Consent-Granted Trigger

:::image type="content" source="media\example-consent-granted-trigger.png" alt-text="Screenshot that shows the example of consent granted trigger.":::

### Create custom HTML tags for consent updates  

#### Custom HTML tag for granted consent

1. Go to **Tags** > **New**.  
1. Choose **Custom HTML Tag**.  
1. Add the following script:  

    ```html
    <script>
    pixie ('consent', 'update', { 'ad_storage': 'granted' });
   </script>

    ```

1. Set the **Triggering** to `Consent Granted Click`.  
1. Save and publish the tag.  

#### Custom HTML tag for denied consent

1. Repeat the steps above but use the following script:

   ```html
   <script>
   pixie ('consent', 'update', { 'ad_storage': 'denied' });
   </script>
   ```

1. Set the **Triggering** to `Consent Denied Click`.
1. Save and publish the tag.  

### Implement the consent banner

Ensure your consent banner HTML includes buttons with IDs or classes that can be used to identify elements for the GTM triggers.

## Example 3: Update consent modes using custom events  

### Send custom events on user choices to GTM's data layer

If your page already listens to user privacy choices and controls JavaScript, you can use custom events sent to GTM’s data layer as custom event triggers in your GTM workspace.

#### Example consent banner HTML

```html
<div id="consent-banner">  
  <p>We use cookies to improve your experience. Do you accept?</p>  
  <button id="consent-yes">Yes</button>  
  <button id="consent-no">No</button>  
</div>  
```

If your consent banner matches the example above, you can send a custom GTM event to GTM’s data layer as follows:

**Using jQuery:**

```javascript
$('#consent-yes').click(function() {
    dataLayer.push({'event': 'consent_granted'});
});
```

**Using JavaScript:**

```javascript
document.getElementById('consent-yes').addEventListener('click', function() {
    dataLayer.push({'event': 'consent_granted'});
});
```

### Create User Interaction Triggers in GTM

To track user interactions with your consent banner, create triggers in GTM that fire when users click **Yes** or **No**.  

### Create a click trigger for "Yes"  

1. In GTM, go to **Triggers** and create a new trigger.  
2. Select **Custom Event**.  
3. Enter a **descriptive event name**.  
4. Select **Some Custom Events**.  
5. Set **Event** as the variable type.  
6. Choose a condition operator and enter the **data layer event name** from your custom JavaScript function.  
7. Name the trigger (for example, **Consent Granted Click**).  

#### Create a click trigger for "No"  

Repeat the steps above for the **No** button (or its equivalent) and name the trigger (for example, **Consent Denied Click**).

### Create Custom HTML Tags for consent updates  

Create two Custom HTML tags in GTM to update the consent state based on user interaction.  

#### Custom HTML tag for granted consent

1. In GTM, go to **Tags** and create a new tag.  
1. Select **Custom HTML Tag**.  
1. Add the following script:  

   ```html
   <script> 
   pixie('consent', 'update', { 'ad_storage': 'granted' });

   ```

</script>

1. Set the Triggering to the "Consent Granted Click" trigger you created earlier.
1. Save and publish the tag.

#### Custom HTML Tag for Denied Consent

```html
<script>
pixie ('consent', 'update', { 'ad_storage': 'denied' });
</script>
```

Follow the same steps as in [Example 2](#example-2-update-consent-modes-using-triggers-for-button-clicks) to create custom HTML tags for `Consent Granted Click` and `Consent Denied Click`.

By implementing these methods, you can ensure compliance with user consent preferences dynamically through GTM.

## Related topics

- [Universal Pixel Service](..\digital-platform-api\universal-pixel-service.md)
- [Universal Pixel SDK](..\mobile-sdk\universal-pixel-sdk.md)
