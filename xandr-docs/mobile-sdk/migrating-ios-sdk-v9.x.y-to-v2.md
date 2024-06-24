---
title: Migrating iOS SDK v9.X.Y to v2
description: Learn how to integrate the AppNexusSDK into your iOS app using CocoaPods, Carthage, or XCFramework with detailed instructions.
ms.custom: ios-sdk
ms.date: 10/28/2023
---

# Migrating iOS SDK v9.X.Y to v2

This page describes how to integrate our iOS SDK within your Xcode project, as well as how to display ads in your app. For instructions on displaying different ad types, see our respective [Ad Unit](ios-sdk-ad-units.md) pages.

## Requirements

- This SDK requires Xcode version 15.0 or higher.
- Your app should target iOS 12.0 or higher.
- In order to show ads, you must have a valid Xandr placement ID and member ID.

## Installation

There are four ways to get our SDK:

- [CocoaPods](ios-sdk-integration-instructions.md#cocoapods)
- [Carthage](ios-sdk-integration-instructions.md#carthage)
- [XCFramework](ios-sdk-integration-instructions.md#xcframework)
- [Swift Package Manager](ios-sdk-integration-instructions.md#swift-package-manager)

### CocoaPods

If you are unfamiliar with CocoaPods review their [documentation](https://cocoapods.org/). Once you have CocoaPods installed:

1. Use Terminal or your command line editor of choice, navigate to the root directory of your project and create a podfile.

      ```
      pod init
      ```

1. Using a text editor, open the newly created podfile. Set the platform version to 12.0 and add `pod`AppNexusSDX`` to the target.

    ```
    # iOS: Podfile config to include our SDK
    platform :ios, '12.0'
    project 'FunBanner'
    target 'FunBanner' do
      pod 'AppNexusSDK'
    end

1. Save your changes and return to the Terminal and enter:

    ```
    pod install
    ```

1. CocoaPods downloads the Xandr SDK and creates a workspace (`.xcworkspace`) in the project directory. If your project is currently open, close it and open the xcworkspace.

### Carthage

If you are unfamiliar with Carthage review their [documentation](https://github.com/Carthage/Carthage/blob/master/README.md).
Once you've installed Carthage on your computer, follow these steps:

1. Open the Terminal app and navigate to the root directory of your project. Create a Cartfile.

   ```
   touch Cartfile
   ```

1. Open the Cartfile in Xcode to edit it.

    ```
    open -a Xcode Cartfile
    ```

1. Add the following lines to the Cartfile.

    ```
    # iOS: Carthage config to include our SDK
    binary "https://acdn.adnxs.com/mobile/mtest/adoreleasetest/9.0.0/carthage/AppNexusSDK.json"
    binary "https://acdn.adnxs.com/mobile/mtest/adoreleasetest/9.0.0/carthage/OMSDK_Microsoft.json"
    ```

    > [!TIP]
    > You can use editor's other than Xcode to edit the Cartfile but be aware that other editing programs such as TextEdit might automatically include smart quotes instead of straight quotes. Carthage does not recognize content within smart quotes and not perform correctly.

1. Save the Cartfile. Run the following command to update dependencies:

      ```
      carthage update --use-xcframeworks
      ```

1. To use `AppNexusSDK` SDK, add the `AppNexusSDKDynamic.xcframework` and `OMSDK_AppNexus.xcframework` to the **Embedded Binaries** section:
    - Navigate to **Target** → **General** → **Embedded Binaries**.
    - Click the `+` icon and select the `.xcframework` files.
    - If you are using Carthage for an application, select **Embed & Sign**. Otherwise select **Do Not Embed**.

## XCFramework

Download and unzip the latest version of our [SDK](https://adsdkdevstand.azureedge.net/dev/mobile/mtest/adoreleasetest/9.0.0-alpha.9/static/sdks.zip) from our CDN.

This file will contain the following four frameworks and two mediation adapters. Ensure you are only using the framework that best suits your needs. The AppNexusSDK is our recommendation for general use.

| Framework | Description |
|---|---|
| AppNexusSDK | Supports all ad types. |
| AppNexusNativeSDK | This framework only supports native ads on **iOS**.|
| AppNexusNativeMacOSSDK | This framework only supports native ads on MacOS. |
| ANSmartAdapter | A mediation adapter for Smart Ad Server.|
| ANGoogleAdapter | A mediation adapter for Google's AdMob.|
| ANFacebookCSRAdapter | A mediation adapter for Facebook Audience Network. |
| ANSDKResources.bundle | This contains necessary files which or SDK utilizes. |

1. Open the app’s Xcode project or workspace.
1. Go to the app target’s **General** configuration page.
1. To use the `AppNexusSDK` SDK, add the `AppNexusSDK.xcframework` and `ANSDKResources.bundle` to the Embedded Binaries section:
    1. Navigate to your project's Target settings.
    1. Navigate to **Target** > **General** > **Embedded Binaries**.
    1. Click the `+` icon and select the `.xcframework` and `.bundle` files.

    :::image type="content" source="media/choose-option-migrate-iOS-SDK-v9-v2.png" alt-text="A screenshot that shows how to choose options for adding the files.":::

    :::image type="content" source="media/choose-option2-migrate-iOS-SDK-v9-v2.png" alt-text="A screenshot that shows how to choose frameworks, libraries, and embedded content.":::

## Swift Package Manager

1. Copy the URL https://github.com/appnexus/mobile-sdk-ios-spm and enter it into your Xcode project's Package Dependencies. You can install either the latest released version or the main branch.

   :::image type="content" source="media/swift-package-manager.png" alt-text="A screenshot that shows how you copy the url and and enter it into your Xcode project's Package Dependencies.":::

   :::image type="content" source="media/swift-package-manager-support-ios-sdk.png" alt-text="A screenshot that shows how Swift Package manager support for IOS SDKs.":::

## Swift Package Manager - Google AdMob Mediation adapters
