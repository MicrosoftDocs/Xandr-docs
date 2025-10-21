---
title: Microsoft Monetize - Create a Conversion Pixel
description: Explore creating a conversion pixel, a tool used to monitor user actions related to advertisements crafted by an advertiser.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Create a conversion pixel

A conversion pixel is used to track user actions in response to an advertiser's creatives, such as registering at a site or making a purchase. This page walks you through the process of creating a conversion pixel.

## Step 1. Get started

Go to the **Conversion Pixel**s screen (**Advertisers** \>  **Conversion Pixels**) and click the **+ New** button. This opens the **Create New Pixel** dialog.

## Step 2. Enter the conversion pixel details

In the **Details** section, enter a name that communicates the purpose of the conversion pixel, and then select how you want conversions to be attributed:

- **Hybrid (view/click)** - Attribute a conversion to the last time the user clicked or, if there were no clicks, the last time the user viewed one of the advertiser's creatives. This option is selected by default.
- **View** - Attribute a conversion to the last time the user viewed one of the advertiser's creatives.
- **Click** - Attribute a conversion to the last time the user clicked on one of the advertiser's creatives.

If the user has neither clicked on nor viewed one of the advertiser's creatives in an actual auction, the conversion will **not** be attributed.

## Step 3. Select the event category (optional)

Optionally, select a category that describes the type of conversion event you want for this line item. Setting an event category will not effect our optimization algorithms immediately. Instead, it provides our optimization team with valuable data for prediction that we can then start to test and incorporate. If you don't see a good match for your
type of conversion event, leave this field blank.

Event categories are:

- **Visit landing page** - A user visits your website after being served an ad.
- **View an item** - A user visits a page on your website that displays one or more products or services.
- **Add to cart** - A user adds one or more of your products or services to their shopping cart.
- **Initiate checkout** - A user begins the checkout process.
- **Add payment info** - A user adds payment information, such as a credit card number, during the checkout process.
- **Purchase** - A confirmed sale of your product or service.
- **Generate lead** - Collect lead information, such as email addresses or zip codes, from people interested in your business.

## Step 4. Set the attribution window

In the **Expiration** section, specify how far into the past you will look to attribute a conversion to a creative viewed or clicked.

- **Post View Interval**: default is 1 day; maximum is 30 days
- **Post Click Interval**: default is 14 days; maximum is 90 days

If you deselect expiration for your conversion pixel, the maximum attribution window will apply.

## Step 5. Select how many conversions you want to count

Depending on what kind of conversion you are tracking, you may be dealing with multiple conversions. In the **Repeat Conversions** section, you can choose whether you want to count more than one conversion per user, all conversions, or how often you want to count conversions. When using the "Count one conversion per user every ..." option, the maximum window is 32,767 minutes (about 22 days).

## Step 6. Add a piggyback pixel (optional)

On the **Piggyback Pixels** tab, you can input the URL of an image or JavaScript pixel to piggyback off the conversion pixel. You might do this to notify external servers about conversion events.

Add **piggyback pixels** with the following in mind:

- Image pixels can only piggyback off other image pixels, and JavaScript pixels can only piggyback off other JavaScript pixels.
- Image pixels can have only one piggyback pixel. If you need to piggyback multiple pixels, be sure to use a JavaScript pixel.
- There are no character limits to piggybacked pixel URLs in Microsoft Monetize, but browser/server URL limits may apply.

## Step 7. Save the conversion pixel

To finish adding the conversion pixel to the Microsoft Advertising platform, click the **Save** button. The pixel is then added to the Conversion Pixels list, where you can add it to your line item.

> [!TIP]
> The conversion pixel can be attached to a line item for valuation.
> [!NOTE]
> Conversion pixels show as **Paused** in the User Interface when they are not attached to a line item, or the attached line item is inactive.
> This is an indicator that the pixel will not be attributing any conversions. It is not attached to an object that those conversions can be attached. Once the pixel is attached to an active line item, the indicator will switch to **Active**. This does not impede its functionality, because the pixel state (in the API) is still active.

## Related topics

- [Export Conversion Pixels](export-conversion-pixels.md)
- [Conversion Pixels Advanced](conversion-pixels-advanced.md)
- [Reporting on Conversions](reporting-on-conversions.md)
- [Server-Side Conversion Pixels](server-side-conversion-pixels.md)
- [Conversion Attribution](conversion-attribution.md)
