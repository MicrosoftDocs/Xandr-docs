---
title: Set Endpoint
description: This function sets the Impression Bus endpoint to which ad requests are made. This page also lists parameters that can be sent as an argument in the function along with an example. 
ms.custom: seller-tag
ms.date: 10/28/2023
---


# Set Endpoint

This function sets the Impression Bus endpoint to which ad requests are made.

``` 
setEndpoint('endpoint', true|false)
```

> [!IMPORTANT]
> If you are looking to use the `setEndpoint` function to force the usage of the simple domain, it's recommended to also disable the AST `userSync` feature in the `setPageOpts`.  This will prevent AST from dropping the `userSync` script at the end of the auction, which will align to your likely desired usage of the simple domain (i.e., to not drop cookies regardless of the user's consent choices).

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
