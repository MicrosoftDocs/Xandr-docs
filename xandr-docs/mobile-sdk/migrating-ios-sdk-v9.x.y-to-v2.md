---
title: SDK integration instructions v9.1.0
description: Learn how to integrate the AppNexusSDK into your iOS app using CocoaPods, Carthage, or XCFramework with detailed instructions.
ms.custom: ios-sdk
---

# SDK integration instructions v9.x

This page describes how to integrate iOS Mobile SDK v9.x within your Xcode project, as well as how to display ads in your app. For instructions on displaying different ad types, see respective [Ad Unit](ios-sdk-ad-units.md) pages.

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
    binary "https://adsdkprod.azureedge.net/mobile/ios/releases/carthage/AppNexusSDK.json"
    binary "https://adsdkprod.azureedge.net/mobile/ios/releases/carthage/OMSDK_Microsoft.json"
    
    ```

    > [!TIP]
    > You can use editor's other than Xcode to edit the Cartfile but be aware that other editing programs such as TextEdit might automatically include smart quotes instead of straight quotes. Carthage does not recognize content within smart quotes and not perform correctly.

1. Save the Cartfile. Run the following command to update dependencies:

      ```
      carthage update --use-xcframeworks
      ```

1. To use `AppNexusSDK` SDK, add the `AppNexusSDKDynamic.xcframework` and `OMSDK_AppNexus.xcframework` to the **Embedded Binaries** section:

    - Navigate to **Target** → **General** → **Embedded Binaries**.
    - Click the `+` icon and sadd the `AppNexusSDKDynamic.xcframework` and `OMSDK_AppNexus.xcframework`.
    
1. If you are using Carthage for an application, select **Embed & Sign**. Otherwise select **Do Not Embed**.
  
## XCFramework

Download the latest iOS SDK v9.x from [Azure CDN](https://adsdkprod.azureedge.net/mobile/ios/releases/9.1.1/static/sdks.zip). The downloaded zip file contains the following frameworks and resources bundle. Ensure that you are using the appropriate framework that best suits your needs. The **AppNexusSDK** is the recommendation for general use.

| Framework | Description |
|---|---|
| AppNexusSDK | Supports all ad types. |
| AppNexusNativeSDK | This framework only supports native ads on **iOS**.|
| AppNexusNativeMacOSSDK | This framework only supports native ads on **MacOS**. |
| ANSmartAdapter | A mediation adapter for Smart Ad Server.|
| ANGoogleAdapter | A mediation adapter for Google's AdMob.|
| ANFacebookCSRAdapter | A client side rendering adapter for Facebook Audience Network. |
| ANSDKResources.bundle | This contains necessary files which the SDK utilizes. |

1. Open the app’s Xcode project or workspace.
2. Go to the app target’s **General** configuration page.
3. To use the `AppNexusSDK`, you need to add the `AppNexusSDK.xcframework` and `ANSDKResources.bundle`.
4. To import the `AppNexusSDK.xcframework`,
    - Navigate to your project's Target settings.
    - Navigate to **Target** > **General**.
    - Click the `+` button under the **Frameworks, Libraries, and Embedded Content** section.
    - Click **Add Other** and then **Add Files**.
    - Choose the `AppNexusSDK.xcframework` file and click **Open**.

    :::image type="content" source="media/add-appnexus-xcf.png" alt-text="A screenshot that shows how to add AppNexus SDK in XCF.":::
5. To include the `ANSDKResources.bundle`,
    - Navigate to **Target** > **Build Phase**.
    - Expand the **Copy Bundle Resources** row and click the `+` icon.
    - Choose the `ANSDKResources.bundle` file and click **Open**.

    :::image type="content" source="media/add-andkresources.png" alt-text="A screenshot that shows how to add ANDK Resource bundle in XCF.":::

## Swift Package Manager

1. Go to **Package Dependencies** under your Xcode project and click on the `+` button.
   :::image type="content" source="media/swift-pkg-mgr-01.png" alt-text="Screenshot shows the steps to open a Swift Package project.":::
1. Copy and paste the URL https://github.com/appnexus/mobile-sdk-ios-spm in the search box and press `Enter/Return`.
   :::image type="content" source="media/swift-pkg-mgr-02.png" alt-text="Screenshot shows the steps to search a Swift Package package.":::
1. In **Choose Package Products for mobile-sdk-ios-spm** pop up window, different package products will be present. Select **AppNexusSDK** and click `Add Package`.
    :::image type="content" source="media/swift-pkg-mgr-03.png" alt-text="Screenshot shows the pop up for Swift Package package.":::
1. The selected package will be displayed and click on `Add Package` to save the configuration in **Package Dependencies**.
