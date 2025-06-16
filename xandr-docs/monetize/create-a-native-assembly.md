---
title: Create a Native Assembly
description: In this article, find information on how to create or modify a native assembly.
ms.date: 10/28/2023
---

# Create a native assembly

## Overview

You can easily modify Native Assembly templates that contain pre-configured native creative asset specifications or create your own from scratch by selecting one of the following template categories: 
- **Adaptive renderer:** The Adaptive renderer is a Microsoft-defined renderer that optimizes asset requests and styling to enhance performance. 
- **Custom template:** A custom template lets you create a renderer completely from scratch or modify pre-designed templates, giving you complete control over assets and styling for your native inventory. 


### Adaptive renderer 

- The Adaptive renderer name is prepopulated. 
- Select **Next** to associate placements with the Adaptive renderer. 
- Select **Add Filter** to filter placements by publisher. This displays all placements associated with the selected publisher.  
    - If you would like to search for and associate placements under a specific publisher, select the **Add Filter** placements by publisher checkbox. 
    - If you would like to search for and associate placements across multiple publishers, leave the **Add Filter** placements by publisher checkbox deselected and proceed to substep f. 
    - Enter a publisher in the **Select a publisher to filter placement options** search field. 
    - Select the corresponding publisher from the search results that display. 
    - Only placements that are available for these specific publishers will display when searching and associating placements. You must associate the native assembly to a placement in order for it to go live. For more information, see [Create a Placement](create-a-placement.md). 
    - Enter a placement name or ID in the **Search placements name or ID** search field. 
    - Search results will automatically display. 
    - Select any of the checkboxes for the corresponding placements that display. 
- The selected placements will appear in the right pane. For more information, [Create a Placement](create-a-placement.md). 
> [!NOTE]
> You must associate the renderer with at least one placement for it to apply to your inventory. 
- Select **Next** to review and enable the Native Assembly renderer. 
    - In the top right corner of the screen, select the three horizontal dots to: 
        - Enable an **Image Floor Price** for each placement if applicable. 
        - Enable a **Video Floor Price** for each placement if applicable. 
    - For more information about floor prices, see [Floor Prices](floor-prices.md) and [Deal Auction Mechanics](deal-auction-mechanics.md).
- In the **Enable server-side Native Assembly** section for associated placements, review the placements you want to associate with the renderer. You can either select each placement individually and select toggle to enable server-side application of your renderer for those placements or you can toggle **Enable server-side Native Assembly** to enable server-side application of your renderer in bulk for all the placements. 
> [!NOTE] 
> Enable the server-side Native Assembly toggle only if you're using Native Assembly with a third-party ad server. If you're using Monetize Ad Server with AST.js or the Mobile SDK, do not enable server-side Native Assembly. For more information, see Learn more 
- Select **Save and exit**

### Custom template 

- Select a pre-configured Native Assembly template, which you can modify, or create your own from scratch by doing one of the following: 
    - In the **Basics** section, enter the Name of your renderer 
    - From the dropdown menu, select the size you want the rendered ad to be. 
    - You can select a size from the dropdown or enter a custom width and height representing the ad unit the renderer should serve. 
    - Based on the rendered size selected, a couple of recommended predefined templates are displayed which represent our suggestions for your chosen size. You can choose a template that gets you started quickly, which can then be customized.  
    - Select a pre-configured Native Assembly or create your own by checking the radio button. 
    - Select **Show all templates** to view and browse all available templates  
    - Select **Next** to move to the **Setup** screen. 
    - In the **Creative Asset Specifications** section, select Add asset if you want to add additional assets for the renderer. All pre-configured templates contain preset creative asset specifications. Although these are recommended configurations, they can be modified. For example, if you want to only serve creatives that contain a particular asset specification, set it to **Required**, which will limit eligible demand. Otherwise, set the creative asset specification to **Optional**. You can also remove any creative asset specification at any time by clicking the **trash** symbol. 
    > [!NOTE]
    > For the best Microsoft Advertising marketplace performance, third-party ad server publishers should refrain from adding video assets and any custom native assets to their specifications. 

    > [!IMPORTANT]
    > It is a marketplace policy to use all returned assets. If you do not want your renderer to use a configured asset, please remove the asset from the request and HTML before continuing. Native Assembly detects assets included in the HTML, and will warn you if an asset is not present. If the asset is handled in custom JavaScript, you can accept the warning and continue.  
    - Toggle the **Edit code** button to add or update the HTML, CSS, and JavaScript in the designated text boxes. To ensure that you're following our native assembly renderer best practices, see [Native Assembly Renderer Best Practices](native-assembly-renderer-best-practices.md). 
    > [!NOTE] 
    > If you remove a creative asset specification, the HTML code won't automatically reflect this change, so you'll have to manually remove the corresponding HTML from the HTML text box to avoid rendering errors. 
    - On the right, you can see a preview of the renderer as currently specified, which can be resized. 
    - You can specify which asset specifications should appear in the **Preview** window by clicking one of the following buttons: 
        - **Video and Text:** Only the sample video and text, such as the title, will display in the Preview window when this button is selected. 
        - **Main Image and Text:** Only the sample main image and text, such as the title, will display in the **Preview** window when this button is selected. 
        - **Text Only:** Only sample text, such as the title, will display in the **Preview** window when this button is selected. 
        - **All:** All sample assets (video, main image, and any text) will display in the Preview window when this button is selected. 
    - You can specify whether the **AdChoices** icon should appear in the **Preview** window by checking the **With privacy URL** checkbox which would ensure the AdChoices icon will be appended to the creative in the **Preview** window when this button is checked. 
    - Select **Next** to associate placements with the renderer. 
    - Select **Add Filter** to filter placements by publisher. This displays all placements associated with the selected publisher.  
        - If you would like to search for and associate placements under a specific publisher, select the **Add Filter** placements by publisher checkbox. 
        - If you would like to search for and associate placements across multiple publishers, leave the **Add Filter** placements by publisher checkbox deselected and proceed to substep f. 
        - Enter a publisher in the **Select a publisher to filter placement options** search field. 
        - Select the corresponding publisher from the search results that display. 
        - Only placements that are available for these specific publishers will display when searching and associating placements. You must associate the native assembly to a placement in order for it to go live. For more information, see [Create a Placement](create-a-placement.md). 
        - Enter a placement name or ID in the **Search placements name or ID** search field. 
        - Search results will automatically display. 
        - Select any of the checkboxes for the corresponding placements that display. 
    - You can see the selected placements on the right section of the pane. For more information, see [Create a Placement](create-a-placement.md).
    > [!NOTE]
    > You must associate the renderer to at least one placement in order for it to apply to your inventory. 
    - Select **Next** to review and enable the Native Assembly renderer. 
        - In the top right corner of the screen, select the three horizontal dots to: 
            - Enable an **Image Floor Price** for each placement if applicable. 
            - Enable a **Video Floor Price** for each placement if applicable. 
        - For more information about floor prices, see [Floor Prices](floor-prices.md) and [Deal Auction Mechanics](deal-auction-mechanics.md).
    - In the **Enable server-side Native Assembly** function on associated Placements section, you can select individual placements to be enabled for server-side application of the associated renderer. 
    > [!NOTE] 
    > Enable the **Enable server-side Native Assembly** toggle if you want to use Native Assembly with a third-party ad server. If you use Monetize Ad Server with AST.js or Mobile SDK, do not enable server-side Native Assembly for native requests. For more information, see [Native Assembly](native-assembly.md).
- Select **Save and exit**


## Related topics

- [Configuring a Native Assembly](configuring-a-native-assembly.md)
- [Native Creative Asset Specifications](native-creative-asset-specifications.md)
- [Enable Native Assembly for the Server Side](enable-native-assembly-for-the-server-side.md)


<!--
You can easily modify native assemblies that contain pre-configured native creative asset specifications or create your own from scratch.

1. Select a pre-configured native assembly or create your own by doing one of the following:
    - Click the **Select** button from one of the corresponding pre-configured assemblies.

      > [!NOTE]
      > We offer a variety of pre-configured native assembly types such as carousel and video. You can filter by creative asset specification to find a specific pre-configured native assembly.

    - Click the **Select** button from the **Create From Scratch** tile.

    The **Native Assembly** > **Setup** screen displays.

1. Enter a new name for the native assembly.

1. Associate placements with the native assembly by doing the following:
    1. If you would like to search for and associate placements under a specific publisher, select the **Filter placements by publisher** checkbox.

        If you would like to search for and associate placements across multiple publishers, leave the **Filter placements by publisher** checkbox deselected and proceed to substep **d**.

    1. Enter a publisher in the **Select a publisher to filter placement options** search field.

    1. Select the corresponding publisher from the search results that display.

        Only placements that are available for these specific publishers will display when searching and associating placements. You must associate the native assembly to a placement in order for it to go live. For more information, see [Create a Placement](create-a-placement.md).

    1. Enter a placement name or ID in the **Choose placements** search field.

        Search results will automatically display.

    1. Select any of the checkboxes for the corresponding placements that display.

        The selected placements will display under the **Choose placements** search field.

    1. Enter a **Main Image Floor Price** for each placement if applicable.

    1. Enter a **Video Floor Price** for each placement if applicable.

        For more information about floor prices, see [Floor Prices](floor-prices.md) and [Deal Auction Mechanics](deal-auction-mechanics.md).

1. Click the **Additional Specifications** menu in the **Creative Asset Specifications** section to add and configure creative asset specifications for the native assembly.

    > [!TIP]
    > For the best Microsoft Advertising marketplace performance, third-party ad server publishers should refrain from adding video assets and any custom native assets to their native assemblies.

    All pre-configured native assemblies contain preset creative asset specifications. Although these are recommended configurations, they can be modified. For example, if you want to only serve creatives that contain a particular asset specification, set it to **Required**, which may limit your demand. Otherwise, set the creative asset specification to **Optional**. You can also remove any
    creative asset specification at any time by clicking the **X**.

    > [!NOTE]
    > If you remove a creative asset specification, the HTML code on the **Renderer** tab won't automatically reflect this change, so you'll have to manually remove the corresponding HTML from the **HTML** text box.

1. Click the **Renderer** tab to add or update the HTML, CSS, and Javascript in the designated text boxes.

    To ensure that you're following our native assembly renderer best practices, see [Native Assembly Renderer Best Practices](native-assembly-renderer-best-practices.md).

1. Use the **Preview** window on the right to ensure that no additional changes are needed.

1. Use the **Preview Settings** to:
    - resize the **Preview** window.

      > [!NOTE]
      > Changing the **Preview** window size doesn't affect the renderer code.

    - specify which asset specifications should appear in the **Preview** window by clicking one of the following buttons if you've selected the video and image asset specifications from the **Creative Asset Specifications** section:
      - **Video and Text**: Only the sample video and text, such as the title, will display in the Preview window when this button is selected.
      - **Main Image and Text**: Only the sample main image and text, such as the title, will display in the Preview window when this button is selected.
      - **Text Only**: Only sample text, such as the title, will display in the Preview window when this button is selected.
      - **All**: All sample assets (video, main image, and any text) will display in the Preview window when this button is selected.

    - specify whether the **AdChoices** icon should appear in the **Preview** window by clicking one of the following buttons from the **Privacy URL Specifications** subsection:
      - **With Privacy URL**: The AdChoices icon will be appended to the creative in the Preview window when this button is selected.
      - **Without Privacy URL**: The AdChoices icon won't be appended to the creative in the Preview window when this button is selected.

    > [!NOTE]
    > Since various combinations of native assets can serve on the same placement when using a flexible renderer, it's important to preview your asset specifications to see how the renderer will handle your placements and native assets.

1. Do one of the following:
    1. Save all changes by clicking the **Save** button.
    1. Save all changes and duplicate the native assembly by clicking the arrow next to the **Save** button and clicking **Save and duplicate**.

    The native assembly is now available from the **Native Assembly Gallery** screen. If you've duplicated the native assembly, the current screen refreshes so that you can make the necessary updates. Use steps 2 - 7 outlined above to make the necessary updates.


## Related topics

- [Configuring a Native Assembly](configuring-a-native-assembly.md)
- [Native Creative Asset Specifications](native-creative-asset-specifications.md)
- [Enable Native Assembly for the Server Side](enable-native-assembly-for-the-server-side.md)
-->