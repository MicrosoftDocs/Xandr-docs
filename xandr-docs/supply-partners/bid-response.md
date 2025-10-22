---
title: Supply Partners - Bid Response
description: Learn about bid responses, their JSON fields, supply templates, types of errors, and examples to help you understand better.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: supply-partners
ms.author: shsrinivasan
---

# Supply Partners - Bid response

> [!WARNING]
> We have disabled the Supply Integration (ASI) protocol (formerly AppNexus Supply Integration) for server-side supply integrations beginning on October 1st, 2017. We strongly encourage that you migrate your supply to the [OpenRTB protocol](https://www.iab.com/wp-content/uploads/2016/03/OpenRTB-API-Specification-Version-2-4-FINAL.pdf). Everything in this section is legacy content.

After you send a bid request, Xandr returns a bid response in JSON format. This page explains the possible JSON fields and their values. The Examples at the bottom of the page show the fields that are returned when:

- Xandr submits a bid
- Xandr does not submit a bid - No bid available
- Xandr does not submit a bid - Error
- Xandr submits a VAST video creative (NOT YET SUPPORTED)

> [!TIP]
> If a Xandr bid wins your auction, you should insert the winning bid price into the `%%pricepaid%%` macro of the `ad_tag` before placing the tag on the web page.

## JSON fields

| Field | Type | Description | Example |
|:---|:---|:---|:---|
| `external_auction_id` | string | The ID of the supply partner auction, as sent in the bid request. | `"A4s24536"` |
| `appnexus_auction_id` | int | Xandr holds its own auction to select the bid to submit for your auction. This is ID of the Xandr auction event. | `4396943919143109134` |
| `bid` | decimal | The CPM value of the Xandr bid.  | `0.206367` |
| `creative_id` | int | The ID of the creative that is served if Xandr wins your auction.  | `345634` |
| `landing_page_url` | string | The landing page URL of the creative.  | `"www.landingpage.com"` |
| `brand_id` | int | The Xandr ID for the brand of the creative. To map brand IDs to names, use the [Brand Service](../digital-platform-api/brand-service.md). | `12` |
| `buyer_member_id` | int | The ID of the member that owns the creative.  | `3453` |
| `no_bid` | boolean | If true, Xandr does not have a bid for your auction.   | `false` |
| `request_error` | boolean | If true, an error prevented Xandr from submitting a bid. | `false` |
| `request_error_id` | int | The ID of the error. This field is returned only when request_error is true. For all the possible error IDs and their meanings, see **[Errors](#errors)** section below. |`3` |
| `ad_tag` | string | The ad tag that is placed on the web page if Xandr wins your auction. <br><br> **Note:** If you wish to track clicks, Xandr can add a macro for your click URL: `&pubclick=%%pub_click_url%%`. <br><br>To learn more about this functionality, reach out to your implementation team. | See [examples](#examples) below. |

## Supply templates

For VAST video creatives, if you require custom parameters not normally included in the `ad_tag` of the bid response, you can ask Xandr to build a supply template for you. Here's how it works:

1. You communicate directly with your Xandr representative about the custom parameters you would like returned for VAST video creatives.
1. If Xandr agrees with your request, Xandr builds a supply template for you and sends you the ID.
1. In your bid requests for VAST video creatives, you include the supply template ID in the `template_id` field.
1. In bid responses, the supply template adds your custom parameters to the `<Extensions>` section of the `ad_tag`.

### Example

Let's say you want Xandr to include the following supplementary information for VAST video creatives:

- Bidding strategy (CPM, CPC, etc.)
- Currency
- Source of the bid

The supply template that Xandr would build for you would add this information to the `<Extensions>` section of the `ad_tag`:

```
"ad_tag":"<?xml version="1.0" encoding="UTF-8" standalone="no"?><VAST version="2.0" xmlns:xsi=
                "http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="vast.xsd">
                <Ad id="560469"><Wrapper><AdSystem version="1.0">adnxs</AdSystem><VASTAdTagURI><![CDA
                TA[http://ib.adnxs.com/ab?enc=AAAAAAAA8D8AAAAAAADwPwAAAAAAAPA_AAAAAAAA8D8AAAAAAADwPwkWl1e
                GIxl9XgZfiHCnHw8p021QAAAAADd8CQBVBAAAVQQAAA0AAABVjQgAMmgBAAAAAQBVU0QAVVNEAAEAAQASEwAAVgAB
                BAMCAQUAAIIAaRIvXgAAAAA.&cnd=%21chngsgiT1QUQ1ZoiGAAgstAFMAA4kqYEQARI1QhQt_glWABgLmgAcAB4A
                IABAIgBAJABAZgBAaABAagBALABALkBAAAAAA AA8D_BAQA AAAAAAPA_yQEzMzMzMzMDQNkBAAAAAAAA8D_gAQA.
                &udj=uf%28%27a%27%2C+51512%2C+1349374761%29%3Buf%28%27r%27%2C+560469%2C+1349374761%29%3B&
                ccd=%212gSgJwiT1QUQ1ZoiGLLQBSAE&vpid=171&referrer=espn.com&dlo=1&pp=%%pricepaid%%]>
                </VASTAdTagURI><Impression></Impression><Creatives><Creative AdID="560469"><Linear>
                </Linear></Creative></Creatives><Extensions><Extension type="Partner Name">
                <Price model="CPM" currency="USD" source="AppNexus">1</Price></Extension>
                </Extensions></Wrapper></>"
```

> [!NOTE]
> For the full bid response for a VAST video creative, see the **[Examples](#examples)** below.

## Errors

When an error prevents Xandr from submitting a bid, the `request_error_id` in the response helps you diagnose the problem.

| `request_error_id` | Meaning |
|:---|:---|
| 1 | The syntax of the bid request was incorrect. |
| 2 | The member ID in the request could not be parsed. |
| 3 | The request did not map to a Xandr user ID. |
| 4 | The bid request did not include `external_auction_id`. |
| 5 | The request did not map to a placement. |
| 6 | The Xandr auction failed. |
| 7 | The requested `ad_format` did not match the placement format. |
| 8 | The inventory (e.g. `page_url`) or user (e.g. ip_address) passed is blocked by Xandr.** |
| 9 | The `ad_format` parameter (required) was not passed in the request. |

> [!NOTE]
> **Error ID 8 will also trigger if the domain passed is excluded by the global targeting profile of the buying member.

## Examples

### Xandr submits a bid

```
{
    "external_auction_id": "A4s24536",
    "appnexus_auction_id": 4396943919143109000,
    "request_error": false,
    "no_bid": false,
    "bid": 0.206367,
    "creative_id": 345634,
    "landing_page_url": "http://www.landingpage.com",
    "brand_id": 12,
    "buyer_member_id": 328,
    "ad_tag": "<scriptsrc='http: //ib.adnxs.com/ab?enc=nkFD_wQXyz-iXL8FfvnHPwAAAAAAAOA_oly_BX75xz-eQUP_BBfLP0p8RFYC0OIKHKmTLdGzBl2rOWpOAAAAALGQCADLAQAAbAEAAAIAAACyGQkAmwkBAAEAAABVU0QAVVNEANgCWgC0AoMDvw4BAgUCAQQAAAAAciHhvwAAAAA.&tt_code=13394&udj=uf%28%27a%27%2C+1008%2C+1315584427%29%3Buf%28%27c%27%2C+117682%2C+1315584427%29%3Buf%28%27g%27%2C+51717%2C+1315584427%29%3Buf%28%27r%27%2C+596402%2C+1315584427%29%3Bppv%2815221%2C+%27784417993571728458%27%2C+1315584427%2C+1318176427%2C+117682%2C+67995%29%3Bppv%2815223%2C+%27784417993571728458%27%2C+1315584427%2C+1315670827%2C+117682%2C+67995%29%3Bppv%2815225%2C+%27784417993571728458%27%2C+1315584427%2C+1318176427%2C+117682%2C+67995%29%3Bppv%2815227%2C+%27784417993571728458%27%2C+1315584427%2C+1318176427%2C+117682%2C+67995%29%3Bppv%2815229%2C+%27784417993571728458%27%2C+1315584427%2C+1318176427%2C+117682%2C+67995%29%3Bppv%2815231%2C+%27784417993571728458%27%2C+1315584427%2C+1318176427%2C+117682%2C+67995%29%3B&cnd=!VyRDEwiylwcQsrMkGAAgm5MEMAA4tAVAAEjsAlAAWABgrARoAHAAeACAAQCIAQCQAQGYAQGgAQGoAQOwAQC5AUw3iUFg5cA_wQFwscHFBhfLP8kBmpmZmZmZ8T_ZAYV80LNZ9eM_4AHkKA..&ccd=!XASOJAiylwcQsrMkGJuTBCAA&referrer=http: //www.nydailynews.com&media_subtypes=1&pp=%%pricepaid%%'></script>"
}
```

### Xandr does not submit a bid - No bid available

```
{
   "external_auction_id":"A4s24536",
   "no_bid":true,
   "request_error":false
}
```

### Xandr does not submit a bid - Error

```
{
   "external_auction_id":"A4s24536",
   "no_bid":true,
   "request_error":true,
   "request_error_id":2
}
```

### Xandr submits a VAST video creative (NOT YET SUPPORTED)

When Xandr submits a VAST video creative:

- The creative is passed as escaped VAST XML in the `ad_tag` field.
- If the bid wins your auction, you must unescape the content before placing it on the page.
- If the bid wins your auction, you must insert the winning bid price (in CPM) into the `%%pricepaid%%` macro in the `ad_tag`.
- If you have asked Xandr to build a supply template that passes custom parameters in VAST creative bids, those custom parameters will appear inside the `<Extensions>` tag of the XML within the `ad_tag`. In the example below, the supply template has added supplementary information about the price of the bid. For more details about about supply templates, see **[Supply Templates](#supply-templates)** above.

> [!TIP]
> Following industry standard practice, Xandr does not log a VAST impression on win. Instead, the impression is logged only once the video starts (user clicks play, etc.).

```
{
   "external_auction_id":"A4s24536",
   "appnexus_auction_id":4396943919143109134,
   "request_error":false,
   "no_bid":false,
   "bid":2.000000,
   "creative_id":345634,
   "landing_page_url":"http://www.landingpage.com",
   "brand_id":12,
   "buyer_member_id":328,
   "ad_tag":"<?xml version="1.0" encoding="UTF-8" standalone="no"?><VAST version="2.0" xmlns:xsi=
                "http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="vast.xsd">
                <Ad id="560469"><Wrapper><AdSystem version="1.0">adnxs</AdSystem><VASTAdTagURI><![CDA
                TA[http://ib.adnxs.com/ab?enc=AAAAAAAA8D8AAAAAAADwPwAAAAAAAPA_AAAAAAAA8D8AAAAAAADwPwkWl1e
                GIxl9XgZfiHCnHw8p021QAAAAADd8CQBVBAAAVQQAAA0AAABVjQgAMmgBAAAAAQBVU0QAVVNEAAEAAQASEwAAVgAB
                BAMCAQUAAIIAaRIvXgAAAAA.&cnd=%21chngsgiT1QUQ1ZoiGAAgstAFMAA4kqYEQARI1QhQt_glWABgLmgAcAB4A
                IABAIgBAJABAZgBAaABAagBALABALkBAAAAAA AA8D_BAQA AAAAAAPA_yQEzMzMzMzMDQNkBAAAAAAAA8D_gAQA.
                &udj=uf%28%27a%27%2C+51512%2C+1349374761%29%3Buf%28%27r%27%2C+560469%2C+1349374761%29%3B&
                ccd=%212gSgJwiT1QUQ1ZoiGLLQBSAE&vpid=171&referrer=espn.com&dlo=1&pp=%%pricepaid%%]>
                </VASTAdTagURI><Impression></Impression><Creatives><Creative AdID="560469"><Linear>
                </Linear></Creative></Creatives><Extensions><Extension type="Partner Name">
                <Price model="CPM" currency="USD" source="AppNexus">1</Price></Extension>
                </Extensions></Wrapper></>"
}
```

> [!NOTE]
> The deal fields below are visible to Xandr employees only.

### Xandr submits a bid for a deal

```
{
    "external_auction_id": "A4s24536",
    "appnexus_auction_id": 4396943919143109000,
    "request_error": false,
    "no_bid": false,
    "bid": 0.206367,
    "creative_id": 345634,
    "landing_page_url": "http://www.landingpage.com",
    "brand_id": 12,
    "buyer_member_id": 328,
    "deal_code": "This is a big deal",
    "deal_id": 123456,
    "ad_tag": "<scriptsrc='http: //ib.adnxs.com/ab?enc=nkFD_wQXyz-iXL8FfvnHPwAAAAAAAOA_oly_BX75xz-eQUP_BBfLP0p8RFYC0OIKHKmTLdGzBl2rOWpOAAAAALGQCADLAQAAbAEAAAIAAACyGQkAmwkBAAEAAABVU0QAVVNEANgCWgC0AoMDvw4BAgUCAQQAAAAAciHhvwAAAAA.&tt_code=13394&udj=uf%28%27a%27%2C+1008%2C+1315584427%29%3Buf%28%27c%27%2C+117682%2C+1315584427%29%3Buf%28%27g%27%2C+51717%2C+1315584427%29%3Buf%28%27r%27%2C+596402%2C+1315584427%29%3Bppv%2815221%2C+%27784417993571728458%27%2C+1315584427%2C+1318176427%2C+117682%2C+67995%29%3Bppv%2815223%2C+%27784417993571728458%27%2C+1315584427%2C+1315670827%2C+117682%2C+67995%29%3Bppv%2815225%2C+%27784417993571728458%27%2C+1315584427%2C+1318176427%2C+117682%2C+67995%29%3Bppv%2815227%2C+%27784417993571728458%27%2C+1315584427%2C+1318176427%2C+117682%2C+67995%29%3Bppv%2815229%2C+%27784417993571728458%27%2C+1315584427%2C+1318176427%2C+117682%2C+67995%29%3Bppv%2815231%2C+%27784417993571728458%27%2C+1315584427%2C+1318176427%2C+117682%2C+67995%29%3B&cnd=!VyRDEwiylwcQsrMkGAAgm5MEMAA4tAVAAEjsAlAAWABgrARoAHAAeACAAQCIAQCQAQGYAQGgAQGoAQOwAQC5AUw3iUFg5cA_wQFwscHFBhfLP8kBmpmZmZmZ8T_ZAYV80LNZ9eM_4AHkKA..&ccd=!XASOJAiylwcQsrMkGJuTBCAA&referrer=http: //www.nydailynews.com&media_subtypes=1&pp=%%pricepaid%%'></script>"
}
```
