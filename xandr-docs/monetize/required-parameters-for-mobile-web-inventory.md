---
title: Required Tag Parameters for Desktop and Mobile Web Inventory
description: This page lists additional tag parameters, like width and height, for desktop and Mobile Web Inventory. 
ms.date: 10/28/2023
---


# Required tag parameters for desktop and mobile web inventory

The required parameters for tags on Mobile Web inventory are `id` and `referrer`. However, you'll need additional parameters such as width and height to monetize your inventory, unless these values have been set on the placement.

| Parameter | Type | Required? | Compatible Handlers | Description |
|--|--|--|--|--|
| `id` | string | Yes | `ptv`, `ssptv`, `vmap`, `ssvmap` | The unique ID of the placement where the ad will serve. If you'd rather not pass the raw placement ID, you can pass in a combination of `member` and `inv_code` parameters. For more information, see "Target Video Attributes via Query Parameters." |
| `referrer` | string | Required for desktop and mobile web only | `ptv`, `ssptv`, `vmap`, `ssvmap` | The URL where the ad will be rendered |
| `vcontext` | int | Required to monetize inventory | `ptv`, `ssptv` | Position of the video placement. Possible Values:<br> - 1 - Linear Pre-roll<br> - 2 - Linear Mid-roll<br> - 3 - Linear Post-roll<br> - 4 - Outstream |
| `vframeworks` | int | Required to monetize inventory | `ptv`, `ssptv`, `vmap`, `ssvmap` | Frameworks supported by the player. Possible values:<br> - 1 - VPAID 1.0<br> - 2 - VPAID 2.0<br> - 3 - MRAID-1<br> - 4 - MRAID-2<br> - 5 - ORMMA<br> - 6 - OMID-1<br>**Note**: `vframeworks` supports single as well as a list of comma-separated integer values. For example,<br>`vframeworks=1,2,3`<br>or<br>`vframeworks=1`. |
| `vheight` | int | Required to monetize inventory | `ptv`, `ssptv`, `vmap`, `ssvmap` | Player height (in pixels). While not required, this parameter is recommended in order to ensure video bidders receive both width and height on bid requests. |
| `vmaxduration` | int | No | `ptv`, `ssptv`, `vmap`, `ssvmap` | For single requests, this is the maximum video placement duration in seconds. Any creative with a duration longer than this value will be excluded from the auction. For podded inventory, this is the length of the full pod. |
| `vwidth` | int | Required to monetize inventory | `ptv`, `ssptv`, `vmap`, `ssvmap` | Player width (in pixels). While not required, this parameter is recommended in order to ensure video bidders receive both width and height on bid requests. |
