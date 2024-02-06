---
title : Support for Overriding Country and Zip Codes for iOS
description : Mobile SDK allows the publishers to override the country codes and zip codes. 
ms.custom: ios-sdk
ms.date : 10/28/2023
---


# Support for overriding country and zip codes for iOS

## Overview

Mobile SDK allows the publishers to override the country codes and zip
codes. The SDK uses City/DMA/Country information from standard feed (log
level data) for reporting purposes. However it is required to overwrite
these values from reverser geocoded latitude and longitude data (if
available) to keep the data sanity intact. Reason being, if those values
are not overwritten, log level data will point to the ip-address based
locations and eventually will project wrong data set especially with
mobile data.

## Properties

| Property | Type | Attribute | Description |
|---|---|---|---|
| `geoOverrideCountryCode` | String | readwrite | Indicates a string value to override country code. |
| `geoOverrideZipCode` | String | readwrite | Indicates a string value to override zip code. |


``` 
/**
* An AppNexus geoOverrideCountryCode  is a string value which allows publishers to override country code.
*/
@property (nonatomic, readwrite, strong, nullable) NSString *geoOverrideCountryCode;
 
/**
* An AppNexus geoOverrideZipCode  is a string value which allows publishers to override zip code.
*/
@property (nonatomic, readwrite, strong, nullable) NSString *geoOverrideZipCode
```

## Example

The properties can be accessed:

**Objective C**

``` 
//Set
ANSDKSettings.sharedInstance.geoOverrideCountryCode = @"US";
ANSDKSettings.sharedInstance.geoOverrideZipCode = @"10010";
.......
//Get
NSString* countryCode = ANSDKSettings.sharedInstance.geoOverrideCountryCode;
NSString* zipCode = ANSDKSettings.sharedInstance.geoOverrideZipCode
```

**Swift**

``` 
//Set
ANSDKSettings.sharedInstance().geoOverrideCountryCode = "US"
ANSDKSettings.sharedInstance().geoOverrideZipCode = "10010"
.......
//Get
let countryCode = ANSDKSettings.sharedInstance().geoOverrideCountryCode;
let zipCode = ANSDKSettings.sharedInstance().geoOverrideZipCode
```






