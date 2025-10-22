---
title: Support for Overriding Country Codes and Zip Codes on Android
description: This page covers setter methods like setGeoOverrideCountryCode, setGeoOverrideZipCode and getter methods like getGeoOverrideCountryCode and getGeoOverrideZipCode which are used by publishers to override the country codes and zip codes.      
ms.custom: android-sdk
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: mobile-sdk
ms.author: shsrinivasan
---


# Support for overriding country codes and zip codes on Android

Mobile SDK allows the publishers to override the country codes and zip codes. The SDK uses City/DMA/Country information from standard feed (log level data) for reporting purposes. However it is required overwrite these values from reverser geocoded latitude and longitude data (if available) to keep the data sanity intact. Reason being, if those values are not overwritten, log level data will point to the ip-address based locations and eventually will project wrong data set especially with mobile data.

## Methods

Use the following methods to override country and ZIP codes.

**setGeoOverrideCountryCode**

Setter method which assigns a country code . It will pass the country code string as the argument in the method.

``` 
/**
 * Overrides the SDKs automatic location retrieval.
 * The countryCode will be passed to request parameters only if it isn't empty
 *
 * @param countryCode The countryCode value to use in the ad call. To reset, pass null.
 */
 public static void setGeoOverrideCountryCode(String countryCode) {
 Settings.getSettings().countryCode = countryCode;
 }
```

**setGeoOverrideZipCode**

Setter method which assigns a zip code. It will pass the zip code string as the argument in the method.

``` 
/**
 * Overrides the SDKs automatic location retrieval.
 * The zipCode will be passed to request parameters only if it isn't empty
 *
 * @param zipCode The zipCode value to use in the ad call. To reset, pass null.
 */
 public static void setGeoOverrideZipCode(String zipCode) {
 Settings.getSettings().zip = zipCode;
 }
```

**getGeoOverrideCountryCode**

Getter method that returns the country code value that is set using **setGeoOverrideCountryCode**.

``` 
/**
 * Returns the countryCode value that is set using {setGeoOverrideCountryCode}
 * */
 public static String getGeoOverrideCountryCode() {
 return Settings.getSettings().countryCode;
 }
```

**getGeoOverrideZipCode**

Getter method that returns the zip code value that is set using **setGeoOverrideZipCode**.

``` 
/**
 * Returns the zipCode value that is set using {setGeoOverrideZipCode}
 * */
 public static String getGeoOverrideZipCode() {
 return Settings.getSettings().zip;
 }
```

## Example

The methods can be accessed as follows:

**Java**

``` 
//Setter
SDKSettings.setGeoOverrideCountryCode("US");
SDKSettings.setGeoOverrideZipCode("10010");
  
  
//Getter
SDKSettings.getGeoOverrideCountryCode();
SDKSettings.getGeoOverrideZipCode();
```
