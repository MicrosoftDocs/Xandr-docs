---
title: iOS SDK integration instructions
description: Learn how to integrate the current iOS SDK into your Xcode project using Swift Package Manager or alternative installation methods.
ms.custom: ios-sdk
ms.date: 09/03/2026
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---

# iOS SDK integration instructions

This article describes how to integrate iOS SDK v9.x into your Xcode project. For instructions on displaying different ad types, see [iOS SDK ad units](ios-sdk-ad-units.md).

## Requirements

- Your app must target iOS 15.0 or later.
- To request ads, use a valid placement ID. For supported ad units, you can instead use a valid member ID and inventory code.

## Installation

> [!IMPORTANT]
> Swift Package Manager (SPM) is the primary and recommended method for integrating the iOS SDK. CocoaPods support will be discontinued in the next SDK release.

Choose an installation method:

| Method | Status |
|:---|:---|
| [Swift Package Manager](#swift-package-manager) | Recommended |
| [XCFramework](#xcframework) | Manual integration |
| [Carthage](#carthage) | Alternative integration |
| [CocoaPods](#cocoapods) | Support ending |

### Swift Package Manager

1. Open your project in Xcode.
1. Select the project in the Project navigator, and then select **Package Dependencies**.
1. Select the **+** button to add a package dependency.

   :::image type="content" source="media/swift-pkg-mgr-01.png" alt-text="Screenshot of the Package Dependencies pane in Xcode.":::

1. Enter the following package URL in the search box, and then press **Return**:

   ```text
   https://github.com/appnexus/mobile-sdk-ios-spm
   ```

   :::image type="content" source="media/swift-pkg-mgr-02.png" alt-text="Screenshot of the iOS SDK package URL entered in Xcode.":::

1. Choose the version setting that fits your project. For new projects, select **Up to Next Major Version**. Then select **Add Package**.
1. In the **Choose Package Products for mobile-sdk-ios-spm** window, select **AppNexusSDK** and your app target. Then select **Add Package**.

   :::image type="content" source="media/swift-pkg-mgr-03.png" alt-text="Screenshot of the AppNexusSDK product selection in Xcode.":::

1. Verify that **AppNexusSDK** appears under **Package Dependencies**.

### Alternative installation methods

Use these methods only when Swift Package Manager doesn't meet your project's requirements.

#### XCFramework

Download [iOS SDK v9.14.0](https://adsdk.bing.net/mobile/ios/releases/9.14.0/static/sdks.zip). The ZIP file contains the following frameworks and resource bundle. Use **AppNexusSDK** for a general integration.

| Framework | Description |
|---|---|
| AppNexusSDK | Supports all ad types. |
| AppNexusNativeSDK | This framework only supports native ads on **iOS**. |
| AppNexusNativeMacOSSDK | This framework only supports native ads on **macOS**. |
| ANSmartAdapter | A mediation adapter for Smart Ad Server. |
| ANGoogleAdapter | A mediation adapter for Google's AdMob. |
| ANFacebookCSRAdapter | A client side rendering adapter for Facebook Audience Network. |
| ANVungleAdapter | A mediation adapter for Vungle. |
| ANSDKResources.bundle | This contains necessary files which the SDK utilizes. |

1. Open the app’s Xcode project or workspace.
1. Go to the app target’s **General** configuration page.
1. To use the `AppNexusSDK`, add the `AppNexusSDK.xcframework` and `ANSDKResources.bundle`.
1. To import the `AppNexusSDK.xcframework`:

    - Navigate to your project's Target settings.
    - Navigate to **Target** > **General**.
    - Click the `+` button under the **Frameworks, Libraries, and Embedded Content** section.
    - Click **Add Other** and then **Add Files**.
    - Choose the `AppNexusSDK.xcframework` file and click **Open**.

    :::image type="content" source="media/add-appnexus-xcf.png" alt-text="Screenshot of adding the AppNexusSDK XCFramework in Xcode.":::

1. To include the `ANSDKResources.bundle`:

    - Navigate to **Target** > **Build Phase**.
    - Expand the **Copy Bundle Resources** row and click the `+` icon.
    - Choose the `ANSDKResources.bundle` file and click **Open**.

    :::image type="content" source="media/add-andkresources.png" alt-text="Screenshot of adding the ANSDKResources bundle in Xcode.":::

#### Carthage

If you are unfamiliar with Carthage, review the [Carthage documentation](https://github.com/Carthage/Carthage/blob/master/README.md). After installing Carthage, follow these steps:

1. Open Terminal and navigate to the root directory of your project. Create a Cartfile:

    ```bash
    touch Cartfile
    ```

1. Open the Cartfile in Xcode:

    ```bash
    open -a Xcode Cartfile
    ```

1. Add the following lines to the Cartfile:

    ```text
    binary "https://adsdkprod.azureedge.net/mobile/ios/releases/carthage/AppNexusSDK.json"
    binary "https://adsdkprod.azureedge.net/mobile/ios/releases/carthage/OMSDK_Microsoft.json"
    ```

    > [!TIP]
    > Use straight quotation marks in the Cartfile. Carthage doesn't recognize smart quotation marks inserted by some text editors.

1. Save the Cartfile, and then update the dependencies:

    ```bash
    carthage update --use-xcframeworks
    ```

1. Add `AppNexusSDKDynamic.xcframework` and `OMSDK_AppNexus.xcframework` to **Target** > **General** > **Embedded Binaries**.
1. For an application target, select **Embed & Sign**. For other targets, select **Do Not Embed**.

#### CocoaPods

> [!WARNING]
> CocoaPods support will be discontinued in the next SDK release. Use Swift Package Manager for new integrations.

If you are unfamiliar with CocoaPods, review the [CocoaPods documentation](https://cocoapods.org/). After installing CocoaPods, follow these steps:

1. In Terminal, navigate to the root directory of your project and create a Podfile:

    ```bash
    pod init
    ```

1. Open the Podfile, set the platform version to 15.0, and add `AppNexusSDK` to the target:

    ```ruby
    platform :ios, '15.0'
    project 'FunBanner'

    target 'FunBanner' do
      pod 'AppNexusSDK'
    end
    ```

1. Save the Podfile, and then install the dependency:

    ```bash
    pod install
    ```

1. Close the open Xcode project, and then open the generated `.xcworkspace` file.
