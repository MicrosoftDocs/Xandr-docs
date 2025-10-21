---
title: Publisher Notifications for Outstream Video Events
description: In this article, learn how notifications are sent to the publisher when video and ad-related events occur and how to implement them.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Publisher notifications for outstream video events

Microsoft Monetize can provide notifications to the publisher when video and ad-related events occur in Microsoft Advertising players. This page describes how these notifications work and how to implement them.

## Prerequisites

This page assumes that you are familiar with certain Microsoft Advertising features, such as [Microsoft Advertising's seller tag (AST)](../seller-tag/seller-tag.md).

## How outstream publisher notifications work

Generally speaking, the process works like this: a publisher specifies an optional callback function as part of the options that are passed into Microsoft Advertising code. Once this callback function is specified, our code then calls this callback whenever important events occur while the ad is being rendered - these may include video reporting events, as well as non-reportable events such as AdLoaded or custom AdUnit events. In addition:

- The field that is added to the "options" that is passed into Microsoft Advertising code, which identifies the callback function.
- The name of field is `"cbNotification"`. In the JSON, this field would look something like `"cbNotification" : callbackFunction` where `callbackFunction` is the name of the publisher function.

> [!TIP]
> Publishers can also put an inline function as the value for `cbNotification` if they prefer.

Outstream version 1.1.10 includes support for a new feature which allows publishers to receive notifications whenever any VAST, VPAID or custom Ad Unit event occurs during the rendering of an Outstream ad. This feature is enabled by the inclusion of a specific option in the set of `rendererOptions` specified in the AST defineTag statement on the publisher's page. This new option names a publisher's callback function which will be called whenever any of the events occur during the running of an Outstream ad.

## To enable callback notifications

### Step 1

Add the field `cbNotification` to the set of `rendererOptions` specified in the AST `defineTag` statement for the Outstream placement.

### Step 2

Set the value of the `cbNotification` field to the name of a publisher-defined function that is to receive all the notifications.

### Example

```
apntag.defineTag({
    tagId : 1234567,
    sizes: [1,1],
    targetId: 'apn_ad_45xxxxxx',
    video: {
        frameworks: [1,2]
    },
    rendererOptions: {
        cbNotification: outstreamNotification
    }
});
```

## Callback function implementation

The callback function provided by the publisher should have the following arguments: (type, name, id)

### type

- A String which identifies the source of the event.
- Possible values:
  - "VAST"
  - "VPAID"
  - "AdUnit" (for non-VAST, non-VPAID events that occur in Outstream)

### name

- A string that identifies the specific event being reported
- For "VAST" and "VPAID, the name will be identical to standard events defined in those specs
- For "AdUnit", the event names can be one of the following:
  - "expand" - dispatched when Outstream expands the first time
  - "collapse" - dispatched when Outstream collapses at the end

### id

A string that identifies a specific Outstream ad

### Example

```
   function outstreamNotification (type, name, id) {
       console.log("Notification received, type=" + type +
           "event=" + name + " id=" + id);
       // put your code here
   };
```

## Sample source code

Below is some sample HTML source code, showing a real outstream seller tag in action:

```
<html>
<head>
  <script type="text/javascript">

    // AST SETUP
    // create empty apntag object if it doesn't exist
    var apntag = apntag || {};

    // create a queue on the apntag object        
    apntag.anq = apntag.anq || [];

    // load ast.js asynchronously
    (function() {
        var d = document, scr = d.createElement('script'), pro = d.location.protocol,
        tar = d.getElementsByTagName("head")[0];
        scr.type = 'text/javascript';  scr.async = true;
        scr.src = ((pro === 'https:') ? 'https' : 'http') + '://acdn.adnxs.com/ast/ast.js';
        if(!apntag.l){apntag.l=true; tar.insertBefore(scr, tar.firstChild);}
    })();

    // push commands to loading queue, to allow for async loading
    apntag.anq.push(function() {

        // set global page options
        apntag.setPageOpts({
            member: 3,
            targetingParams: {
            }
        });

        // define ad tag
        apntag.defineTag({

            targetId: 'apn_ad_40954389053',
            tagId: 14, // tagId is placement ID
            sizes: [1, 1],
            allowedFormats: ['video'],
            targetingParams: {},
            video: {
                frameworks: [1,2]
            },
            // the rendererOptions object is passed to the renderer which writes the outstream video container to the page
            rendererOptions: {
                playerTechnology: [
                    'flash',
                    'html5'
                ],
                adText: 'Ad',
                showMute: true,
                showVolume: true,
                showProgressBar: true,
                allowFullscreen: true,
                cbNotification: outstreamNotification,
                skippable: {
                    videoThreshold: 15,
                    videoOffset: 5,
                    skipLocation: 'top-left',
                    skipText: 'Video can be skipped in %%TIME%% seconds',
                    skipButtonText: 'SKIP'
                }
            }
        });

        // start loading tags
        apntag.loadTags();
    });

    // outstream callback for notifications
    function outstreamNotification (type, name, id) {
        console.log("Notification received, type=" + type +
            "event=" + name + """ id=""" + id);
        // put your code here
    };
  </script>
</head>
<body>

  <h1>OUTSTREAM SAMPLE PAGE</h1>
  <p><button onclick="apntag.refresh()">Refresh All</button></p>

  <script type="text/javascript">
  <p>apntag.anq.push(function() {</p>
    <p>// signal to script that this DOM element has been loaded and is ready to be populated with an ad</p>
    <p>apntag.showTag('apn_ad_40954389053');</p>
    <p>});</p>
    </script>

</body>
</html>
```
