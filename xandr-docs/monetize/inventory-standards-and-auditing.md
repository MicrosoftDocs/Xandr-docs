---
title: Inventory Standards and Auditing
description: In this article, find information about the procedure and details of inventory standards and auditing.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Inventory standards and auditing

Microsoft Advertising devotes significant resources toward safety and quality on both sides of transactions taking place on our platform.

Buyers on our platform may submit their creatives for human auditing by the Microsoft Advertising audit team. The manual audit process includes checking technical and content criteria as well as offer type categorization to enable the seller protection features on the platform. Buyers may self-audit their creatives, but because many sellers allow only Microsoft Advertising audited creatives, self-auditing may reduce access to inventory outside of one's network.

Additionally, all creatives (including publisher default ad tags) on Microsoft Advertising's platform are continuously monitored for overt malvertising threats and suspicious behavior regardless of audit status. Our auditing technology also adds metadata to the creatives.

You can find more information about creative auditing in [Creative Standards](creative-standards.md).

Similarly, Microsoft Advertising monitors, both manually and automatically, inventory sources available on our platform, and blocklists URLs that do not meet platform standards. The Microsoft Advertising auditing team regularly audits new inventory and reaudits existing inventory to apply categorization and metadata at the domain level. This data can be leveraged on the demand side to further target campaigns or to restrict delivery.

## Process and procedure

For advertisers' safety, Microsoft Advertising provides two modes of inventory auditing.

First, we maintain a strict set of baseline criteria for excluding unacceptable inventory from being sold over our platform. Any inventory that we detect as falling within these criteria will be added to our platform blocklist. We reject all requests made to our servers originating from an inventory on our blocklist, including auction requests, pixel calls and user syncing activities.

Second, inventory available on our platform may be tagged with content categories, brand sensitive attributes, and intended audiences, either by the Microsoft Advertising audit team or by sellers.

- **Platform-Reviewed**: Microsoft Advertising reviews a sub-set of domains available on our platform. Metadata is provided on a domain level, and is based on the referrer we receive from the browser, ad server, or aggregator.
- **Sellers**: Auditing may also be done by the network, aggregator, or exchange that represents the publisher.
  
  > [!NOTE]
  > While we believe that our audited domains are of a high quality, the nature of the internet is such that we cannot provide any guarantee regarding the nature or content of any inventory sold on the platform. For questions about this, or to report miscategorized inventory or inventory that should be banned under our blocklist criteria, contact us via [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com) and select "Inventory Quality" as the request type.

## Standards

### Prohibited and restricted inventory

> [!NOTE]
> In the past, filtered impressions on inventory flagged as violating platform standards would serve blanks. Now, these impressions follow seller preferences for impressions with no demand. As with all impressions that follow this workflow, sellers will be charged the applicable fee.
> [!IMPORTANT]
> See the [Part of Service Policies](../policies-regulations/index.yml) for policies that apply globally on our platform.

Microsoft Advertising works hard to create a safe and trusted ad marketplace. We use various methods to continuously monitor traffic that passes through our impression bus, whether it comes from Microsoft Advertising tags, white-labeled tags, or third-party ad tags. This includes, but is not limited to, direct publisher relationships and media buys placed with other ad servers, networks, platforms and supply sources.

In applying content policies, we do not differentiate between inventory that is monetized by the owning member or that is resold via the platform.

Except for creatives banned by our [Part of Service Policies](../policies-regulations/index.yml), networks may run any creatives on their own inventory regardless of audit status (for more information, see [Creative Standards](creative-standards.md)). To allow this, under the Ad Quality manager for each publisher, leave **"Ban unaudited creatives for direct advertisers"** unchecked.

### Restricted content

In keeping with our inventory standards, there are categories of sites that will not serve impressions. These categories are outlined clearly in our Service Policies under Policies for Selling.

### Unauditable inventory

Domains listed as "unauditable" will be available for managed line items, any buyers who set you as a "trusted partner", and those that have not enabled inventory quality filtering.

- **Desktop apps and toolbars**: Sites whose purpose is the download of browser toolbars.

- **Automatic redirection to other sites**: Domains which automatically redirect to a different URL.

- **Website does not appear to function**: Sites that appear to be broken or have no content.

- **Website has no ads on page**: Sites that contain no visible ad units.

  To contest the audit status of a site, contact us via [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com) and select "**Inventory Quality**" as the request type. In the request, please detail your relationship with the publisher and add a brief description of why you believe the site has not been audited correctly.

## Inventory categorization standards

### Sensitive attributes

These are qualities of a site or page that advertisers may wish to exclude. We encourage all members to use these categories and descriptions when self-classifying their own inventory.

- **Political**: Editorial content that is predominantly aimed at furthering the cause of any political party, organized campaign, or informal pressure group.
- **Social media**: A website platform primarily intended for independent publication by site users of personal thoughts and links, and interaction among its members.
- **Photo & video sharing**: Independent publication by site users of photographs and videos utilizing a tool provided by the site.
- **Forums (moderated)**: Online forums, comments areas, discussion groups, and newsgroups where people exchange ideas about a common interest, where the user's comments are subject to editorial control or moderation by a site publisher, or require the user to log in or supply personally identifying information like an email address. Moderation may occur either before or after the user's contribution is posted.
- **Forums (unmoderated)**: Sites or parts of sites primarily comprising forums, comment areas, discussion groups, and newsgroups not subject to any editorial control or moderation by or on behalf of the site publisher, and not requiring any login or identifying information from the user.
- **Incentivized clicks**: Sites or parts of sites containing content, such as links, to be clicked on by live users who subsequently receive some reward or incentive.
- **Non-English languages**: Sites where a significant portion of the text appears in a language other than English, and the site appears targeted to a non-English-speaking audience.
- **Streaming media**: Sites or parts of sites containing streaming music or embedded videos or flash games.
- **Toolbars, plug-ins or extensions**: Ad-supported browser plug-in inventory installed with user consent. More information on compliant toolbars can be found in our [Part of Service Policies](../policies-regulations/index.yml).
- **Contextual nudity**: Non-sexual, non-vulgar nudity that appears as an incidental aspect of the site without being the focus of it.

### Intended audience

This category is used to indicate the age range of the target audience for the content on the site. A site falls into "General audiences" unless it contains content that is specifically targeted toward children, young adults, or the 18+ category. (18+, also called "mature", does not include so-called "adult content", i.e. pornography.)

- **Children**: A site or part of a site whose content is specifically targeted toward children. For special rules that apply to child-directed sites, see the Child-Directed Inventory Policy section of our [Part of Service Policies](../policies-regulations/index.yml).
- **Young Adults**: A site or part of a site whose content is specifically targeted toward young adults.
- **General Audiences**: A site or part of a site which has no particular intended audience and whose content is appropriate for all ages.
- **Mature (18+)**: A site or part of a site whose content is not appropriate for children or young adults under 18.
