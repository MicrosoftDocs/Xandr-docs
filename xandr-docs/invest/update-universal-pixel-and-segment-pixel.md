---
title: Microsoft Invest - Update Universal Pixel and Segment Pixel integrations for user consent signals 
description: A guide for advertisers who operate in EEA on how to provide Microsoft with user consent signals for Universal Pixel and Segment Pixel integrations.
ms.date: 04/10/2025
ms.author: rupambaruah
---

# Microsoft Invest - Update Universal Pixel and Segment Pixel integrations for user consent signals

As part of our commitment to respect user privacy and consent choices, we have updated our privacy practices for Universal Pixel (UP) and Segment Pixel (SP) integrations. In this guide, we will explain how you can update your UP and SP integrations to provide us with user consent signals. Microsoft will soon start to strictly require consent signals for all requests from users within the European Economic Area, the United Kingdom and Switzerland. Advertisers will have a choice to provide Transparency and Consent Framework signals as defined in IABs (Interactive Advertising Bureau) TCF (Transparency & Consent Framework) Framework. Alternatively, Microsoft will accept binary consent signals. Binary signals are an option available for advertisers who do not use a CMP (Consent Management Platform) that complies with the IAB's TCF. Please note that this guide does not constitute legal advice, nor is it intended to address all legal or self-regulatory requirements that may apply to your organization or the organizations you are working with.

## What are binary user consent signals?

Binary user consent signals are simple indicators that tell us whether a user has given consent for the processing of their personal information for advertising purposes. Unlike TCF signals, which provide granular and standardized information about the purposes and vendors for which consent is given, binary signals only indicate a yes or no answer. Binary signals are useful for advertisers who do not use a CMP that supports TCF, or who want to have more flexibility and control over their consent signals. However, binary signals also have some limitations, such as not being able to specify the purposes and vendors for which consent is given or not being able to revoke or modify consent once given. Therefore, we recommend that you use a CMP that complies with TCF whenever possible, as this will provide you with more benefits and features, such as transparency, interoperability, and user choice.

## How to update your Universal Pixel on websites using TCF Consent Management Platforms?  

If your website uses a CMP that complies with TCF, you do not need to make any changes to your Universal Pixel integration, as our JavaScript can automatically receive consent signals through pre-defined APIs (Application Programming Interfaces).  

## How can I verify whether a TCF Consent Management Platform is being used on a website?

One way to verify whether a TCF Consent Management Platform is being used on a website is to reach out to the website owner or a person responsible for the consent banners and ask them if their CMP supports TCF and offers APIs described in the TCF specification. These APIs are used to communicate consent signals between the CMP and other parties, such as us. If the CMP does not support TCF or does not offer these APIs, then you need to update your UP to pass binary consent signals as described below.  

Another way to evaluate whether a TCF API is available on a given website is by following these steps:  

- Visit the webpage in your browser.

- Open the browser developer tools and navigate to the JavaScript console.  

- Copy and paste the code below into your JavaScript console and hit enter.  

```javascript
//COPY BELOW 
const callbackFunction = (tcData, success) => { 
    validEvents = ['tcloaded', 'cmpuishown', 'useractioncomplete']  
    
    if(success && validEvents.includes(tcData.eventStatus)) {  
        console.log('%c TCF v2.2 CMP available on this page.', 'color: green; font-size: 20px'); 
    }  
}  

try {  
    window.__tcfapi('addEventListener', 2, callbackFunction);  
} catch(err) {  
    console.log('%c TCF v2.2 CMP NOT available on this page.', 'color: red');  
}  
//COPY END 
```

This code will check if the window object has a __tcfapi method, which is used by TCF compliant CMPs to communicate consent signals. If the method exists, it will add an event listener that will execute a callback function when the consent data is loaded. The callback function will log a message to the console indicating that a TCF CMP is available on the page. If the method does not exist, it will catch the error and log a message to the console indicating that a TCF CMP is not available on the page.

## How to update your Segment Pixel on websites using TCF Consent Management Platforms?

### Segment Pixel Deprecation Notice

Please note that segment pixels are a legacy feature that will soon be deprecated and will no longer allow segments to be created. This is due to the third-party cookie deprecation in several major browsers like Google Chrome and Microsoft Edge. Therefore, users are expected to migrate these integrations to universal pixel, which allow Microsoft to communicate with newly introduced Browser APIs.

It is highly recommended to use the opportunity of the currently requested changes to switch from legacy segment pixels to universal pixels in the process. The option to update segment pixel to the new consent requirements is reserved for clients that may require additional time to move to universal pixels. However, this option should be considered as a temporary option.

Segment pixels are a way of tracking user behavior and sending data to us through HTTP requests. These requests are made by the browser when the user visits a web page that has a segment pixel embedded in it. The segment pixel can be integrated directly on the web page or through a tag management system that allows you to add scripts and tags to your website. However, since segment pixels are plain image URLs, they cannot access the TCF APIs that provide consent signals from the CMPs. Therefore, if you want to use segment pixels with TCF compliant CMPs, you need to append additional parameters to the segment pixel URLs and provide the TC signals as parameter values. This will allow us to respect the user consent and process the data accordingly.

#### Before

```html
<img src="https://secure.adnxs.com/seg?t=2&add=123456789" width="1" height="1" />
```

#### After

```html
<img src="https://secure.adnxs.com/seg?t=2&add=123456789&gdpr=1&gdpr_consent=<GDPR-CONSENT-STRING>" width="1" height="1" /> 
```

Please note that the value of ```<GDPR-CONSENT-STRING>``` must be replaced by the actual value of the consent string provided by the CMP.

You can find further information on how to pass consent signals for segment pixels in our [documentation](segment-pixels-advanced).  

## How to update your Universal Pixel on websites without TCF Consent Management Platforms?

To update your UP integrations for binary user consent signals, you need to follow these steps:

- Collect user consent: You need to properly collect user consent for the processing of their personal information for advertising purposes. You can use your own consent mechanism or a third-party CMP that does not support TCF, if you ensure that the consent is valid, clear, and informed.

- Load the universal pixel on your page.

- Toggle the binary consent mode as outlined below before making any event calls through your Universal Pixel integration  

### Set negative binary consent if consent has not been granted (Default)

```javascript
<!-- Xandr Universal Pixel - Set negative binary consent --> 

<script> 
    pixie('consent', 'default', { 
        'ad_storage': 'denied' 
    });  
</script> 
```

### Set positive binary consent if consent has been granted

```javascript
<!-- Xandr Universal Pixel - Set positive binary consent --> 

<script> 
    pixie('consent', 'update', { 
        'ad_storage': 'granted' 
    });  
    
</script> 
```

You can find further information on how to enable the binary consent mode for Universal Pixel in our [documentation](set-up-consent-mode-in-universal-pixel).  

## What happens if advertisers fail to provide consent signals for Microsoft pixel integrations?

Consent signals are required by Microsoft to process user data in accordance with our terms and policies. User data includes user IDs that are stored on the end device, such as cookies or mobile identifiers. This data allows Microsoft to perform various tasks, such as associating the user with audience segments that can be used for targeting ads or using data to validate conversion events that measure the effectiveness of ad campaigns. If advertisers fail to provide consent signals, Microsoft will not be able to process user data and therefore will not be able to perform these tasks. This could result in a significant decrease in the size of audience segments or the ability to measure the performance of ad campaigns.

## What qualifies as consent under TCF?

The Transparency and Consent Framework (TCF) serves as a standardized method for compressing and communicating user consent choices across various platforms. As part of utilizing this framework, our systems will specifically check for the user’s consent choice for purpose 1 (storing and accessing information on the device) and vendor permissions for the vendor Xandr Inc. (ID 32) tied to the consent string. If you are providing TCF consent signals, please ensure to request user consent for our vendor and all applicable purposes.

## Why should you consider switching Segment Pixels for Universal Pixel in the process?  

One of the advantages of using Universal Pixel over Segment Pixels is that it is more future-proof and compatible with the upcoming changes in the online advertising industry. Segment Pixels rely on third-party cookies, which are being phased out by major browsers due to privacy concerns. This means that Segment Pixels will become less effective and reliable over time, as they will not be able to track users across different websites and devices. Universal Pixel, on the other hand, is based on JavaScript, which can interact with browser-based API solutions that browsers like Chrome and Edge will introduce as alternatives to third-party cookies. These solutions, such as the Privacy Sandbox, aim to balance user privacy and advertiser needs, and will require JavaScript-based pixels to function. Therefore, we recommend that you switch from Segment Pixels to Universal Pixel as soon as possible, as this will ensure that your campaigns continue to perform well and reach your target audiences.
