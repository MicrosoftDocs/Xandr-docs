---
title: Create a PSP Configuration
description: In this article, find step-by-step instructions on how to create and set up a new PSP configuration.
ms.date: 10/28/2023
---

# Create a PSP configuration

Once inventory has been [Integrated with Prebid Server Premium (PSP)](integrate-with-psp.md), [Global Settings have been reviewed](add-or-edit-psp-global-settings.md), and [Demand Partners have been enabled](add-or-edit-a-demand-partner.md), inventory must be mapped to Demand Partners via PSP configurations. These mappings allow PSP to send bid requests with demand partners’ parameters so the partners can identify the inventory and better represent it to their buyers, increasing yield and honoring publisher settings such as floors and ad quality.

- Each configuration targets a portion of publisher inventory in Monetize, either by a set of flexible targeting (geography, inventory type, key value, etc.) or by explicitly specifying Monetize objects (placement, placement group, publisher).  
- Each configuration includes one or more demand partners the publisher would like to bid on the inventory.  
- Each demand partner specifies the required and optional parameters they want to receive in their open-source [Prebid Server Go adapter](https://docs.prebid.org/dev-docs/pbs-bidders.html), which are surfaced in PSP. These allow the partner to match the bid request to objects in their platform.  
- Publishers fill out demand partner parameters with values mapped to objects in each partner’s platform, typically another supply-side platform (SSP).  

## Demand partner requirements

All demand partners the publisher would like to bid on the inventory defined in a PSP configuration must be added to the same configuration. Before creating the first set of configurations, review requirements with each of the [planned PSP demand partners](prebid-server-premium-demand-partner-integrations.md) to determine a mapping strategy. Some partners pull information dynamically from the bid request (ad size, geographic location, language, etc.) while others may require separate parameter mappings, and in turn, PSP configurations. If a demand partner requires very granular mapping to objects in their platform, that will determine how other partners are mapped and how many configurations are required. The better a demand partner can identify the inventory (either through the bid request or static Prebid parameters), the more information they can provide to their buyers, increasing publisher revenue.

Demand partner parameters can be found:

- In the PSP configuration UI, as detailed below:
- [On the Prebid site](https://docs.prebid.org/dev-docs/pbs-bidders.html) with full context and details
- In the [PSP demand partner schema service](../digital-platform-api/demand-partner-schema-service.md)

## Create a configuration

Follow these steps to create a new PSP configuration:

1. Starting in the Monetize navigation bar, select the **Publishers Menu** then click **Prebid Server Premium**. This loads the default Demand Partner Configurations screen.
1. In the top section of the **Demand Partner Configurations** screen, click the **New** button.

### Configuration details

- Enter the name of the configuration. Ideally, this is a high-level description of the inventory or strategy to differentiate from other configurations in the UI and reporting.
- Once the configuration is saved, bid requests will be sent to any included demand partners. Toggle the configuration status to **Disabled** before saving to prevent requests from being sent.
- Proceed with the steps in each of the sections below.

## Monetize inventory selection

This section determines which publisher bid requests will initiate the PSP configuration. Targeting can be as broad (run-of-site) or as narrow (a Monetize placement ID only in the United States when a key value is present) as the publisher needs.

### Media types

Select one or more ad formats (banner, video, native) to request from demand partners. If a bid request includes multiple formats, each demand partner will only receive requests for the [format(s) they support](prebid-server-premium-demand-partner-integrations.md). These selections will also filter the available demand partners in the next section to those that support at least one of the selected media types.

#### Targeting method

Select one of the options below which determine how the inventory is selected.

- **Targeting Profile**: Also known as flexible configurations, using this method is strongly recommended as it offers the most control. A variety of targeting options such as geographic location, system, and key value can be used to specify which inventory is included.
- **Placement, Placement Group, or Publisher**: This legacy option allows a single object (placement, placement group and all its placements, or a publisher and all its child objects) to be targeted. Each object (ID) can only be targeted in a single configuration.

> [!NOTE]
> **Auction configuration selection**:
>
> Each auction only uses one PSP configuration and its set of demand partner parameters. If an auction matches multiple configurations, the configuration at the highest level of the hierarchy will be selected. The hierarchy from highest to lowest is:
>
> 1. Targeting Profile (if available, any lower configurations are ignored)
> 1. Placement
> 1. Placement Group
> 1. Publisher
>
> When multiple Targeting Profile configurations are eligible, the user-defined **Priority** setting of the configuration is used to determine which configuration to use. When multiple Targeting Profile configurations of the same Priority are present, the configuration with the higher (more recent) ID will be used in the auction.

### Targeting profile options (recommended)

After setting the **Targeting Method** as **Targeting Profile**, proceed with the optional targeting described below.

#### Targeting profile description

Optionally, provide a label to further define the targeting beyond what is used in the configuration name.

#### Configuration priority level

Select a value, 1 being the lowest, 20 being the highest, to inform Monetize which configuration to use if the targeting of multiple configurations overlap on a single bid request. As mentioned in the purple note above, only one configuration and its set of demand partner parameters can be used in an auction.

#### Geography targeting

Select bid requests based on varying granularities of geographic targeting, such as:

- Country
- Region
- City
- Metro code
- Postal code
- Latitude/longitude

#### Inventory targeting

- **Supply source**: Select bid requests based on one or more of the following:

  - Monetize objects (placement, placement group, publisher)
  - Content categories
  - Specific domains
  - Apps
  
  When a publisher is excluded, its placement groups and placements are not available for further inclusion or exclusion. When a placement group is excluded, its placements are not available for targeting.
  
  When a top-level category is excluded, its sub-categories are not available for further inclusion or exclusion. When targeting more than one universal category, the categories have an OR relationship. For example, targeting "Custom Category 1" and "Custom Category 2" would request bids on inventory in either category.
  
- **Inventory type**: Select bid requests for web or app inventory. Default allows both web and app.

- **Key/Value**: Target bid requests containing specific key values. Key values must be defined in **Monetize** > **Network** > [Key Values](https://monetize.xandr.com/tools-key-value) first.

- **Banner size targeting**: Restrict which banner bid requests demand partners receive based on the size of the ad slot. Sizes must first be defined in **Monetize** -> **Network** -> **Tools** -> **General** -> **Custom Sizes** -> **Manage Custom Sizes** via the [Creative Manager](https://monetize.xandr.com/creative-sizes).

#### Environment targeting

- **Device Type Targeting**: Target broad categories of user devices. Mobile includes phones and tablets. CTV includes televisions, set top boxes, and game consoles.

- **Systems Targeting**: Target technical attributes detected in the bid request such as operating system, browser, language, device model, and mobile carrier.

After applying all desired targeting, proceed to the **Demand Partners** section below.

## Placement, placement group, publisher options (legacy alternative to Targeting Profile)

After setting the **Targeting Method** as **Placement**, **Placement Group**, or **Publisher**:

1. Click into the box to select from a list of available objects in the Monetize seat, or type within the box to search by object name or ID.
1. Click to choose the desired object (placement, placement group, or publisher) to associate with the configuration. All bid requests for this object (and any child objects) will initiate this configuration and send its parameters to demand partners.
1. Optionally, limit which bid requests are sent to demand partners by the dimensions below, then proceed to the Demand Partners section below.

### Banner Ad size targeting (Legacy)

To restrict which banner bid requests demand partners receive by the size of the ad slot, click the selection field to view a list of options. Sizes must first be defined in **Monetize** -> **Network** -> **Tools** -> **General** -> **Custom Sizes** -> **Manage Custom Sizes** via the [Creative Manager](https://monetize.xandr.com/creative-sizes).

#### Operating systems targeting (Legacy)

To restrict which bid requests demand partners receive by the operating system of the user, click the selection field to view a list of options. For more information, see the [Operating System-Families API Service](../digital-platform-api/operating-system-families-service.md).

## Demand partners

For a demand partner to receive bid requests for the inventory defined in the section above, they must be added to the configuration. While there is no technical limit to the number of partners that can be included in a configuration, the more partners there are, the lower their win rates tend to be, and some may start to bid less often if at all. Best practice is to start testing with 3 to 4 demand partners then gradually add more, while [continuously optimizing](prebid-server-premium-analytics.md) and removing any under-performing partners.

1. Click **Add Demand Partner** to view the side panel.
1. Click in the selection box to view a list of demand partners enabled in [PSP Global Settings](add-or-edit-a-demand-partner.md) or type to search by name.
1. Click to select a demand partner. Their required and optional parameters are displayed. Partner parameters are also available in the [Demand Partner Schema API Service](../digital-platform-api/demand-partner-schema-service.md) and on the [Prebid site](https://docs.prebid.org/dev-docs/pbs-bidders.html).
1. Referencing identifiers and values from the partner’s platform, fill out their required and optional parameters.
1. Click **Save**.
1. Click **Add Demand Partner** to add additional partners. More partners can be added at any time.

> [!NOTE]
> If the desired demand partner is not listed:
>
> - Ensure a media type the partner supports is selected.
> - Ensure the demand partner is added on the **Global Settings** page under **Demand Partners**, as described in [Add or Edit a Demand Partner](add-or-edit-a-demand-partner.md).
>
> A full list of available PSP demand partners and their supported media types is available [here](prebid-server-premium-demand-partner-integrations.md).
> [!NOTE]
> Publishers do not need to select Xandr as a demand partner. All standard managed/direct and real-time bidding (RTB) demand in the Monetize marketplace will operate and flow as it normally does outside of the PSP context. If Xandr is selected as a demand partner, do not input parameters that map the configuration to inventory within the same Member ID (Monetize seat). The Xandr demand partner is for mapping inventory from the publisher's member/seat to a different Monetize network seat where that partner has reselling authority. This use case is strongly discouraged unless the secondary Monetize seat has unique demand or data to offer.

### Save and send bid requests

1. If bid requests should be sent to the demand partners immediately, click **Save** at the top of the configuration setup screen. Otherwise, deselect **Enabled** in the **Configuration Details** section, then click **Save** to save all changes in an inactive state.

All settings tied to configurations can be changed at any time.

Once live, review [Prebid Server Premium Analytics](prebid-server-premium-analytics.md) resources to monitor and optimize PSP demand. [PSP common issues and best practices](psp-common-issues-and-best-practices.md) also contains key guidance.

## Run of site configurations

To ensure any inventory not captured by other configurations is sent to demand partners, consider creating a run-of-site or fallback configuration where the **Targeting Method** is **Targeting Profile** with no other, or limited geographic targeting, applied. **Before enabling such a configuration**, ensure:

- **Demand partner parameters** are populated; otherwise, no bid requests will be sent.
- **Configuration priority level** is set to 1 or another low value.
- Other configurations with more detailed targeting, and therefore more specific objects mapped in demand partners’ platforms, are created and given higher configuration priority level values (20 being the highest).

## Related topics

- [Manage a PSP Configuration](manage-a-psp-configuration.md)
- [Manage PSP Configurations in Bulk](manage-psp-configurations-in-bulk.md)
- [Add or Edit PSP Global Settings](add-or-edit-psp-global-settings.md)
- [Add or Edit a Demand Partner](add-or-edit-a-demand-partner.md)
- [Prebid Server Premium Demand Partner Integrations](prebid-server-premium-demand-partner-integrations.md)
- [Config Service](../digital-platform-api/config-service.md)
- [PSP Campaign Objects Service](../digital-platform-api/campaign-object-service.md)
- [Common Issues and Best Practices](psp-common-issues-and-best-practices.md)
