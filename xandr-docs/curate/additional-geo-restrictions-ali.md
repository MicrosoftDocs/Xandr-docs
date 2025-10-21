---
title: Microsoft Curate - Additional Geo Restrictions
description: In this article, learn about the geographic targeting restrictions for impressions that the users are viewing. These restrictions help in customizing content delivery.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-curate
ms.author: shsrinivasan
---

# Microsoft Curate - Additional geo restrictions

If you are advertising in connection with any financial, insurance, education, career and employment, and/or housing services, you may not use postal code for the purpose of personalizing advertising, segmenting, or profiling customers.

In addition to country, you can also restrict the impressions you target based on other geographic details of the users viewing them.

## Geographic targeting considerations

Although restricting by country is highly accurate, the more specific the targeting, the more imprecise the results. This is especially true when targeting locations as granular as cities, metro codes, and zip codes. Also, depending upon which geographic restriction options you choose, you may significantly reduce the likelihood of a match and thus jeopardize delivery.

## Geographic restrictions overview

To restrict the impressions you target based on other geographic details of the users viewing them, select **Additional Geo Restrictions** next to **Geography** in the **Audience & Location Targeting** section of your line item and follow the instructions for the relevant geographic targeting option referenced below:

- Restrict users by country, region, or city
- Restrict users by metro code
- Restrict users by postal code

> [!NOTE]
> If you have not targeted at least one country on your line item, you will be required to target a region, city, metro code, or postal code.

### Third-party buying filters

For third-party buying, geographic targeting is limited by any existing country settings in your Third-Party Buying Filters at the network level. If countries are included in your Third-Party Buying Filters, only those countries and the regions and cities within them will be available for targeting. If you target (include) geographies at the Region, City, Metro Code, or Postal Code level, Microsoft Advertising will use these settings to derive the country target to be compared with your Third-Party Buying filters.

## Restrict users by country, region, or city

When creating ALIs, you will be required to include at least one geographic location. You can either chose to target an entire country, or use the **Additional Geo Restrictions** section within **Audience and location targeting** to include/exclude specific regions, or cities.

- The **Countries** list shows all of the countries that can be targeted. You can include countries or drill into a country to see its regions/states.
- The **Regions** list is more granular than countries. Generally speaking, regions are based upon whatever method the country in question uses to divide itself into parts. For example, regions within the United States are states. Canada is divided into its provinces, and India is divided into its states and union territories. The **Regions** list shows all of the regions/states that can be targeted. You can either include or exclude regions/states or drill into a region/state to view its cities. When you exclude a region, its cities are not available for further inclusion or exclusion.
- The **Cities** list shows all of the cities that can be targeted. You can either include or exclude cities.

### Sorting locations

You can sort countries, regions, or cities by name or ID using the column headers, or use the search field to find a specific location.

> [!WARNING]
> Do not add conflicting geographic targeting at multiple levels. For example, if you are including the United States, Canada, and Mexico, and then you also include US zip codes, only the US zip codes targeted will be served. In this scenario, zip code targeting will automatically limit the targeting to the US only. Similarly, do not target both the region of Arizona and the metro code of New York, because geo restrictions are an AND relationship.

## Restrict users by metro code

Metro codes are available in 13 countries. Available metro codes range from large cities such as New York City, United States, or Oslo, Norway, to smaller cities such as Rochester, NY, United States. Unless you are excluding an entire "country" in country targeting, you will target all metro codes by default. However, on the **Metro Code** tab, you can narrow your targeting to include or exclude specific metro codes.

The countries that support metro code targeting are:

- Aland Islands
- Australia
- Canada
- China (Diji Shi cities)
- Finland
- France (Departments)
- Germany (German Nielsen Metro Codes)
- Korea, Republic of (Si/Gun/Gu)
- New Zealand
- Norway
- Russian Federation (Federal Districts)
- United Kingdom (ITV Regions)
- United States (Metro Code/MSAs)

## Restrict users by postal code

> [!NOTE]
> You can't target more than 4,000 postal codes per line item.

On the **Postal Code** tab, once you select a country, you can include up to 4,000 postal codes using a comma-separated or line-separated list. Postal codes can be alphanumeric strings of up to 14 characters and can contain a space or hyphen. Unlike other types of geographic targeting, postal codes may only be included (not excluded).

> [!NOTE]
> Certain legitimate ZIP or postal codes are unrecognizable or invalid within the Microsoft Advertising geography targeting system. This can happen because [Digital Envoy](https://www.digitalelement.com/), a Microsoft Advertising partner that handles geolocation data, can't recognize a ZIP or postal code's existence until an IP address (user) has been associated with it. Postal codes that don't exist in the system often represent obscure or otherwise small geographical zones with minimal internet activity.

As a guide to how postal codes should be formatted for each country, consult the list below.

| Country | Sample Postal Code |
|---|---|
| Australia | 7470 |
| Austria | 9992 |
| Brazil | 99990-000 |
| Canada | Y1A 6T5 |
| China | 860700 |
| Czech Republic | 798 62 |
| Finland | 99999 |
| France | 95880 |
| Germany | 99998 |
| Hungary | 9985 |
| India | 855107 |
| Italy | 98168 |
| Japan | 999-8317 |
| Mexico | 99994 |
| Netherlands | 9999 XA |
| Norway | 9990 |
| Poland | 99-440 |
| Portugal | 9980-032 |
| Romania | 927250 |
| Russian Federation | 694923 |
| Spain | 52080 |
| Sweden | 984 94 |
| Switzerland | 9658 |
| United Kingdom | ZE3 9JJ |
| United States | 99950 |

If your list contains postal/zip codes that don't exist in the Microsoft Advertising database, you will be presented with an error message and given the chance to correct and resubmit any invalid postal codes. Some common formatting errors that may generate an error message are:

- **Excel-Truncated Zeros**: Excel may truncate leading zeros from postal codes if they are numeric (06514 becomes 6514). However, an alphanumeric postal code such as "0AH 135" would not be affected.
- **Country**: Postal codes can only be added for one country at a time.

> [!NOTE]
> Ranges are not supported. You will need to add each individual postal code to the list or import them from a CSV, Excel, or Text file.

## Restrict users by postal code lists

> [!NOTE]
> At the line item level, you can target:
>
> - both a postal code list and an individual postal code (which does not belong to the list)
> - either a postal code list or an individual postal code (which does not belong to the list)
>
> The include and exclude functionality needs be consistent between the postal code list and an individual postal code.

You can include and exclude postal code lists and individual postal codes from targeting on a line item.

To target specific postal code lists available to you, select the **Postal Codes** section within **Additional Geo Restrictions**, and then use the **Postal Code List** tab. You can search for available postal code lists by ID or name, and then select the **green check** to include a list or the **red dash** to exclude a list. For the United States, you can target the full 9-digit postal code (also known as zip +4). For example, 10010-7456.

## Restrict users by political districts

> [!NOTE]
> Postal code list, postal code, and political district include/exclude functionality should be consistent.

Political Geography Targeting allows political buyers to target geographies based on legislative district boundaries. The feature is available within the existing geo targeting module in Microsoft Invest, and it's called "**Political District (US Only)**". The Political District Targeting allows buyers to target the following political geography levels:

- Congressional District
- State Senate District
- State House District

## Related topics

- [Object Hierarchy](object-hierarchy.md)
- [Buy-Side Targeting](buy-side-targeting.md)
- [Postal Code Lists](postal-code-lists.md)
