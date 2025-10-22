---
title: API Segment Management
description: Learn creating, modifying and deleting segments. This page also covers best practices for managing data provider segments. 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: data-providers
ms.author: shsrinivasan
---


# API segment management

## API segment management

Data providers will need to use Xandr's impression bus API (api.adnxs.com) to create, modify and delete segments. For any API interaction, you will need the following:

1. Authorization: see [Authentication Service](../digital-platform-api/authentication-service.md)
1. Segment creation or modification: see [Segment Service](../digital-platform-api/segment-service.md)

## Best practices

When managing the data provider segments, the following best practices should be adhered to:

- **Use codes**: Integration codes (the "code" field on the segment service) allows a data provider to inject their own identifiers into the Xandr backend. This allows users to be added to segments using an alternative syntax, specifying the integration code rather than the Xandr ID. The primary benefit to using codes is that the API enforces unique code values within a single member. If integration codes are utilized for all data provider segments in a given Xandr member's account, the uniqueness check will ensure that duplicate segments are not created.
- **Keep segment names consistent**: In general, data provider segments use a consistent naming convention. This makes data provider segments easier to find by allowing the user to search in by data provider name or hierarchy structure. The details of the naming convention are below:
  - The name of the data provider is appended in parentheses, e.g., "Segment 1 (Data Provider Name)"
  - Hierarchies are denoted using the greater than symbol ("\>"), e.g., "Parent Group \> Child Group (Data Provider Name)"
  - The segment name must not be longer 255 characters, including the data provider name. If a segment name with the data provider name appended is longer than 255 characters, the segment name should be truncated to fit the data provider name.

    > [!TIP]
    > The "segment name" here corresponds to the value of the `short_name` field in the JSON used to create the segment (see [Segment Service](../digital-platform-api/segment-service.md) for more information).

- **Specify an expiry time**: Many integrations will only consist of adding users to segments and not removing users from segments. For this reason, it is necessary to specify a period of time after which a user will drop out of a segment if they are not added to that segment prior to the expiration. If no expiration time is specified, a user remains in the segment until they are explicitly removed or they purge their cookies.
- **Set max usersync pixels to 0**: (This is only relevant for audience segments that are being placed on a page.) By default, all client-side segment pixel calls will result in redirecting the user to a usersync pixel for at least one of Xandr's supply, demand or data partners depending on the pixel rotation and the number of times the user has already been synced in recent history. In order to avoid this usersyncing process, set the "max_usersync_pixels" parameter on the segment service to 0. This prevents the user from being redirected from the segment pixel to the usersync pixel. Please note that by setting this parameter to 0, it may limit the overlap between available inventory and users in the data provider segments. The usersync process enables communication about each user across multiple platforms outside of Xandr, giving a unified view of the user across a larger portion of internet traffic. For more information, see "User ID Syncing" in documentation.
- **Make sure clients are targeting just your segments on a single campaign**: Campaigns that are actively targeting segments belonging to multiple data providers may have data billing issues down the line because currently buyers only have visibility into campaign level spend and impressions rather than segment level visibility into spend and impressions within a campaign.
