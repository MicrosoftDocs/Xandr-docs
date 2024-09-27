---
title: Yield Analytics Overview
description: This page provides basics on Yield Analytics.
ms.date: 10/28/2023
ms.custom: yield-analytics-ui
---

# Yield Analytics overview

This page deals with concepts on Yield Analytics.

## About Yield Analytics

Yield Analytics is a data analytics tool that helps publishers properly forecast, manage, price, and sell their ad inventory in order to maximize revenue.

## Basics of Yield Analytics technology

This is how Yield Analytics works behind the scenes:

### Integration

We integrate with an ad server, as well as many other systems. This includes:

- Order Management Systems
- DMPs (Data Management Platforms)
- First-party Data Systems
- Third-party Data Systems
- Additional Ad Servers (e.g.: Video Ad Server)

### Analysis

Yield Analytics integrates with the above systems and pulls the information into our system. We take log-level data. This means that rather than just looking at a certain set or “sampling” of data, Yield Analytics analyzes every single impression that ran through the ad server, video server, or any of the systems mentioned in the bullet points above. We run analytics on the data to forecast and emulate.

### Forecast

Forecasting for the client’s system - Yield Analytics not only analyzes for your site, but correlates that information to certain products within your system. We look at specific sites, sections, different audiences, etc. to better estimate how many impressions are going to be needed at those locations.

### Emulation

Emulating campaign delivery – Yield Analytics analyzes every line item in your server that is running. Based on our findings, we estimate which line items:

- Are most likely to serve
- May have delivery issues (under-delivering)
- Any issues that may cause financial consequence

Many ad servers can do everything that Yield Analytics can do as far as looking at campaign management, line delivery and forecasting. So why is Yield Analytics better?

## Methodology

A typical ad server will look at a sample set of data. This means that instead of looking at every impression that goes through your system, they’ll only look at a handful. From that, they’ll estimate their forecasting, campaign contention, etc.

Yield Analytics takes a census-based approach, which means we are looking and analyzing every single impression that goes through your system. This assists with two things:

- **Forecast highly targeted line items**

Within an ad server, since you are working with a sample set of data, some of those highly-targeted impressions may be missed. But Yield Analytics is looking at every single impression. Historically, it will give you the correct amount of impressions that have served at that particular line item – and then also accurately forecast it.

- **Future forecast**

If it is desired to do forecasting far into the future, Yield Analytics is looking at a larger set of the data so we have a better understanding of the behavior of your site. When you want to forecast three to six months in advance – Yield Analytics is going to have a better understanding of your system to determine the correct numbers for when you are requesting that forecasting information.

## Lookback window

A typical ad server looks back only 28 days and extrapolates that information for however long the forecast is being conducted. Yield Analytics holds information for as long as you allow us to access it, so then we can look as far back as that point in time.

Example: The start date of a campaign is Sept. 1. You allowed Yield Analytics to have access to your data going back to January 1. So you can “look back” to January 1 for historical data.

## Manual adjustments

In some cases, you may know that the ad server is likely to forecast incorrectly, so it's important that you can make manual adjustments within Yield Analytics to better forecast accurate numbers, based on your insider knowledge of how things really work.

One helpful way this feature can be applied is when you know your site is going to have a one-day spike in traffic. Example: there is going to be a high-traffic news story, or a major event is approaching and you want to raise the impression capacity for a particular time period. This can be accomplished within Yield Analytics as well.

## Seasonal models

When you know that you are going to have seasonal fluctuations in traffic, you can represent these changes within Yield Analytics. Example: You know that during the holidays your site typically has a 10% rise in traffic. You can add that percentage. The system will look at whatever the yield default is based on your historical data, and then you can adjust it to what you know will be an accurate representation of the amount of impressions that are going to occur on a particular site or in a specific area.

> [!NOTE]
> The importance of manual adjustments and seasonal models (see above) is if you are a seller, you are selling on a volume (impression) basis. You want to ensure that you are accurately selling what is available. You do not want to over or undersell. These two features allow the Sales team to pull as accurate numbers as possible - based on true, complete data.

## Spike mitigation

When you know you are going to have “one-time event” that will bring an abundance of traffic to your site, you are able to alert the ad server. The ad server is not going to know that it was some great story, or some viral video that drove all the traffic. The ad server is going to assume that spike is going to be there until it cycles out of their system. Within Yield Analytics you will are able to look at the historical data and determine that a spike of that magnitude is nearly impossible to occur, and chances are it will most-likely never happen again. Yield Analytics will account for a portion of those impressions, in the outside chance that it happens again. However, it does not account for the full spike. This feature greatly helps the Sales Team to accurately sell. They are not going to oversell based on that one-time spike, now that Yield Analytics has applied the spike mitigation – they will be able to sell the correct amount.

## Calendar view

When you are booking sponsorships, and you are trying to determine where there is availability for a specific product, you can look at the calendar view. This is going to show you what is available (color code = green), and what is not (color code = red). In an ad server, you have to look day-by-day to try to determine this information.

## Bulk queries

If a query is made within Yield Analytics that involves thousands of line items, it will typically take the system a few minutes to analyze and process all that data. You have the ability to save the findings in a bulk query folder. This allows you to continue working while the system is generating the query result.

> [!NOTE]
> Yield Analytics only processes once per day, because of how large the log file is. It is impractical to do it more than that, because yield analyzes every single impression in the system.

## Forecast

The primary thing Yield Analytics is known for is forecasting. This includes:

- Understanding the inventory capacity
- Understanding various ways that impressions can be consumed
- Availability for custom and pre-defined products

## Delivery management

Delivery management incudes everything that occurs post-sale. Yield Analytics emulates ad server delivery to understand under-delivery risk. We are analyzing campaign contention, to better forecast what ads are most likely to serve, which line has a higher priority, and various ways to optimize revenue.

## Pricing analysis

Pricing analysis is where clients get some of the biggest value from Yield Analytics. With this information, you can potentially uncover different audiences that you were unaware of. This is accomplished by looking historically at:

- Revenue delivery
- Item pricing
- Pricing discrepancies
- Yield Analytics increase potential for specific products

## KPI reports (Key performance indicators)

Since Yield Analytics is merging data across many different platforms, we make combined insights across an array of dimensions.

## Programmatic management

If you are integrated with different SSPs, Yield Analytics can pull that information into our system. We can determine where there are high pockets of demand, based on metrics such as fill rate, eCPM, CPM, RPM, etc. We manage the yield to capture revenue through different programmatic channels.

Yield Analytics functionality and the resulting gained information benefit many sectors. Included are:

### Sales

Sales is going to look through ways to drive revenue through client solutions. They are building out Sales plans, and receiving RFPs from the clients and responding back to them. They also manage the client relationship.

### Ad ops

Ad Ops teams ensure all that revenue gets delivered. They also implement client plans, and solve technical issues on a basic level.

## Yield Analytics management

This is the primary team in the workflow. The Yield Analytics management responsibilities include:

- Optimizing revenue
- Managing
- Pricing
- Prioritizing campaign delivery
- Ownership of KPI reporting

## Finance

Even though most clients use an order management system, Yield Analytics has the ability to manage your revenue, handle fine invoicing, track bad debit, and other related functionality. This is sometimes accomplished through a third-party data system. (e.g.: Adjuster)

## Management

Management can be defined as “accountable for revenue”, and personnel who are responsible for making strategic decisions. Some examples of typical information that is available in high-level reporting are:

- Who is my top advertiser?
- What is my advertiser’s eCPM across the board?
- What is the eCPM for every single advertiser?
- How are my salespeople doing?
- How are my top products doing?

When reports are being run, the content will not be broken into historical and forecasted data points. If you would like to see historical data in reports – ensure that you are selecting dates from the past. If the date overlaps between historical and forecasted, you will receive a blend of that data.

A product in the Yield Analytics system is a combination of targeting attributes from the ad server. The ad server has logic built into it to determine where and when an ad is going to serve. As a convenience, in our system we have different product types.

We’ve created a few different product types that are going to look at the targeting attributes that are pulled from the ad server. Those targeting attributes are going to be imported into Yield Analytics. The most common ones are going to be size, site, page, position, audience segments, geo-location, etc.

When you are running reports you typically want to filter to certain product types, based on what you are looking for. There are three different types of products, which are described below.

## Rate card

The Rate Card Product is something that is frequently sold by the sales team that represents the product catalog. This may have a rate card price associated with it.

> [!NOTE]
> If the client has an order management system integrated with Yield Analytics, that information needs to get pushed over from the order management system to our system. If they do not have an order management system, they can create all the Rate Card Products within Yield Analytics.

## Reports

This is a product created specifically for reporting purposes. They are products based on the desired types of reports clients want to run. Yield Analytics will look at what the reporting product is and look at the targeting attribute. Then we will access the ad server to find line items that had some aspect of that targeting attribute. We then pull the information and reflect it in the reports. Some examples are:

- How are different Sites/Sections performing?
- Compare Mobile app vs. Mobile web
- All Mobile products

> [!NOTE]
> When the client is first on-boarded, a Yield Analytics representative will walk them through the process of how to create a product, and offer some ideas of different products that they can create.

## Custom

A Custom Product is a unique product referenced by the order lines within the ad server. It is usually a product that is sellable, but is not commonly sold. Custom Products are mainly used as a convenience if you would like to access specific information on a specific, exact product.

> [!NOTE]
> Yield Analytics encourages the client to create a substantial amount of products when they are first on-boarded. This allows them to begin gathering historical data from the outset.

In Yield Analytics, revenue is broken out two different ways: contracted and earned. Impressions are broken out three different ways: contracted, scheduled, and consumed. Below is a brief explanation of each type of impression.

## Contracted

Contracted is anything that comes from the order management system.

## Scheduled

The ad server is broken out from the order management system. When information is pushed to the ad server, it will show up as scheduled. There are clients who have an order management system who will incorporate a “buffer” of scheduled impressions to ensure they deliver in full.

> [!NOTE]
> If a client doesn’t have an order management system, (they just have an ad server) - contracted and scheduled will always be the exact same number.

## Consumed

Consumed impressions are what actually ran, served, or what is forecasted to run on the ad server.

Consumption type is another way to break down sell-through rate. A basic example of traditional sell-through rate is: Out of a million impressions, 900 thousand were sold. That equates to a 90% sell-through rate.

Consumption type asks the basic question: Was something on a particular product directly or indirectly sold to? (Back to the example) Out of those 900 thousand impressions, were those ads actually targeted to that specific product, or did that product just have an abundance of capacity?

## Direct consumption

Direct consumption is very straightforward. On the order line, the item is targeted and served in the exact same location.

Example: There is a product in our system named News 300 x 250 home page. The targeting characteristics would be Site=News, Size=300x250, Page=Homepage. The order line is targeting to that exact same string. Those ads are appearing on the News 300x250 homepage. Every time an ad would serve, that would be considered direct consumption. If you bought this particular product, the ad is serving directly on that product.

## Contained consumption

Contained consumption correlates to direct consumption. Every site has a hierarchy. If you are a newspaper, for example, you are going to have your different sites/sections such as news, politics, sports, local, etc. Within each of those sections is going to be further subsections that “trickle down” for that particular site/section.

Example: Our example is no longer the home page but you are looking at the news 300x250 run-of-site. If an ad is targeted to any particular site that falls under news – that would be considered contained consumption. I have an order-line that is going to news/politics 300 x 250 – that falls anywhere within news. That one ad (or impression) would show up as a contained consumption. It is not directly targeting news, but it is targeting a subsection that is still considered ‘related’ to that particular product.

## Indirect consumption

The concept of indirect consumption is best shown by an example.

Example: I am located in New York, and accessing the news section. There is a line item that is targeted “run-of-site”, and the DMA=New York. The ad is a car ad, which is also targeted to DMA=New York.

That impression was considered, sold through an ad, and it was served. It did not serve because I was on news, or politics. It served because I was in New York. This is called indirect consumption. It basically answers the question: Was that ad served and targeted to that particular product, or was there some other targeting characteristic on another line item that happened to serve there?
