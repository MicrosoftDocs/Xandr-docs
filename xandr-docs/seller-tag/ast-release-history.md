---
title: AST Release History
description: In this article, find the release history of AST and the updates made for each release.
ms.custom: seller-tag
ms.date: 10/28/2023
---

# AST Release History

> [!TIP]
> To utilize the most current version of AST, link to our CDN at [https://adsdk.microsoft.com/ast/ast.js](https://adsdk.microsoft.com/ast/ast.js).

| Release | Description | Date |
|---|---|---|
| [1.10.8](https://adsdk.microsoft.com/ast/ast.js) | -  Regular SDK updates to fix bugs, optimize performance, and improve user experience. | 22 April 2025 |
| [1.10.7](https://adsdk.microsoft.com/ast/ast.js) | -  Regular SDK updates to fix bugs, optimize performance, and improve user experience. | 15 April 2025 |
| [1.10.6](https://adsdk.microsoft.com/ast/ast.js) | -  Regular SDK updates to fix bugs, optimize performance, and improve user experience. | 10 April 2025 |
| [1.10.5](https://adsdk.microsoft.com/ast/ast.js) | -  Regular SDK updates to fix bugs, optimize performance, and improve user experience. | 9 April 2025 |
| [1.10.4](https://adsdk.microsoft.com/ast/ast.js) | -  Regular SDK updates to fix bugs, optimize performance, and improve user experience. | 3 April 2025 |
| [1.10.3](https://adsdk.microsoft.com/ast/ast.js) | -  Add the new `setPageOpts` parameter, `loadOutstreamUpgradeUrl`. | 1 April 2025 |
| [1.10.2](https://adsdk.microsoft.com/ast/ast.js) | - Regular SDK updates to fix bugs, optimize performance, and improve user experience. | 27 March 2025 |
| [1.10.1](https://adsdk.microsoft.com/ast/ast.js) | - Regular SDK updates to fix bugs, optimize performance, and improve user experience. | 25 March 2025 |
| [1.10.0](https://adsdk.microsoft.com/ast/ast.js) | - Added support for `pxratio`, `height`, `width`, and `ppi` to device fields in AST. | 18 March 2025 |
| [1.9.0](https://adsdk.microsoft.com/ast/ast.js) | - Regular SDK updates to fix bugs, optimize performance, and improve user experience. | 13 March 2025 |
| [1.8.0](https://adsdk.microsoft.com/ast/ast.js) | - Add additional consent checks to the Fledge auction workflow. <br> - Improve the release framework and smoke tests. | 10 March 2025 |
| [1.7.0](https://adsdk.microsoft.com/ast/ast.js) | - Regular SDK updates to fix bugs, optimize performance, and improve user experience. | 6 March 2025 |
| 1.6.0 | - Regular SDK updates to fix bugs, optimize performance, and improve user experience. | 27 February 2025 |
| [1.5.0](https://adsdk.microsoft.com/ast/ast.js) | - - Regular SDK updates to fix bugs, optimize performance, and improve user experience. | 25 February 2025 |
| [1.4.0](https://adsdk.microsoft.com/ast/ast.js) | - Add support for OpenRTB Native requests and responses. | 21 February 2025 |
| [1.3.0](https://adsdk.microsoft.com/ast/ast.js) | - add `batchId` and `adTrackingId` to AST telemetry events.<br> - refactor code around user agents. | 13 February 2025 |
| [1.2.0](https://adsdk.microsoft.com/ast/ast.js) | - add `feedbackUrl` and `native.custom` fields to `adObject`. <br> - fix sizes passed into AST IG <br> - correct `topic` field name in AST. <br> - remove extra fields in `auctionConfig` for AST. <br> - Private Auction runs for treatment labels <br> - add `removeTag` API function <br> - new AST event `mrcView` | 12 February 2025 |
|[1.0.0](https://adsdk.microsoft.com/ast/ast.js) | - Transition to Microsoft domain and CDN. <br> - Update the event name `adCodeRenderStart` to `adSlotRenderStart`.|28 January 2025|
| [0.66.0](https://acdn.adnxs.com/ast/static/0.66.0/ast.js) | - Update owner and reference URLs used for Fledge. | 18 November 2024 |
| [0.65.0](https://acdn.adnxs.com/ast/static/0.65.0/ast.js) | - Update fledge logic to use `deprecateURN` function instead of `auctionConfig` approach. <br> - Include `geooverride` information for AST context Interest Groups.| 4 November 2024 |
| [0.64.7](https://acdn.adnxs.com/ast/static/0.64.7/ast.js) | - Various updates to include additional data in AST telemetry. <br> - Update the version of telemetry package used by AST. <br> - Additional updates to (FLEDGE) private auction workflows for Chrome (in beta status). <br> - Support custom native assets for MSN. <br> - Add new AST event `adCodeRenderStart`. | 13 September 2024 |
| [0.63.3](https://acdn.adnxs.com/ast/static/0.63.3/ast.js) | - Various updates to (FLEDGE) private auction workflows in Chrome (in beta status). <br> - Added additional data for core AST telemetry events. <br> - Fixed issues with Native Assembly ads in AST SafeFrame. | 12 August 2024 |
| [0.62.4](https://acdn.adnxs.com/ast/static/0.62.4/ast.js) | - Add support to run (FLEDGE) private auctions in Chrome (in beta status) <br> - Add `msft_tag` field to `defineTag` <br> - Add `rewardedAds` field to `defineTag` <br> - Fix `adRequestFailure` error logic to trigger only on active tags <br> - Update SafeFrame HTML title attribute for accessibility readers | 10 June 2024 |
| [0.61.2](https://acdn.adnxs.com/ast/static/0.61.2/ast.js) | - Add support for DSA Transparency <br> - Remove tracking iframe and pixels when refresh is called <br> - Improve error handling when encountering a HTTP error | 14 February 2024 |
| [0.60.1](https://acdn.adnxs.com/ast/static/0.60.1/ast.js) | - Integrate telemetry logging in AST <br> - Add content language field in `setPageOpts` <br> - Improve logic on specific null checks | 15 December 2023 |
| [0.59.0](https://acdn.adnxs.com/ast/static/0.59.0/ast.js) | - Add MSFT `setPageOpts` field <br>- Add `isExclusive` and `isRoadblock` fields to AST event object | 08 November 2023 |
| [0.58.0](https://acdn.adnxs.com/ast/static/0.58.0/ast.js) | - Include `invCode` with `apntag.getTag` function <br> - Update `clearRequest` to choose certain tags <br> - Add support for GPP 1.1 <br> - Add MSFT bid fields to AST event object | Sep 20 2023 |
| [0.57.0](https://acdn.adnxs.com/ast/static/0.57.0/ast.js) | - Add native renderer information for AST events <br> - Check value of `gdprApplies` before checking `tcString` <br> - Catch exception when calling `getTag()` in certain cases <br> - Update `attachClickTrackers()` to be compatible inside web component environment <br> - Update AST `usersync` domain and logic | Jul 14 2023 |
| [0.56.0](https://acdn.adnxs.com/ast/static/0.56.0/ast.js) | - Add support for coppa <br> - Add support to specify sandbox attributes for AST iframe <br> - Add support to include extra div container around AST iframe <br> - Update the this context in `xhr` call <br> - Fix function call in `adManager` | May 31 2023 |
| [0.55.0](https://acdn.adnxs.com/ast/static/0.55.0/ast.js) | - Add `userSync` feature <br> - Add setting to control when viewability script loads for native ads | Mar 28 2023 |
| [0.54.1](https://acdn.adnxs.com/ast/static/0.54.1/ast.js) | - Add param for `setEndpoint` function to optionally lock impbus URL <br> - Update `postMessage` logic for Global Privacy Platform consent feature | Jan 18 2023 |
| [0.53.0](https://acdn.adnxs.com/ast/static/0.53.0/ast.js) | Add support for Global Privacy Platform (US) | Dec 19 2022 |
| [0.52.0](https://acdn.adnxs.com/ast/static/0.52.0/ast.js) | Update notify function to support a targetId | Nov 30 2022 |
| [0.51.0](https://acdn.adnxs.com/ast/static/0.51.0/ast.js) | Update logic around simple domain usage | Oct 18 2022 |
| [0.50.0](https://acdn.adnxs.com/ast/static/0.50.0/ast.js) | Fix window reference for AST div when using safeframe | Aug 03 2022 |
| [0.49.0](https://acdn.adnxs.com/ast/static/0.49.0/ast.js) | - Add a `globalPlacementId` field to `defineTag` <br> - Add a `pageUrl` override field for certain mobile environments | Jun 21 2022  |
| [0.48.1](https://acdn.adnxs.com/ast/static/0.48.1/ast.js) | - Replace unload event with pagehide <br> - Update dependency packages to support Node 14 <br> - Add an optional parameter for `resizeAd` | Jun 01 2022  |
| [0.47.0](https://acdn.adnxs.com/ast/static/0.47.0/ast.js) | Update type for publisher first party IDs feature | May 04 2022  |
| [0.46.2](https://acdn.adnxs.com/ast/static/0.46.2/ast.js) | Add support for publisher first party IDs | Mar 21 2022  |
| [0.45.0](https://acdn.adnxs.com/ast/static/0.45.0/ast.js) | - Resolve issue when SafeFrame is loaded in a scrollable event <br> - Resolve issue with Safari Outstream and SafeFrame where ad was not expanding | Feb 08 2022  |
| [0.44.0](https://acdn.adnxs.com/ast/static/0.44.0/ast.js) | Remove usage of localStorage within debugger feature | Dec 21 2021 |
| [0.43.0](https://acdn.adnxs.com/ast/static/0.43.0/ast.js) | Add conditional check for some `postMessage` requests | Nov 11 2021  |
| [0.42.1](https://acdn.adnxs.com/ast/static/0.42.1/ast.js) | - Add support for new cpm fields available in bid response <br> - Add schain support | Nov 03 2021  |
| [0.41.0](https://acdn.adnxs.com/ast/static/0.41.0/ast.js) | - Update `adRequested` event trigger conditions <br> - Additional updates to WebComponent and SafeFrame support <br> - Update logic on when to set the displayed flag | Sep 29 2021  |
| [0.40.0](https://acdn.adnxs.com/ast/static/0.40.0/ast.js) | - Add support for UID2 userId <br> - Add support for Google Additional Consent field | Jun 24 2021  |
| [0.39.0](https://acdn.adnxs.com/ast/static/0.39.0/ast.js) | Add support for web components to banner ads | Jun 10 2021  |
| [0.38.0](https://acdn.adnxs.com/ast/static/0.38.0/ast.js) | - Ignore case on userId field <br> - Address issue in refresh behavior fro video ads | May 17 2021  |
| [0.37.1](https://acdn.adnxs.com/ast/static/0.37.1/ast.js) | Fixed issue around `withCredentials` field | May 03 2021  |
| [0.37.0](https://acdn.adnxs.com/ast/static/0.37.0/ast.js) | Add support for simple domain/cookieless requests | Apr 28 2021  |
| [0.36.0](https://acdn.adnxs.com/ast/static/0.36.0/ast.js) | Add support for LiveRamp userId in AST |  |
| [0.35.0](https://acdn.adnxs.com/ast/static/0.35.0/ast.js) | - Add support for userId netID in AST <br> - Correct the format used to pass segment data in UT request <br> - Resend Criteo data over EIDS for AST <br> - Ensure mediation.js is loaded with correct protocol in iframes |  |
| [0.34.0](https://acdn.adnxs.com/ast/static/0.34.0/ast.js) | Send native custom fields to universal tag request |  |
| [0.33.0](https://acdn.adnxs.com/ast/static/0.33.0/ast.js) | Send Criteo userId data via `tpuids` property in universal tag request. |  |
| [0.32.0](https://acdn.adnxs.com/ast/static/0.32.0/ast.js) | - Improve AMP domain detection <br> - Add test headers when debug is enabled <br> - Update TCF2 Purpose 1 check to treat undefined as false <br> - Safeframe security updates |  |
| [0.31.0](https://acdn.adnxs.com/ast/static/0.31.0/ast.js) | - Add support for Criteo and TTD IDs through `setPageOpts` API  <br> - Add deal Id to `adObj` API  <br> - Support video fallback from mediation in safeframe |  |
| [0.30.1](https://acdn.adnxs.com/ast/static/0.30.1/ast.js) | Add support for expandBy creative flag in mediation. |  |
| [0.30.0](https://acdn.adnxs.com/ast/static/0.30.0/ast.js) | Add display none property to AST div when resizeAd uses 0x0 |  |
| [0.29.0](https://acdn.adnxs.com/ast/static/0.29.0/ast.js) | - Add support for consent strings in AMP <br> - Enforce Purpose one consent in TCF v2 |  |
| [0.28.1](https://acdn.adnxs.com/ast/static/0.28.1/ast.js) | Codebase improvements |  |
| [0.28.0](https://acdn.adnxs.com/ast/static/0.28.0/ast.js) | - Add “USP API” support for CCPA <br> - Make all Impbus requests secure(https) by default |  |
| [0.27.1](https://acdn.adnxs.com/ast/static/0.27.1/ast.js) | Add CCPA support through `setPageOpts` API. |  |
| [0.27.0](https://acdn.adnxs.com/ast/static/0.27.0/ast.js) | - Add TCF v2.0 support <br> - Add support for multi-size prebid creatives in mediation fallback <br> - Add support for native custom types in AST |  |
| [0.26.1](https://acdn.adnxs.com/ast/static/0.26.1/ast.js) | Codebase improvements |  |
| [0.26.0](https://acdn.adnxs.com/ast/static/0.26.0/ast.js) | - Codebase improvements  <br> - Create versioned safe frame and mediation |  |
| [0.25.0](https://acdn.adnxs.com/ast/static/0.25.0/ast.js) | Add support for fallback video ads |  |
| [0.24.0](https://acdn.adnxs.com/ast/static/0.24.0/ast.js) | - Add blanks to reporting for mediation <br> - Enhance `adObj` for mediation events <br> - Add support for video outstream fallback from mediation |  |
| [0.24.0 alpha](https://acdn.adnxs.com/ast/alpha/0.24.0/ast.js) | **Warning:** This is an alpha release and functionality could change without notice. <br><br> - Add blanks to reporting for mediation <br> - Enhance adObj for mediation events <br> - Add support for video outstream fallback from mediation |  |
| [0.23.2](https://acdn.adnxs.com/ast/static/0.23.2/ast.js) | - Add support for native assembly on mediation fallback <br> - Add  support for mediation events (see [Ad Object API](ad-object-api.md)) |  |
| [0.23.1](https://acdn.adnxs.com/ast/static/0.23.1/ast.js) | Added AMP environment detection flag |  |
| [0.23.0 alpha](https://acdn.adnxs.com/ast/alpha/0.23.0/ast.js) | **Warning:** This is an alpha release and functionality could change without notice. <br><br> - Add support for native assembly on mediation fallback (see [Ad Object API](ad-object-api.md)) <br> - Add  support for mediation events (see [Ad Object API](ad-object-api.md)) |  |
| [0.22.0](https://acdn.adnxs.com/ast/static/0.22.0/ast.js) | - Added support for mediation iframe size change dynamically <br> - Added support for getting consent management (GDPR string) through SafeFrame API <br> - Add brand category to `adObj` <br> - Bug Fixes |  |
| [0.21.1](https://acdn.adnxs.com/ast/static/0.21.1/ast.js) | Bug Fixes |  |
| [0.21.0](https://acdn.adnxs.com/ast/static/0.21.0/ast.js) | - Added geo override functionality to `setPageOpts` <br> - Enabled toolkit from apntag <br> - Bug Fixes |  |
| [0.20.0](https://acdn.adnxs.com/ast/static/0.20.0/ast.js) | - Feature Added override option to `apntag.setKeywords` <br> - Added media type and media sub-type to `adObj` <br> - Bug Fixes |  |
| [0.19.0](https://acdn.adnxs.com/ast/static/0.19.0/ast.js) | - Feature Support desc2 and other assets on native bid request (see [defineTag](define-tag.md)) <br> - Bug Fixes |  |
| [0.18.1](https://acdn.adnxs.com/ast/static/0.18.1/ast.js) | - Feature Invoke server-supplied renderers on native mediation bids <br> - Feature Added `apntag.getTag(<targetId>)` for returning tag data <br> - Convert member strings to numbers automatically |  |
| [0.18.0](https://acdn.adnxs.com/ast/static/0.18.0/ast.js) | - Feature Support Secure Frame with Outstream <br> - Feature Added `usePmtRule` field to defineTag function <br> - Added referrer data to request |  |
| [0.17.1](https://acdn.adnxs.com/ast/static/0.17.1/ast.js) | - Feature Added `auctionTimeout` to `setPageOpts` <br> - Bug Fix |  |
| [0.17.0](http://acdn.adnxs.com/ast/static/0.17.0/ast.js) | - Feature Support native rtb creatives from mediation <br> - Bug Fix |  |
| [0.16.2](https://acdn.adnxs.com/ast/static/0.16.2/ast.js) | Bug Fixes |  |
| [0.16.1](http://acdn.adnxs.com/ast/static/0.16.1/ast.js) | Bug Fix |  |
| [0.16.0](http://acdn.adnxs.com/ast/static/0.16.0/ast.js) | - Feature GDPR support <br> - Feature Added `apntag.attachClickTrackers` for firing native click trackers <br> - Feature Added `skipOffset` as a definable video parameter |  |
| [0.15.1](http://acdn.adnxs.com/ast/static/0.15.1/ast.js) | - Feature Added `desc2` to native response object <br> - Bug Fix |  |
| [0.15.0](http://acdn.adnxs.com/ast/static/0.15.0/ast.js) | - Feature Support protocol-less urls <br> - Safeframe rewrites and updates <br> - Bug Fixes |  |
| [0.14.0](http://acdn.adnxs.com/ast/static/0.14.0/ast.js) | - Feature Render AMP Ads above the fold (availability pending AMP Project support) <br> - Feature Support for Safeframe "meta" information |  |
| [0.13.0](http://acdn.adnxs.com/ast/static/0.13.0/ast.js) | - Feature Support Privacy Field and Flag in AST <br> - Feature Support for Scroll offset in the SafeFrame API |  |
| [0.12.2](http://acdn.adnxs.com/ast/static/0.12.2/ast.js) | - Feature Safeframe Sandbox Mode to disallow window.top navigation <br> - Bug Fixes |  |
| [0.12.0](http://acdn.adnxs.com/ast/static/0.12.0/ast.js) | - Feature  Initialize ad iframe in collapsed state <br> - Test Native video support <br> - Bug fixes |  |
| [0.11.0](http://acdn.adnxs.com/ast/static/0.11.0/ast.js) | - Feature Click to open iTunes in iPhone <br> - Activation Viewability measurement of native creatives available (requires server-side activation) <br> - Bug fixes |  |
| [0.10.2](http://acdn.adnxs.com/ast/static/0.10.2/ast.js) | Bug fixes for mediation impressions |  |
| [0.10.0](http://acdn.adnxs.com/ast/static/0.10.0/ast.js) | - New method `apntag.getAstVersion` <br> - Option to remove debug information from querystring <br> - Bug fixes <br> - Removed deprecated code |  |
| [0.9.0](http://acdn.adnxs.com/ast/static/0.9.0/ast.js) | - Add support for Publisher ID <br> - Fix internal error causing "ad_type undefined" <br> - Fix bug with Target ID not set for Native ads <br> - Other minor bug fixes and improvements |  |
| [0.8.2](http://acdn.adnxs.com/ast/static/0.8.2/ast.js) | Fix bug for ads not rendered in IE8 |  |
| [0.8.1](http://acdn.adnxs.com/ast/static/0.8.1/ast.js) | - Fix bug for `Object.defineProperty` not supported in IE8 <br> - Add "targetid" to `adObj` in AST events <br> - `minWidth`  setting is for ad, container must be greater   <br> - CookieSet feature released. See the API page for details. |  |
| [0.8.0](http://acdn.adnxs.com/ast/static/0.8.0/ast.js) | **Warning:** Breaking Change <br> This version of AST contains breaking changes. It will not be promoted to [the production version of AST](https://acdn.adnxs.com/ast/ast.js) until on or after July 10, 2017. For more details about out breaking change policy, please refer to [Breaking Changes - AST API](breaking-changes-ast-api.md). <br><br> - Support v3native assets. Changes consist of: <br> &nbsp;&nbsp;- The `adType` object returned for native demand will be changing to support our new native asset model, and to be more aligned with the OpenRTB native standard. <br> &nbsp;&nbsp;- The following fields have been renamed: <br> &nbsp;&nbsp;&nbsp;&nbsp; - `description` renamed to `body` <br> &nbsp;&nbsp;&nbsp;&nbsp; - `mainMedia` renamed to `image` <br> &nbsp;&nbsp;- The following fields have been removed: <br> &nbsp;&nbsp;&nbsp;&nbsp; - `custom` <br> &nbsp;&nbsp;&nbsp;&nbsp; - `rating` <br> &nbsp;&nbsp;- The following field has been moved: <br> &nbsp;&nbsp;&nbsp;&nbsp; - `iconImgUrl` has been moved under the `icon` object to `icon.url` <br> - Improvement in page performance by reducing the number of times our Viewability javascript can be inserted to once per page (instead of once per ad slot) <br> - Minor bug fixes |  |
| [0.7.4](http://acdn.adnxs.com/ast/static/0.7.4/ast.js) | Fix bug for Cannot read property 'ad_type' of null with video mediation on AST |  |
| [0.7.3](http://acdn.adnxs.com/ast/static/0.7.3/ast.js) | - Fix bug for mediated ads not rendering in IE browsers <br> - Fix bug for bad request event callback when adcall request fails |  |
| [0.7.2](http://acdn.adnxs.com/ast/static/0.7.2/ast.js) | - Fix bug for IE11 issue with base target <br> - Fix bug for banner ads coming from `AstMediationManager` not getting displayed |  |
| [0.7.1](http://acdn.adnxs.com/ast/static/0.7.1/ast.js) | Minor bug fixes |  |
| [0.7.0](http://acdn.adnxs.com/ast/static/0.7.0/ast.js) | - Implement Viewability functions in AST through Safeframe <br> - Support size mapping in AST <br> - Fix bug for updating Safeframe expand params, as per IAB spec <br> - Fix bug for AST Toolkit not displaying when there is a no-bid <br> - Fix bug for AST Toolkit creative size is displayed backwards |  |
| [0.6.0](http://acdn.adnxs.com/ast/static/0.6.0/ast.js) | - SafeFrame expand/collapse support options on individual tags <br> - Support banner mediation in SafeFrame <br> - Support for `$sf.ext.winHasFocus` API in SafeFrame <br> - AST Toolkit v0 <br> - Fix issue with Native fullText attribute <br> - Remove extraneous logging with SafeFrame enabled |  |
| [0.5.1](http://acdn.adnxs.com/ast/static/0.5.1/ast.js) | Minor bug fixes |  |
| [0.5.0](http://acdn.adnxs.com/ast/static/0.5.0/ast.js) | - Implement SafeFrame in AST (phase 1) <br> - Support for global event handling with the `onEvent` function <br> - Fix bug for not setting iframe size as inline style <br> - Add `setKeywords` method <br> - Fix bug to ensure that the `showTag` function clears the targetdiv content before rendering new content if not using refresh API <br> - Fix bug for duplicate resource requests being made for CDN in some instances <br> - Copy sizes in `adObj` to root level instead of just within banner object |  |
| [0.4.2](http://acdn.adnxs.com/ast/static/0.4.2/ast.js) | Resolve issue with ads not displaying in Chrome 54 after using the browser back button. |  |
| [0.4.1](http://acdn.adnxs.com/ast/static/0.4.1/ast.js) | Fix bug with stray character appearing on page |  |
| [0.4.0](http://acdn.adnxs.com/ast/static/0.4.0/ast.js) | - Added `alwaysUseXDomainIframe` parameter to `defineTag` function to prevent creatives from accessing the parent page directly. <br> - Fix bug for unrelated logging when calling `apntag.refresh` on specific ad slots. <br> - Fix bug for AST with prebid not resizing placements dynamically. |  |
| [0.3.9](http://acdn.adnxs.com/ast/static/0.3.9/ast.js) | - Added `notify` function to allow AST to send a messagetoarenderer on a page. <br> - Added optional `externalImpId`  parameter to support the unique identifier of an externally generated auction. <br> - Fix bug when keyword segment sends integers. <br> - Fix bug where Outstream video in third party iframes was not loading in Safari <br> - Fix bug for `user.age` and `user.gender` not being sent <br> - Fix bug for `event.collapseAd` |  |
| [0.3.8](http://acdn.adnxs.com/ast/static/0.3.8/ast.js) | Added optional `trafficSourceCode` parameter to `defineTag` function. The value of this field will be logged to Standard Feed in the `traffic_source_code` column. |  |
| [0.3.7](http://acdn.adnxs.com/ast/static/0.3.7/ast.js) | - Add support for `mediation.js` <br> - Add `resizeAd` function <br> - New required query string parameter for running a debug auction: `debug_member` |  |
| [0.3.6](http://acdn.adnxs.com/ast/static/0.3.6/ast.js) | Fix bug where `apntag.refresh()` function throws exception with missing `div` element |  |
| [0.3.5](http://acdn.adnxs.com/ast/static/0.3.5/ast.js) | - Add `offEvent` for turning off multiple event handlers at one time  <br> - Add optional `noBidIfUnsold` parameter to `defineTag` function <br> - Add `forceCreativeId` parameter to `defineTag` function <br> - Log additional information in debug mode <br> - Bug fixes for Internet Explorer |  |
| [0.3.4](http://acdn.adnxs.com/ast/static/0.3.4/ast.js) | - Add `adBadRequest` event <br> - Make member optional field <br> - Bug `fixforadCollapse` event <br> - Remove CORS preflight requirement to improve performance <br> - Add `TEST` flag for test auction <br> - Add `promoAlignment` support |  |
| [0.3.3](http://acdn.adnxs.com/ast/static/0.3.3/ast.js) | - Bug fixes for IE browser support <br> - Support additional reserved keywords |  |
