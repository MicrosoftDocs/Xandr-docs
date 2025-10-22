---
title: API references overview
description: In this article, explore API services and information about each service.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# API references overview

This page lists Xandr's API services, as well as the following information about each service:

- **Name:** The name of each service in the table below is also a link to its documentation.
- **Endpoint:** The URL where you can reach the service.
- **Context:** Whether the service is primarily used for buying, selling, etc.
- **Read-only?:** Whether the service responds to https requests other than `GET`.

## Apps marketplace services

Below are examples of a few apps marketplace services. For details of all the services for apps marketplace, see [Apps Marketplace Services](apps-marketplace-services.md).

| Service Name | Endpoint | Context | Read-only? |
|:---|:---|:---|:---|
| [App Installation Service](app-installation-service.md) | [https://api.appnexus.com/app-installation](https://api.appnexus.com/app-installation) | Apps | No |
| [Developer Service](developer-service.md) | [https://api.appnexus.com/developer](https://api.appnexus.com/developer) | Apps | No |
| [Fee Service](./partner-fee-service.md) | [https://api.appnexus.com/fee](https://api.appnexus.com/fee) | Apps | No |

## Authentication services

Below are examples of a few authentication services. For more details, see [Authentication Service](authentication-service.md).

| Service Name | Endpoint | Context | Read-only? |
|:---|:---|:---|:---|
| [Authentication Service](authentication-service.md) | [https://api.appnexus.com/auth](https://api.appnexus.com/auth) | Foundation | No |
| [Account Recovery Service](account-recovery-service.md) | [https://api.appnexus.com/account-recovery](https://api.appnexus.com/account-recovery) | Foundation | No |

## Buy-side services

Below are examples of a few buy-side services. For details of all the services for buy-side, see [Buy-Side Services](buy-side-services.md).

| Service Name | Endpoint | Context | Read-only? |
|:---|:---|:---|:---|
| [Advertiser Service](advertiser-service.md) | [https://api.appnexus.com/advertiser](https://api.appnexus.com/advertiser) | Buying | No |
| [Broker Service](broker-service.md) | [https://api.appnexus.com/broker](https://api.appnexus.com/broker) | Buying | No |
| [Campaign Service](campaign-service.md) | [https://api.appnexus.com/campaign](https://api.appnexus.com/campaign) | Buying | No |

## Change log services

Below is an example of a change log service. For more details, see [Change Log Services](change-log-services.md).

| Service Name | Endpoint | Context | Read-only? |
|:---|:---|:---|:---|
| [Change Log Services](change-log-services.md) | - [https://api.appnexus.com/change-log](https://api.appnexus.com/change-log)<br>- [https://api.appnexus.com/change-log-detail](https://api.appnexus.com/change-log-detail) | Buying | Yes |

## Member services

Below are examples of a few member services. For more details, see [Member Service](member-service.md).

| Service Name | Endpoint | Context | Read-only? |
|:---|:---|:---|:---|
| [Member Service](member-service.md) | [https://api.appnexus.com/member](https://api.appnexus.com/member) | Foundation | No |
| [Member Profile Service](member-profile-service.md) | [https://api.appnexus.com/member-profile](https://api.appnexus.com/member-profile) | Foundation | No |

## Profile service

Below is an example of a profile service. For more details, see [Profile Service](profile-service.md).

| Service Name | Endpoint | Context | Read-only? |
|:---|:---|:---|:---|
| [Profile Service](profile-service.md) | [https://api.appnexus.com/profile](https://api.appnexus.com/profile) | Buying/Selling | No |

## Read-only services

Below are examples of a few read-only services. For details of all read-only services, see [Read-Only Services](read-only-services.md).

| Service Name | Endpoint | Context | Read-only? |
|:---|:---|:---|:---|
| [Browser Service](browser-service.md) | [https://api.appnexus.com/browser](https://api.appnexus.com/browser) | Buying | Yes |
| [Country Service](country-service.md) | [https://api.appnexus.com/country](https://api.appnexus.com/country) | Buying | Yes |
| [Media Type Service](media-type-service.md) | [https://api.appnexus.com/media-type](https://api.appnexus.com/media-type) | Buying | Yes |

## Reporting services

Below are examples of a few reporting services. For details of all report services, see [Reporting Services](reporting-services.md).

| Service Name | Endpoint | Context | Read-only? |
|:---|:---|:---|:---|
| [Report Service](report-service.md) | [https://api.appnexus.com/report](https://api.appnexus.com/report) | Reporting | No |
| [Report Status Service](report-status-service.md) | [https://api.appnexus.com/report-status](https://api.appnexus.com/report-status) | Reporting | Yes |
| [Saved Report Service](saved-report-service.md) | [https://api.appnexus.com/saved-report](https://api.appnexus.com/saved-report) | Reporting | No |

## Sell-side services

Below are examples of a few sell-side services. For details of all sell-side services, see [Sell-Side Services](sell-side-services.md).

| Service Name | Endpoint | Context | Read-only? |
|:---|:---|:---|:---|
| [Publisher Service](publisher-service.md) | [https://api.appnexus.com/publisher](https://api.appnexus.com/publisher) | Selling | No |
| [Placement Service](placement-service.md) | [https://api.appnexus.com/placement](https://api.appnexus.com/placement) | Selling | No |
| [Deal Service](deal-service.md) | [https://api.appnexus.com/deal](https://api.appnexus.com/deal) | Selling | No |

## Shared platform service

Below is an example of a shared platform service. For more details, see [Shared Platform Services](shared-platform-services.md).

| Service Name | Endpoint | Context | Read-only? |
|:---|:---|:---|:---|
| [Privacy Service](privacy-service.md) | [https://api.appnexus.com/privacy](https://api.appnexus.com/privacy) | Foundation | No |

## User service

Below is an example of a user service. For more details, see [User Service](user-service.md).

| Service Name | Endpoint | Context | Read-only? |
|:---|:---|:---|:---|
| [User Service](user-service.md) | [https://api.appnexus.com/user](https://api.appnexus.com/user) | Foundation | No |
