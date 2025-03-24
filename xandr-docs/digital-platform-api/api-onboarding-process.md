---
title: API Onboarding Process
description: Integrate with APIs by following the instructions in the API onboarding process.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# API onboarding process

Customers who plan to integrate with Xandr APIs need to complete the following steps in our API onboarding process.

> [!NOTE]
> The Xandr API endpoints are accessible only to current customers. If you're not currently a Xandr customer but are interested in becoming one, [request a consultation](https://about.ads.microsoft.com/en-us/solutions/xandr/contact-xandr).

To know more about Xandr's API, go to [Reference](./reference.md) page.

## Get API access

The first step you must take to begin using the Xandr API is to [contact the support team](https://support.ads.microsoft.com) to gain access to the API endpoints. In order to be granted API access, you must meet the following criteria:

- Be a current Xandr UI customer with a *current* user ID and member ID. Support cannot create a new user to fulfill a request for API access.
- Be a Network, Network Observer, Advertiser, or Publisher user. We cannot grant API access to Network Advertiser Manager or Network Publisher Manager users. See [User Service](./user-service.md) for more on user types.

When you open your support ticket, use the title "Request for API Access". In the body of the support ticket, include the following information:

- The numeric ID of the *user* that requires API access.
- The billing name and numeric ID of the *member* under which that user exists.

The support team cannot grant access to clients who are not platform UI or Invest users. If you are a customer with users who would like access to the API, contact the Platform Integrations team for your business unit.

After you've been granted access, you can use the following endpoints:

- Monetize UI: `https://monetize.xandr.com`
- Invest UI: `https://invest.xandr.com`
- Digital Platform API: `https://api.appnexus.com`

## Read the documentation

The API documentation provides insight into the structure of the API and will help you determine the best approach for integration as well as provide details on typical use cases. Read through the [Reference](./reference.md) to find information and examples for the individual services that are available to you.

> [!TIP]
> **API change information**
>
> We will notify customers of API changes. You can sign up to receive emails of API changes, as well as other Xandr news. If you have a Xandr user account, you should receive relevant communications automatically.

## Related topics

- [API Semantics](./api-semantics.md)
- [API Best Practices](./api-best-practices.md)
