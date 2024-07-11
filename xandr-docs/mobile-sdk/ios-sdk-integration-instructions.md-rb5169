---
title: iOS SDK Integration Instructions
description: In this article, explore the detailed step-by-step iOS SDK integration instructions and their requirements.
ms.custom: ios-sdk
ms.date: 10/28/2023
---

# iOS SDK integration instructions

This page describes how to integrate Mobile SDK with your project. Follow the instructions in this page to set up Mobile SDK to show ads in your app. For instructions on showing different ad types, see our various [ad unit](ios-sdk-ad-units.md) pages.

## Requirements

- This SDK requires **Xcode version 15.0 or higher** and your app should target **iOS 12.0 or higher**.
- In order to show ads, you must have a valid Xandr placement ID.
- Configure App Transport Security (ATS).

## Installation

There are four ways to get our SDK:

- [CocoaPods](#cocoapods)
- [Carthage](#carthage)
- [XCFramework](#xcframework)
- [Swift Package Manager](#swift-package-manager)
<!-- - [Download from source](#download-from-source) -->

### CocoaPods

If you are unfamiliar with CocoaPods review their [installation and user guides](https://cocoapods.org/). Once you have CocoaPods installed:

1. Use Terminal or your command line editor of choice, navigate to the root directory of your project and create a podfile.

   ```
   pod init
   ```

1. Using a text editor, open the newly created podfile. Set the platform version to 12.0 and add pod 'AppNexusSDX' to the target.

   ```
   # iOS: Podfile config to include our SDK
   platform :ios, '12.0'
   project 'FunBanner'
   target 'FunBanner' do
     pod 'AppNexusSDK'
   end
   ```

1. Save your changes and return to the Terminal and enter:

   ```
   pod install
   ```

1. CocoaPods downloads the Xandr SDK and creates a workspace in the project directory. If your project is currently open, close it and open the workspace.

### Carthage

If you are unfamiliar with Carthage review their [installation and user guides](https://github.com/Carthage/Carthage/blob/master/README.md). Once you've installed Carthage:

1. Open the Terminal app and navigate to the root directory of your project. Create a Cartfile.

   ```
   touch Cartfile
   ```

1. Open the file in Xcode to edit it.

   ```
   open -a Xcode Cartfile
   ```

1. Add the following line to the file.

   ```
    # iOS: Carthage config to include our SDK
   github "appnexus/mobile-sdk-ios" 
   ```

   > [!TIP]
   > You can use editor's other than Xcode to edit the Cartfile but be aware that other editing programs such as TextEdit might automatically include smart quotes instead of straight quotes. Carthage does not recognize content within smart quotes and not perform correctly.

1. Run below command.

   ```
   carthage update --use-xcframeworks
   ```

1. To use **AppNexusSDK** SDK, add the **AppNexusSDK.xcframework** and **OMSDK\_AppNexus.xcframework** to the **Embedded Binaries (Target → General → Embedded Binaries)** section by clicking the **+ icon**.
1. Drag the built `.xcframework` bundles from `Carthage/Build` into **Embedded Binaries (Target → General → Embedded Binaries)** section by clicking the **+ icon**.
1. If you are using Carthage for an application, select **Embed & Sign**, otherwise **Do Not Embed**.

<!-- ### Download from source

1. Download and unzip or clone the latest release of our SDK from our [Github Release](https://github.com/appnexus/mobile-sdk-ios/releases/latest) page.
1. Once the source from Github is downloaded, link the **AppNexusSDK.Xcodeproj** in your **Xcode project**.
1. Open the app’s Xcode project or workspace. Right click on Project and click on **Add Files to "Project Name**".
  :::image type="content" source="media/ios-sdk-integration-instructions-a.png" alt-text="Screenshot of Add files to Project screen.":::
1. Go to AppNexusSDK project folder and select the **AppNexusSDK.Xcodeproj**. Make sure to select **Copy items if needed** and select **Add**.
   :::image type="content" source="media/ios-sdk-integration-instructions-b.png" alt-text="Screenshot of the project folder.":::
1. Click **Link Binary With Libraries** (Target-&gt;General-&gt;Link Binary With Libraries) and select **AppNexusSDK.framework**.
   :::image type="content" source="media/ios-sdk-integration-instructions-c.png" alt-text="Screenshot of Link Binary with Libraries screen.":::

   :::image type="content" source="media/ios-sdk-integration-instructions-d.png" alt-text="Screenshot of the library selected from the drop-down menu."::: -->

### XCFramework

1. Download and unzip the latest version of **AppNexusSDK.xcframework.zip** of our SDK from [Github Releases page](https://github.com/appnexus/mobile-sdk-ios/releases). **AppNexusSDK.xcframework.zip** contains **AppNexusSDK.xcframework**, **AppNexusNativeSDK.xcframework**, and **OMSDK\_AppNexus.xcframework**.
1. Open the app’s Xcode project or workspace.
1. Go to the app target’s **General** configuration page.
1. To use **AppNexusSDK SDK**, add the **AppNexusSDK.xcframework** and **OMSDK\_AppNexus.xcframework** to the **Embedded Binaries (Target → General → Embedded Binaries)** section by clicking the **+ icon** or to use **AppNexusNativeSDK SDK**, add the **AppNexusNativeSDK.xcframework** and **OMSDK\_.xcframework** to the **Embedded Binaries (Target → General → Embedded Binaries)** section by clicking the **+ icon**.
   :::image type="content" source="media/ios-sdk-integration-instructions-e.png" alt-text="Screenshot of the General configuration screen.":::
1. Select **Add Files** from the drop-down and navigate to the location where you have the unzipped **AppNexusSDK.xcframework** and **OMSDK_AppNexus.xcframework** folders.
   :::image type="content" source="media/ios-sdk-integration-instructions-f.png" alt-text="Screenshot of the Add Files screen.":::
1. Select the unzipped folders and click **Open**.
   :::image type="content" source="media/ios-sdk-integration-instructions-g.png" alt-text="Screenshot shows that the unzipped folder has been selected and opened.":::
1. The added **AppNexusSDK.xcframework** and **OMSDK_AppNexus.xcframework** would be visible under the **Framework, Libraries, and Embedded Content** section.
   :::image type="content" source="media/ios-sdk-integration-instructions-h.png" alt-text="Screenshot shows that the added framework is visible in the Embedded content section.":::

### Swift Package Manager

1. Copy the URL [https://github.com/appnexus/mobile-sdk-ios.git](https://github.com/appnexus/mobile-sdk-ios.git) and check the latest
  version of SDK in [Release notes](ios-sdk-release-notes.md).
1. Open the app’s Xcode project or workspace. Select **Project → Swift Package** and click on **+ icon**.
   :::image type="content" source="media/ios-sdk-integration-instructions-i.png" alt-text="Screenshot shows the steps to open a Swift Package project.":::
1. Paste the Github URL [https://github.com/appnexus/mobile-sdk-ios.git](https://github.com/appnexus/mobile-sdk-ios.git) mentioned earlier in search bar of **Choose Package Repository** screen and click **Next**.
   :::image type="content" source="media/ios-sdk-integration-instructions-j.png" alt-text="Screenshot of the Choose Package Repository screen.":::
1. Select the appropriate version from the drop-down (checked in [Release notes](ios-sdk-release-notes.md) as mentioned earlier) and click **Next**.
   :::image type="content" source="media/ios-sdk-integration-instructions-k.png" alt-text="Screenshot of the Choose Package Options screen.":::
1. Select the applicable **Package Product** and click **Finish** to complete the setup.
   :::image type="content" source="media/ios-sdk-integration-instructions-l.png" alt-text="Screenshot of the Finish screen.":::
1. The added **AppNexusSDK** package would be visible under the **Framework, Libraries, and Embedded Content** section.
   :::image type="content" source="media/ios-sdk-integration-instructions-m.png" alt-text="Screenshot shows that the package is visible in the Embedded Content section.":::

## Set up for mediation (optional)

For instructions on getting set up for mediation, see [Mediate with iOS](mediate-with-ios.md).

## Related topics

- [Show Banners](show-banners-on-ios.md)
- [Show Interstitials](show-interstitials-ads-on-ios.md)
