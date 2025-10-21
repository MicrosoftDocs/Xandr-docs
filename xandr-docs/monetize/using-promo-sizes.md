---
title: Using Promo Sizes
description: This page provides FAQs on Promo Sizes. Learn advantages of using promo sizes and steps to enable them in this page. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---


# Using promo sizes

## Why use promo sizes?

There are two main use cases for promo sizes:

- Larger placements with fixed sizes and little demand on the large size can benefit from opening up to demand with smaller sizes.
- Smaller placements with fixed sizes can lift up revenues by opening up to larger sizes.

## How do promo sizes work?

When an impression allows multiple sizes (example: `size=300x250&promo_sizes=300x600`), we run a normal auction, but only allow creative sizes specified in the size and promo sizes fields to be eligible to serve. During the auction process, we initially evaluate line items to verify that all targeting criteria are met. If so, we look at all eligible creatives associated with the line items (based on size and ad-quality attributes) and factor in their individual bid prices. We then take the creative with the highest bid and submit it as a bid in the auction.

## Enabling promo sizes

### Step 1:

Be sure to create a sizeless placement. The sizes that you'd like to open your inventory up to will be passed in the tag.

### Step 2:

When exporting the placement, check the parameter **Allow additional sizes**.

This will add a parameter in the tag called `promo_sizes`. It is here that you'll pass in the sizes, separated by a comma.

Optional: The alignment option determines what alignment you'll use when the creative size served is smaller than the ad-slot.

### Step 3:

Export the tag to your publisher's page or to your adserver.

For example, if your main size is 300x250 and you would like to open to 300x600 and 300x1000, the tag will have the following form:

``` 
<SCRIPT SRC="http://ib.adnxs.com/ttj?id=1417164&size=300x250&promo_sizes=300x600,300x1000" TYPE="text/javascript"></SCRIPT>
```

If you choose to center the tag using the promo alignment option, it would have the form:

``` 
<SCRIPT SRC="http://ib.adnxs.com/ttj?id=1417164&size=300x250&promo_sizes=300x600,300x1000&promo_alignment=center" TYPE="text/javascript"></SCRIPT>
```

## FAQ

### How is the size reported in the Network Reports?

For impressions in Network Reporting, Microsoft Advertising reports on the size of each creative that serves.

For example, let's say 30 impressions were generated with this tag:

``` 
http://ib.adnxs.com/ttj?id=1418346&size=300x250&promo_sizes=300x600
```

If a 300x600 creative served 26 times and a 300x250 creative served 4 times, the impressions for the 300x600 creative and the impressions for the 300x250 creative would be reported separately.

### How is the size reported to other buyers in the Inventory Research Tool?

To determine the amount of available impressions, Microsoft Advertising reports on the parameter size of the tag. In other words, other buyers are only able to view impression availability based on the primary size that is passed in the tag.

### How are reserve prices applied?

If the placement is declared sizeless, and you have input the appropriate `promo_sizes`, you'll need to add a default creative for each size. The reserve price for each default creative may be different.

### Can external bidders buy several sizes on our `promo_sizes` tags?

Yes. External bidders use the promo sizes info to bid on the different sizes we pass in the `promo_sizes` parameter.

### Is there a way to avoid creatives serving in placements that use promo sizes?

Currently there is no way to prevent this from the buy-side.
