---
title: Selling Programmatic Guaranteed Deals
description: In this article, find information about what PG selling line items are and how to create and sell PG deals to various clients.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Selling Programmatic Guaranteed deals

Programmatic guaranteed (PG) selling line items provide a workflow for you to for create and sell PG deals to buyers who use Microsoft Invest and other partner DSPs.

PG deals combine the certainty of direct sales with the power of programmatic, enabling publishers to programmatically execute direct deals with buyers. With PG deals, you have the power of guaranteed selling within a bidding environment using deal IDs. Instead of using traditional insertion orders, Microsoft Advertising PG offerings unlock the world of direct buying and selling through centralized, programmatic channels. They also bring the advantage of commitments to programmatic-oriented buyers and sellers, enabling far greater predictability for your deals.

PG selling line items are used to create fixed price deals with specified impression budgets, forecasts in the ad server, reservations, and guaranteed pacing and delivery.

A PG selling line item defines a negotiated order with a buyer, including:

- **Revenue Type and Floor Pricing** - how the advertiser has agreed to pay you

  - **CPM** ("fixed price" deals) that compete in the auction at a fixed price whenever the buyer bids above that price

- **Priority** - the buyer's ranking in the auction, and also whether or not open-auction bids are allowed to compete with the deal line item in the auction

- **Budget** - the deal's impression goal target

PG selling line items offer some of the following advantages:

- ability to run and accept programmatic guarantees with programmatic buyers
- streamlined execution and reporting of guaranteed media buys
- frequency and reach management within the PG deal
- predictable revenue

## Eligible DSP partners

- Microsoft Invest
- Google DV360
- Infillion (MediaMath)
- The Trade Desk - **CTV only**
- AdForm
- Roku OneView
- Bidtheatre
- Adobe
- Yahoo DSP
- StackAdapt

## PG Deals for Microsoft Monetize ad server clients

Creating PG deals as a Microsoft Monetize Ad Server client entails wide-scale deal customization. These types of PG deals are handled through header bidding, and they allow guaranteed deals, sales, and reporting to all take place within Monetize. PG deals created and sold through Microsoft Monetize Ad Server are especially advantageous when your deal buyers use Microsoft Invest. For information on creating a PG deal through Microsoft Monetize Ad Server, see [Create a Programmatic Guaranteed Deal](create-a-programmatic-guaranteed-selling-line-item.md).

> [!IMPORTANT]
> Creating and selling PG deals through Microsoft Monetize Ad Server is currently a **beta** feature.

## PG Deals for Microsoft Monetize clients

As a Microsoft Monetize client, you have two options for PG deal creation:

- **Microsoft Monetize** - configuring targeting, pacing, and other PG deal parameters in your desired third-party ad server through a placement-tag integration.
  
    For information on creating a PG deal through Microsoft Monetize, see [Create a Programmatic Guaranteed Deal that Uses Third-Party Ad Server Pacing, Tag Integration](create-a-programmatic-guaranteed-selling-line-item-ssp.md).

    > [!IMPORTANT]
    > PG deals creation through Microsoft Monetize is currently for display only.

- **Microsoft Monetize Ad Server** - configuring all PG deal parameters within Monetize through header bidding. This method is advantageous when your deal buyers use Microsoft Invest.

    For information on creating a PG deal through Microsoft Monetize Ad Server, see [Create a Programmatic Guaranteed Deal](create-a-programmatic-guaranteed-selling-line-item.md).

Additionally, the two PG selling options have these respective benefits and trade-offs:

| Microsoft Advertising Ad Server | Microsoft Monetize |
|---|---|
| Header-bidding integration | Tag-based integration |
| Streamlined beginning-to-end deal configuration | Greater setup flexibility |
| Access to advanced PG configuration options | Simple PG configuration workflow |
