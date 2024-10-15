---
title: Microsoft Curate - Ad Viewability Methodology (DOM)
description: In this module, understand the Microsoft Advertising viewability measurement process and methodology. It is designed for Microsoft Advertising clients, prospects, and partners only.
ms.date: 10/28/2023
---


# Microsoft Curate - Ad viewability methodology (DOM)

This document is meant to describe the Microsoft Advertising viewability measurement process and methodology. It is designed for Microsoft Advertising clients, prospects, and partners only.

## Introduction

### Scope and purpose

Ad viewability measurement is a complex issue. It must take into account various and changing specificities, such as:

- Publisher and agency ad servers, and their various versions
- Operating systems (desktops and mobiles), and their various versions
- Browsers (and their specific operating systems versions)
- Website page layouts (including first and third party's scripts on the pages)
- Ad formats (including country-specific ones)
- Local viewability standards (US IAB, first pixel viewability, etc.)
- Client-specific requirements (definitions, reporting, etc.)
- Ad-exchanges real-time constraints, optimization processes, etc.
- A fast-changing environment, constantly innovating

### Confidentiality

This document is confidential and not public.

It is available to Microsoft Advertising clients, prospects, and partners.

It must not be transferred to any other recipient without explicit agreement from Microsoft Advertising.

### Document updates

Microsoft Advertising measurement technology must constantly be updated to provide a consistent and stable methodology in a changing environment.

This document reflects Microsoft Advertising methodology at the date it was written. We advise you not to use a PDF export of this document, as it may become obsolete.

Microsoft Advertising shall not be held responsible for any conclusion drawn from an obsolete version of this document.

### Description of this document

This document follows the main steps of the Microsoft Advertising viewability measurement process:

- In-page measurement
- Data collection, filtering, and processing
- Client-facing reporting

## Client-side measurement

### Overview

Microsoft Advertising technology relies on a JavaScript that is served with the advertising creative. This script runs in the browser of the internet user.

Several functions are performed by the script:

- Impression counting
- Detection of the impressions that must be measured
- Measurement of the viewability of these objects
- Transfer of the viewability data to a collection platform

### Compatibility

#### Compatible formats

Microsoft Advertising technology is compatible with the following types of formats:

- Display creatives
- Rich media creatives (javascript + images)
- Desktop browsers
- Mobile browsers
- Ads in mobile apps (using our Mobile SDK, the Microsoft SDK, or OMSDK)
- Native ads (display ads only)
- VAST Video when VPAID is available ([Measurement of Video Viewability using VPAID Wrapper](video-viewability.md))

#### Incompatible formats

Microsoft Advertising technology is currently not compatible with the following formats:

- Ads in sites that refuse third party scripts
- Custom banner ad formats

### Script implementation

The Microsoft Advertising script is implemented as a native call from the creative's script. The script is served to all impressions traded on the Microsoft Advertising platform.

#### Compatible Ad Servers

Microsoft Advertising ad viewability is independent from publisher or agency ad servers. Nevertheless, its measurement has been tested on the following non-exhaustive list:

- Google DoubleClick: Doubleclick For Agencies (DFA), Doubleclick For Publishers (DFP)
- Sizmek
- AOL Adtech
- SmartAdserver
- Open Ad Stream
- Atlas
- Weborama
- Any other ad servers which accept third part script

#### Known limitations: Third-party script support

All desktop ad servers allow third party scripts, except some browser toolbars also reject JavaScript.

### Script call

#### Methods

The Microsoft Advertising script is called as a script tag (`<SCRIPT>`) included into the creative's JavaScript.

Since Microsoft Advertising serves the creative, the script call is generated natively by the platform. No manual copy and paste, or option checkbox is required.

#### Compatible platforms

- Windows
  - Internet Explorer
  - Firefox
  - Chrome
  - Safari
  - Edge
- Mac OS
  - Safari
  - Firefox
  - Chrome
- iOS
  - Safari
- Android
  - Chrome
  - Android browser
- Windows mobile

#### Known limitations: JavaScript requirement

**JavaScript** must be enabled in the browser of the internet user. If JavaScript is not enabled, the impression cannot be measured.

### Sampling

Microsoft Advertising does not conduct any form of sampling.

### Impression counting

#### Script delivery

The Microsoft Advertising script is delivered by a CDN that automatically chooses the closest server to ensure quick delivery of the script. Script delivery, however, is not used to count the number of impressions served.

#### Impressions

Impressions are counted by the Microsoft Advertising ad-trading platform, not by the measurement script. Our count of impressions (imps) is the one used for billing. It corresponds to the real total number of traded impressions.

This metric differs from third party ad viewability providers. Vendors rely on their script to count impressions. If the script is not loaded, or cannot fire a pixel, no impression is counted by third party vendors, whereas the impression is inherently counted by Microsoft Advertising.

> [!NOTE]
> The Microsoft Advertising impression count is higher than third-party impression numbers.

#### Measured impressions

Measured impressions are counted when the measurement script fires a pixel to the Microsoft Advertising platform.

In cases where the user quits the page before the Microsoft Advertising script has actually launched, the impression is counted as served, and not measured.

> [!NOTE]
> Microsoft Advertising measured impressions are comparable with third party's measured impressions.

#### No impact on ad viewability

Ad viewability is not impacted by the impression counting methodology. By default, impressions are tagged as "not measured". Following the IAB requirements, viewability indicators are computed only on measured impressions.

The consequence of a higher (and real) number of impressions is a lower measurement rate (measured impressions / impressions).

> [!NOTE]
> The Microsoft Advertising measurement rate should not be compared with a third party vendor's measurement rate.

### Compound tracking

Microsoft Advertising does not allow compound tracking. If several ads must be measured, they must be configured individually.

Microsoft Advertising can however, measure banners made of several objects, as a single impression.

### Cache-busting techniques

Microsoft Advertising uses specific http headers, such as "Cache-Control:no-store, no-cache, private" or "Pragma no-cache," to force browsers not to cache tracking requests.

Microsoft Advertising tracking requests (impression count and viewability measurement) also use a double system to ensure that http requests are not cached by browsers.

Each script loading is associated with a unique ID. The script fires several pixels during the lifetime of the impression. Each pixel is unique, as it contains all the measured information and a unique timestamp (milliseconds).

Those unique IDs are used in the file path and as parameters when building the URL. The following sample shows the beginning of an URL:

```
http:// fra1.ib.adnxs.com/vevent?e=wqT_.... 
&dlo=1&referrer=http%3A%2F%2Fib.adnxs.com%2Ftt%3Fid%3D3747591&type=pv&px=0&py=0&bw=300&bh=250 
&sw=2560&sh=1440&pw=1440&ph=351&ww=1440&wh=351 
&x=1427978373745428462,149999,v,mac,webkit_chrome,view5-1,90,,0 
```

Despite all these precautions, in a negligible number of cases, impressions may be under-counted.

### Object detection

Microsoft Advertising detects the banner object that must be measured. The object can be an image or an iframe. It must be fully loaded on the page to be considered as viewable.

Non-loaded banner objects are not viewable.

### Viewability conditions

#### Required information

The Microsoft Advertising script monitors the following events and browser statuses to assess whether an ad is viewable or not:

- Window focus / non-focus
- Tab switches
- Page scroll
- Page resize
- Browser zoom
- Screen saver start
- Banner object load / non-load
- Mouse / keyboard activity / inactivity

#### Known limitations: Viewability and measurement constraints

- Microsoft Advertising considers only the window that is in focus as visible. This methodological choice matches the norms of internet audience measurement.
- When two monitors are used, if an out-of-focus browser window is visible on one monitor, the impression may be considered non-viewable even if the user may see it.
- When measured from a cross-domain iframe, an impression that is loaded in a window that is not in focus, may be counted as viewable. This may lead to an overestimation of viewable impressions.
- Microsoft Advertising does not monitor if the whole browser window is moved out of the screen while still in focus. In this case, the impression may be considered viewable even if it is out of the screen.
- Auto-refresh pages may generate additional ad impressions. The refreshed page can either be viewable or not. If the page is not viewable (hidden tab or window), the impression is not viewable.
- If the refreshed page is viewable, the impressions on the page may be viewable if they are in the visible part of the page. In this case, the number of viewable impressions may be overestimated. Although Microsoft Advertising cannot quantify this overestimation, it should remain limited, as highly refreshed pages can be detected by fraud detection procedures.
- If a Firefox browser window is resized, the impression may be out of view. When the impression is loaded within a cross-domain iframe, it may result in an overestimation of its viewability status.

#### Iframes

Microsoft Advertising measures ad viewability in iframes (HTML pages within the HTML page), even when served in a cross-domain configuration (the domain of the iframe is different from the domain of the page).

In order to achieve this, several techniques are used:

- geometric approach and browser API for Internet Explorer (versions 7 to 10) and Firefox (all versions)
- browser optimization for all Webkit browsers (Safari, Chrome and Internet Explorer 11+)

#### Abandonment

Microsoft Advertising records impressions when the impression is transacted on the platform, prior to delivery of the selected ad content.

In certain situations, the user may abandon the web page after the impression was counted, but prior to delivery of the ad content. In this case, the impression is counted in the "imps" metrics, but the impression is not counted as "viewable impression".

### Techniques for log management

The Microsoft Advertising script periodically transfers data to a collection platform. Data transfers contain partial information about ad viewability that is then aggregated on the platform.

It is not prudent to send viewability data only when the user navigates away from the page because pages can remain open in hidden tabs, sometimes for days or weeks and the information may be lost if the page is closed when the user is offline.

For this reason, data transfers are made periodically so that the risk of losing data is minimized. When the impression reaches the viewability threshold, a pixel is fired to the Microsoft Advertising platform.

### Miscellaneous

#### Domain-based ad blockers

Ad blockers are browser extensions that prevent ads from showing on pages. They rely on lists of ad servers, and block http calls to these ad servers.

Because Microsoft Advertising is an ad server, no call to Microsoft Advertising is made by browsers that use ad blockers.

#### Image size-based ad blockers

In cases where an ad server is called but images are blocked, the Microsoft Advertising script detects no creative object. The ad impression is counted (the ad server counts it too, so numbers remain consistent), but the ad is not viewable. See [Object Detection](#object-detection) for more information.

#### User's disability image rendering

Microsoft Advertising measures the actual impression size, zoom, etc. on the screen of the user. If the images are zoomed, the real size is taken into account.

### Rich media banners

Rich media banners are most often made of two distinct objects. The main object is a regular ad impression. The second object is often called expand.

Microsoft Advertising can measure both objects for rich media banners. But viewability reporting is on the main object only.

## Data collection, filtering, and processing

### Robots.txt

The Microsoft Advertising collection servers host the `robots.txt` file. This file excludes all official robot traffic to collection pages. This way, official robots cannot generate fake impression records on the Microsoft Advertising platform.

### Server crawlers

If non-official robots access a collection page, they can either:

- replay existing requests
- randomly generate new requests

If a request is replayed, Microsoft Advertising detects duplicated requests (same full URL) thanks to the unique ID used to generate unique URLs. Duplicated lines are filtered out.

If a random request is generated, Microsoft Advertising checks for consistency of the different parameters of the request. The probability of randomly generated valid requests with the existing IDs (customers, campaigns, etc.) is negligible.

Microsoft Advertising uses a list of robot names that is checked against the user agent of the request. User agents that do not correspond to real browsers are filtered out.

#### Known limitations: Robot traffic detection

Some robots do not use their real user agent name. They pretend to be a regular browser. In this case, their traffic may not be correctly filtered out using the above mentioned method.

Microsoft Advertising has developed a series of methods to detect and exclude non-human traffic. These methods are applied in the process of ad-serving, before making the ad viewability script call.

### Impression counts

Microsoft Advertising impression counts closely match the ones gathered by the ad servers.

For this reason, except for fake traffic mentioned above (robotic impressions), no impressions are filtered out. Additional rules apply to viewable impressions though.

### Microsoft Advertising test traffic

Microsoft Advertising staff can potentially generate ad-impressions for testing purposes. In this case, they render the creatives in a preview mode such that no impressions are generated.

Therefore, tests run by Microsoft Advertising do not impact reporting and viewability results are not impacted.

### Projections

No projection is made for ad viewability on the Microsoft Advertising platform.

### Invalid traffic (IVT) guideline

Microsoft Advertising filters for sIVT and gIVT on:

- User ID (i.e. cookie ID)
- User agent
- JavaScript based detection
- IP address
- Domain where the ad placement is located
- Seller of the impression request (i.e. via ads.txt)

Our detection runs, depending on the method:

- On every single impression request
- Hourly on aggregated data
- Daily on aggregated data
- Weekly on aggregated data

We do not filter and subject all impression requests on the Microsoft Advertising platform to IVT filtration. Generally, thresholds and standards are checked on a weekly basis. Though there is no fixed cadence, we often update certain filters daily.

## Client-facing reporting

### Time zones

A day starts at 0:00 :00 am and ends at 23:59:59. The default time zone is New York (ET). Local time zones are also available in the reporting interface.

Microsoft Advertising processes data every hour.

### Quality assurance process

The Microsoft Advertising Quality Assurance (QA) process is a mix of automatic and manual verifications.

#### Automatic QA

On all measured impressions, trends are monitored automatically. Members and placements whose viewability rates vary out of range raise alerts that are analyzed by the engineering team.

For Quality Assurance purposes only, a sample of impression data is measured with additional indicators and processed on a QA platform.

The automatic verification process performs several analyses:

- Data consistency
- Technical verifications
- Performance per browser
- Object detection

#### Manual QA

Given the volumes managed by Microsoft Advertising (20 billion impressions measured per day), no manual QA is feasible.

Microsoft Advertising has created a 3-level support for ad viewability:

- TAMs (Technical Account Managers) are trained to answer most client questions.
- Ad viewability experts or SMEs (Subject Matter Experts) can investigate more complex questions that TAMs cannot solve.
- If necessary, SMEs can contact the ad viewability engineering team.

#### Quality improvement

A continuous process allows Microsoft Advertising to constantly improve its measurement. Feedback from the production team is shared with the engineering team. If necessary, the script is updated, and new tests are added.

### List of tests

On the QA sample, the following tests are run automatically:

#### At the object level

An impression can involve several objects (image, expand format, etc.).

Each object is checked for:

- control on duration limits (deviant behavior)
- object presence calculations (called 'Display Rate')
- detecting a non-standard size for an ad

#### At impression level

Each impression is checked for:

- control on visible surface
- control on placement performance
- control on duration
- control on page duration
- control on absolute duration, at least 1 pixel, (used for performance and fraud detection)
- technical control on script's context

#### At group level

On each group of data (member, placement, and creative) the following tests are run:

- browser results different from other browsers
- control on visible surface
- control on placement performance
- control on visibility rate
- control on duration
- control on page duration
- control on absolute duration, at least 1 pixel (used for performance and fraud detection)
- control on internal QA controller

Each group of data must contain a minimum number of impressions (1, 100, 1000 depending on the indicator) so that the average values do not have a high degree of variability.

### List of reported metrics

- Downloaded Impressions
- Measured Impressions
- Technical Measurement Rate
- Viewable Impressions
- Viewability Rate
- Non-Viewable Impressions
- Undetermined Impressions
- Viewable Distribution
- Non-Viewable Distribution
- Undetermined Distribution

Definitions of the accredited indicators are available in the [Introduction to Viewability](introduction-to-viewability.md).

All these metrics are available in a specific report called "**Viewability Report**". Note that this report excludes mobile web traffic, even though it is measured by Microsoft Advertising.

#### Other viewability indicators

Custom definitions can be used to determine viewable impressions. In this case, different indicators are used in reporting:

- Custom viewable impressions: number of impressions that successfully pass the custom definition
- Custom viewability rate = Custom viewable impressions / measured impressions

#### Mobile traffic

Viewability metrics are not segregated between desktop browsers and mobile browsers, except in the "**Viewability Report**" where mobile impressions are filtered out.

However, it is possible to run the [Site Domain Performance](../monetize/site-domain-performance.md) report and group by "Operating system".

### Retention period

Depending on the level of granularity, the data collected by Microsoft Advertising are stored for a specific period of time. See [Availability of Reporting Data](availability-of-reporting-data.md) for more information.

### Changes in description of methodology

Major changes to the methodology can be communicated to clients through Microsoft Advertising product communication mailing lists.
