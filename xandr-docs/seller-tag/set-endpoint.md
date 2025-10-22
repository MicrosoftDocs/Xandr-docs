---
title: Set Endpoint
description: This function sets the Impression Bus endpoint to which ad requests are made. This page also lists parameters that can be sent as an argument in the function along with an example. 
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: seller-tag
ms.author: shsrinivasan
---


# Set Endpoint

This function sets the Impression Bus endpoint to which ad requests are made.

``` 
setEndpoint('endpoint', true|false)
```

> [!IMPORTANT]
> If you plan to use the `setEndpoint` function to ensure the use of the simple domain, it's advisable to concurrently deactivate the AST `userSync` feature within the `setPageOpts`. This action will ensure that the `userSync` script remains disabled throughout the auction process, aligning with your preference to maintain cookie integrity regardless of the user's consent choices.

The parameter listed below can be sent as an argument in the function.

| Parameter | Type | Description |
|--|--|--|
| `endpoint` | string | Specifies a URL endpoint. |
| `freezeIbUrl` | Boolean | An optional setting. Default is **false**.<br>When set to **true**, AST will not attempt to switch the Impression Bus domain to normal or simple domain as per consent information present in the auction.<br>When set to **false**, AST will switch to normal or simple domain as appropriate.<br>**Note**: See [Set Up Placements with AST](set-up-placements-with-ast.md) for more details about the simple domain and when it should be used. |

## Example

``` 
apntag.setEndpoint('ib.adnxs-simple.com', true);
```

> [!NOTE]
> Users who want to test the AST tag against non-production data can use the example above to point to our testing environment.
