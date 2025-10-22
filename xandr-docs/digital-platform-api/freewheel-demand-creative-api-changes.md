---
title: Freewheel change in Demand Creative API
description: Avoid updating Freewheel creatives via API from Jan 29 to Mar 5, 2024, due to suspension for implementing new logic, causing errors. Consider creating new creatives instead.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Freewheel change in demand creative API

Freewheel is temporarily suspending the creative update functionality in the Demand Creative API. This suspension is necessary due to the implementation of new creative detection logic. During this temporary suspension, users may encounter errors when updating their creatives. Once the suspension period ends, the API function is expected to behave as before, and users will no longer encounter the following errors.

> [!NOTE]
> Timeline of this suspension activity is from January 29th, 2024, to March 5th, 2024.

**Users may encounter an error during the following scenarios**

- When a user attempts to update a creative that was ingested via the API after January 29, 2024.
- In certain edge cases, the API update call might fail for creatives ingested before January 29, 2024.

## Users may encounter the following errors

> [!NOTE]
> Updates to the creatives may result in failure, accompanied by one of the following error messages with the HTTP response error code 422.

- "This demand ad cannot be updated because it is associated with multiple underlying creatives"
- "This demand ad cannot be updated because its underlying creative is associated with other demand ads"
- "This demand ad cannot be updated because it is associated with a creative that is based on our new creative uniqueness logic"

> [!TIP]
> We suggest creating new creatives instead of updating existing ones during this period.
