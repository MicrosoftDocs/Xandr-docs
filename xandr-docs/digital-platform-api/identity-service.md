---
title: Identity Service
description: Learn about the Identity service, the Identity Management Framework, and how publishers can monitor and control the identifiers for monetization purposes.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Identity service

> [!NOTE]
> This service currently is in Alpha. It is still under development and may be subject to change without notice. Contact your Xandr Account Representative to get enabled.

The advertising industry is embracing new types of identifiers as the deprecation of third-party cookies is imminent in near future. These identifiers can be industry-wide, bidder-specific, or publisher-specific and for inventory monetization, publishers typically use multiple identifiers to cover different use cases, needs, and privacy controls.

Due to this changing landscape, publishers need to have the ability to control the identifiers that they are using (or owning) at a granular level. It is in order to comply with the privacy or use case requirements of leveraging separate identifiers. By providing publishers with an efficient, granular, and easy-to-use tool set, the Identity Management Framework of Microsoft platform aims to address this requirement.

## Identity Management Framework

Using the Identity Management Framework, publishers can monitor and control how identifiers are used for monetization purposes. This is becoming increasingly important as emerging identity solutions are gaining momentum in the market and privacy regulations continue to change. The framework allows the publishers to retain a fine grain controls over each identifier they opt to use, irrespective of whether it is their own identifier or a solution adopted across the entire industry.

The Identity Management Framework contains the following APIs that are the crucial in implemeting this solution:

- [Identity Type Service](identity-type-service.md)
- [Identity Type Participant Service](identity-type-participant-service.md)

## Permissions

These APIs can be used to create, update and delete various identifiers in the platform as well as managing permissions. However there is various degrees of accessibility to these functions of the APIs and it is determined by defining following roles and associating them with the users:

- Microsoft Admin (can register a new identity source, control updates, or delete a source).
- Owner (typically a publisher that can control updates or delete an identity source).
- Participant (have child control privileges).

For more details about the APIs, see the reference pages mentioned above.
