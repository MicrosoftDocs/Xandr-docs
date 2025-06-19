---
title: Identity Manager in Microsoft Monetize 
description: Microsoft offers a transparent, secure platform designed to support your identity strategy, prepare for a cookie-less future, and drive maximum value across Windows and Microsoft Edge.  
ms.date: 06/16/2025
ms.author: shsrinivasan
---

# Identity manager in Microsoft Monetize 

> [!NOTE]
> This feature is currently in Beta and might undergo changes without notice. To enable this feature, contact your Microsoft Advertising Account Representative. Alternatively, you can contact our support team by completing the [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com/sign-in).

Microsoft offers a transparent, secure platform designed to support your identity strategy, to manage a wide range of existing and emerging signals and drive maximum value across Windows and Microsoft Edge. 

## Key highlights 
- Activate first-party data using Publisher Provided Identifiers (PPIDs) and supported universal IDs. 
- Leverage Microsoft and partner data to optimize demand and monetization. 
- Maintain control and compliance through data governance and secure integrations. 


### Publisher Provided Identifiers (PPIDs) 

PPIDs are publisher-defined, first-party identifiers that can be added via Microsoft’s identity framework for audience segmentation, enhanced frequency capping, cross-device targeting, and household targeting. These identifiers enhance targeting and measurement, while preserving user privacy.  
 
**Benefits of PPIDs:**
- **Enable proprietary first-party identifiers:** alongside other signals in a single bid request.
- **Support audience segmentation:** frequency capping, and enhanced personalization.
- **Comply with privacy standards:** sensitive data is not shared with third parties. 
- **Retain full control:** configure access and usage through the Identity Manager. 


### Navigate the identity landscape 

The advertising industry is adapting to signal loss and the rise of new channels by embracing alternative types of identifiers. These identifiers can be industry-wide, bidder-specific, or publisher-specific and for inventory monetization, publishers typically use multiple identifiers to cover different use cases, needs, and privacy controls. 

Due to this changing landscape, publishers need to have the ability to control the identifiers that they are using (or sharing with partners) at a granular level. Controls are increasingly important to ensure compliance with the privacy or use case requirements of leveraging separate identifiers. Microsoft's Identity Management Framework offers a powerful, intuitive toolset that allows publishers to manage these identifiers with precision, ensuring compliance and enabling monetization without compromise. 

## Identity management framework 

Identity Management Framework enables publishers to monitor and control how identifiers are used for monetization purposes. This is becoming increasingly important as emerging identity solutions are gaining momentum in the market and privacy regulations continue to change. The framework allows the publishers to retain fine-grained control over each identifier they opt to use, irrespective of whether it is their own identifier or a solution adopted across the entire industry. 

 ### Navigate the Identity manager 

If you do not yet have Identity Manager enabled in your seat, contact your Microsoft Advertising representative and designate a user who should have access. To access the Identity Manager in Microsoft Monetize, go to the vertical navigation pane on the left and select **Network > Identity Manager**. It contains two primary sections: 
- Identity Sources You Own 
- Identity Sources You Have Access To 

#### Identity Sources You Own

- The Identity Sources You Own section can be used to retrieve, create, update and delete an identifier in the platform. Additionally, owners can: 
    - Manage permissions for their identity solutions.  
    - View and edit member-level permissions, or control whether another Microsoft Monetize member can 
    - Pass the ID in a request 
    - Onboard the ID in a segment 
    - See the ID in log-level data. For more information, see [Identity Type service](../digital-platform-api/identity-type-service.md).
> [!NOTE]
> PPID onboarding is a prerequisite for an ID source to show up in this section, and once it's registered you can then use the Identity manager to manage permissions. 
- The Identity Sources You Own section includes the following fields: 
    - **ID:** The unique identifier created by Microsoft for the identity source. 
    - **Source:** Indicates the source of the identifier (e.g., LiveRamp, Warner Media). Each identifier must have a unique source. 
    - **Pass ID in Request to Monetize:** Specifies whether the ID can be included in bid requests sent to Microsoft Monetize for use in auctions. 
    - **Onboard ID to Segment:** Indicates whether IDs from this source can be onboarded into a segment for targeting. 
    - **See ID Value in Log-Level Data (LLD):** Indicates whether IDs from this source are included in log-level data exports. 
    - **Demand Side Platforms (DSPs):** Specifies whether non-Microsoft DSPs can receive the ID in bid requests from the Microsoft Advertising platform. 
    - **Prebid Server Premium (PSP):** Indicates whether the ID is shared with  Prebid Server Premium in bid requests. Controls for individual Demand Partners are configured in Prebid Server Premium.  
- To view more information about an identity source: 
    - Hover over the identity source name and select it. 
    - A details pane opens on the right, displaying the configured settings. 
    - The top section shows Base Permissions, or whether access is enabled, enabled for an allowlist, or disabled. 
    - These indicate whether capabilities such as Pass ID in Request to Monetize, Onboard ID to Segment, and See ID Value in LLD are enabled or disabled by default. 
    - To edit base permissions: 
        - Hover over the **Enabled/Disabled** label. 
        - Select the pencil icon to edit values. 
    - To assign custom permissions for individual member IDs: 
        - Select **+ Add Member-Level Permissions** button. 
        - Use the search box to find a Member ID or Member Name. 
        - After selecting a member, you can enable or disable the following options: 
            - Pass ID in Request to Microsoft Monetize 
            - Onboard User ID to Segment 
            - See User ID Value in LLD 
    - To view DSP-specific permission settings: Select the appropriate tab to display a list of DSPs with their permissions marked as **Enabled** or **Disabled**. 

#### Identity Sources You Have Access To 

- The Identity Sources You Have Access To section allows identity framework participants to manage permissions for all identity solutions that they are leveraging. Additionally, each publisher participant can: 
    - Choose the external bidder(s) permitted to access their identifier. 
    - Determine the partner(s) on the platform that are entitled to receive the identifier's value within their log-level data feeds. 
- This Identity Sources You Have Access To section includes the following subsections: 
    - **ID:** The unique identifier created by Microsoft for the identity source. 
    - **Source**:** The name of the newly registered source (For example, LiveRamp, Warner Media). This value must be unique to the identifier. 
    - **Owned By:** The member's name of the identifier’s owner. 
    - **Pass ID in Request to Monetize:** Indicates whether your seat is permitted to pass the ID in bid requests to Microsoft Monetize for use in auctions. This permission is controlled by the ID owner. 
    - **Onboard ID to Segment:** Indicates whether your seat is permitted to onboard IDs from this source into a segment for targeting. This permission is controlled by the ID owner. 
    - **See ID Value in LLD:** Indicates whether your seat is permitted to view the ID in Log Level Data (LLD) when accessing transaction logs. This permission is controlled by the ID owner. 
- To view detailed settings for a specific identity source: 
    - Hover over the identity source name and select it. 
    - A side pane opens, displaying all configured permissions and settings. 
- The top section displays Master Settings (Identity Owner Permissions), which control whether your seat can view the ID in Log Level Data (LLD). These permissions are managed by the ID owner. 
- The Base Permissions section reflects whether core capabilities (such as passing the ID in bid requests, onboarding to segments, and viewing in LLD) are enabled or disabled globally. These must be allowed by the ID owner to enable any member-level customizations. 
- To assign custom permissions for individual member IDs: 
    - Select **+Add Member-Level Permissions** button. 
    - Use the search box to find a Member ID or Member Name. 
    - Once selected, set the individual-level permission for See User ID Value in LLD to **Enabled** or **Disabled**. 
    - Select **Save** to apply the configuration. 
- To view DSP-specific permission settings: Select the appropriate tab to display a list of DSPs with their permissions marked as **Enabled** or **Disabled**. 

## Related topics
- [Identity Type service](../digital-platform-api/identity-type-service.md)
- [Identity Type Participant service](../digital-platform-api/identity-type-participant-service.md)