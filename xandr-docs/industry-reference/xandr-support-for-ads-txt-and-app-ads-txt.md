---
title: Xandr Support for Ads.txt and App-Ads.txt
description: Implement Ads.txt and App-Ads.txt to integrate support, boost ad campaign reliability, and safeguard revenue against fraudulent impressions.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: industry-reference
ms.author: shsrinivasan
---

# Xandr support for Ads.txt and App-Ads.txt

> [!WARNING]
> The information in this document is based on the latest [Ads.txt specification for the IAB](https://iabtechlab.com/ads-txt/) as of January 22, 2018, and [App-Ads.txt specification](https://iabtechlab.com/wp-content/uploads/2019/03/app-ads.txt-v1.0-final-.pdf) as of March 2019. This information is subject to change based on IAB updates to the specification.

In the online advertising ecosystem, many buyers are concerned that fraudulent impressions will negatively impact their advertising, resulting in campaign unreliability and lost revenue. Xandr takes these concerns very seriously, and ads.txt and app-ads.txt are some tools among a range of strategies we employ to ensure the quality of inventory and the validity of impressions.

Ads.txt and App-Ads.txt (also known as [Authorized Digital Sellers](https://iabtechlab.com/ads-txt/) or Application Authorized Digital Sellers)  are an initiative put forth by the [IAB Technology Laboratory](https://iabtechlab.com/) as a way to help publishers ensure inventory is sold only through authorized dealers and partners. The goal of ads.txt and app-ads.txt is to give publishers more control over who sells their inventory and help prevent counterfeiting, while giving buyers confidence that they're purchasing approved inventory.

Ads.txt files are used to declare authorized sellers of display inventory on domains. App-Ads.txt files are used to declare authorized sellers of application inventory.

> [!NOTE]
> For additional details about the IAB's work on this initiative, see [About Ads.txt](https://iabtechlab.com/ads-txt-about/) on the IAB website.

Xandr supports the `Ads.txt` and `App-Ads.txt` initiatives, and works with publishers, resellers, buyers, and bidders on implementation.

> [!NOTE]
> Ads.txt Adoption and Support
>
> **Seller Impact:** Xandr has been enforcing
> Ads.txt compliance since **January 24, 2018** whenever ads.txt files are detected, and began enforcing app-ads.txt compliance in August of 2019.
>
> - Ads.txt checks are performed daily.
> - App-Ads.txt checks are performed weekly.
> - **If ads.txt or app-ads.txt files are present, Xandr disables buying from parties that are not directly identified through publishers' ads.txt / app-ads.txt files as authorized resellers.**
> - Deals, Managed, and external Bidder demand is not impacted by ads.txt / app-ads.txt enforcement. *If an ads.txt or app-ads.txt file is present, we disable buying from parties that are not directly identified through the publisher’s ads.txt files as authorized resellers*.
>
> **Buyer impact:** Xandr encourages all sellers to ensure they are listed in the ads.txt files of the inventory they are selling on our system.
>
> - For more information about this process, see the IAB's [How To Ads.txt](https://iabtechlab.com/how-to-ads-txt/).
>
> - There is no buyer opt-in process as this is default buying behavior. For additional questions regarding how ads.txt adoption may impact Xandr clients, please contact [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com).

## The Ads.txt and App-Ads.txt file

In practice, ads.txt and app-ads.txt files are the name of files that publishers can create and add to their websites. This file is a plain text file that lists names and information about authorized ad networks, SSPs, and exchanges that have permission to sell the publisher's inventory.

> [!TIP]
> This idea is similar to [robots.txt](http://www.robotstxt.org/), a file that is used by website owners to give instructions about their site to web robots (such as search engine crawlers) about which parts of their website can be crawled and which should be off-limits.

- Web Publishers place the ads.txt file on their domains at a URL following the format `website.com/ads.txt`.
- App publishers place the app-ads.txt file, [per IAB recommendations](https://iabtechlab.com/wp-content/uploads/2019/03/FAQ-for-ads.txt-and-app-ads.txt-UPDATED-March-4-2019.pdf), on the root of the developer website URL associated with their application in the relevant app store where the application is hosted.

Within the ads.txt / app-ads.txt file is a list showing each approved partner, along with each partner's tech platform (Xandr, Google, etc.), account ID, and relationship to the publisher. The file gives publishers a way to list all of their approved SSP, ad network, and exchange partners (both direct and resellers). DSPs can then choose to leverage the information in the ads.txt file in order to ensure authorized resale compliance.

All ads.txt / app-ads.txt files must have the following format:

`advertising-system-domain, member-id, relationship`

For example, let’s say a publisher worked with four Xandr accounts. The ads.txt /app-ads.txt file on their domain would look like this:

```
appnexus.com, 123, DIRECT
appnexus.com, 456, RESELLER
```

The first line of this example specifies that the publisher is using Xandr (xandr.com) directly with a member ID of 123. The second line specifies that the domain can also be resold through a reselling partner with Xandr's member ID 456.

> [!NOTE]
> The member-IDs shown in the example file above must be replaced by actual member IDs.
>
> Check the [IAB FAQ for Ads.txt and App-Ads.txt](https://iabtechlab.com/wp-content/uploads/2019/03/FAQ-for-ads.txt-and-app-ads.txt-UPDATED-March-4-2019.pdf) for more information on structuring files and other processes related to ads.txt / app-ads.txt.

### Certification ID (optional)

There is a fourth, optional field known as a certification authority identifier that sellers may choose to include in ads.txt files. Sellers add this unique ID as an additional measure to demonstrate validity and trustworthiness of the advertising platform being used Xandr has an identifier issued by the [Trustworthy Accountability Group](https://tagtoday.net/aboutus/)(TAG).

To include the Xandr's TAG-ID, add the ID f5ab79cb980f11d1 to the end of each Xandr line in your ads.txt file:

`appnexus``.com, 958, DIRECT, f5ab79cb980f11d1`

### Ads.txt / App-Ads.txt for sellers

Here are some simple steps sellers can take to start using Ads.txt and App-Ads.txt.

> [!NOTE]
> Anywhere in this document you see a reference to the member ID, Xandr is referencing your Xandr member ID, not your publisher ID. The ads.txt team at IAB has approved the use of the Xandr member ID in publishers' ads.txt / app-ads.txt files, similar to how Google is planning to use network ID.

#### Publishers

Publishers on the our platform should follow these steps to create and implement ads.txt files that contains their Xandr seller information.

1. Start by gathering up the list of all partners - ad networks,
    a. exchanges, and SSPs - where publisher inventory is sold.

1. For each partner, collect the ad serving domain (appnexus.com), the Xandr member ID, and your relationship with the member (DIRECT or RESELLER).

1. Use any text editor to create a plain text file.

1. For publisher direct seats, add a line to the file that looks like this:

    `appnexus``.com, <publisher member ID>, DIRECT`

   > [!NOTE]
   >
   > Sellers can find their member ID in Microsoft Monetize by navigating to the **Monetization Dashboard** and looking for the ID at the bottom of the screen.
   >
   > :::image type="content" source="media/publisher-direct-seats.png" alt-text="Screenshot that explains how sellers can find their member ID in console by navigating to the Monetization Dashboard and looking for the ID at the bottom of the screen.":::
   >
   > Be sure to note that you need your member ID, not your publisher ID.
   > For further questions, please reach out to [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com).

1. For publishers working with partners who have Xandr seats, create lines that look like this, with one partner per line:

    `appnexus.com, <partner member ID>, RESELLER`

Partners should be able to provide their member IDs.

1. Save the file with the name **ads.txt** or app-ads.txt - depending on the type of inventory you are declaring the file for - and upload it to the root folder for the publisher domain, or app developer url declared in the relevant app store. (ie./ **example.com/ads.txt** or **appdeveloper.com/app-ads.txt**)

1. Validate your ads.txt / app-ads.txt file using one of many free online resources for this purpose. This will help ensure that your ads.txt / app-ads.txt file has been configured correctly.

#### Publisher reselling partners

Resellers working with publishers should make sure publishers include them in their ads.txt / app-ads.txt files to show that the reseller has permission to sell their inventory. This can be done by sending publishers the instructions in the "Publishers" section above (or simply directing them to this page) and a request to be added to their ads.txt files.

> [!NOTE]
> Resellers with multiple member IDs should give all IDs to their publishers and ask them to include each ID on a separate line of the ads.txt file.
> [!WARNING]
> To be correctly listed, resellers must work with publishers to ensure that their reseller member ID is included in the ads.txt file.

### Ads.txt / App-Ads.txt for buyers

The following sections describe how Xandr works with Ads.txt for Monetize buyers and external bidders.

#### Buyers

As a benefit to Microsoft Invest buyers, Xandr will begin to use Ads.txt / App-Ads.txt information to strengthen our existing inventory quality programs. Buyers working with sellers who have not yet implemented ads.txt / app-ads.txt should please direct them to this page to get started.

#### External bidders

For external bidders and DSPs planning to crawl publisher domains to gather seller information from ads.txt /  app-ads.txt files, there are two key pieces of information required in order to correctly map inventory from Xandr sellers: domain and member ID. Xandr sellers will have a domain of **appnexus.com**. The IDs of publishers, exchanges and SSPs will be sent in the `seller_member_id` field in the OpenRTB request.

## Additional client tools and resources

[IAB Ads.txt / App-Ads.txt Spec](https://iabtechlab.com/ads-txt/) - IAB Techlab

## Related topics

- [Ads.txt/App-Ads.txt FAQ for Buyers](ads-txt---app-ads-txt-faq-for-buyers.md)
- [Ads.txt/App-Ads.txt FAQ for Sellers](ads-txt---app-ads-txt-faq-for-sellers.md)