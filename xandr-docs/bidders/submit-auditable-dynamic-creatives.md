---
title: Submit Auditable Dynamic Creatives
description: Learn to submit your creatives using custom Macros that can reduce the number of audits performed by consolidating any creative with the same size and brand. 
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---


# Submit Auditable Dynamic Creatives

In order to maximize your reach on Xandr's platform, you need to submit all of your creatives using the Creative API service.

However, submitting all variations for auditing can be cumbersome and costly. Using custom macros, you can reduce the number of the audits performed by consolidating any creative with the same size and brand.

A creative is defined as a object within Xandr's system that defines how an ad should be rendered based on the HTML/JavaScript code (or a URL that points to the HTML/JavaScript code) along with the size of the creative and other values. **According to [Xandr creative policy](../monetize/ad-quality-and-creative-standards.md), this creative object must always render an ad that has a consistent brand, language and size.**

Please see below for a sample JSON that would be submitted to Xandr system using the Creative API service.

``` 
{
    "creative": {
        "content": "<script type="text/javascript" language="javascript">
                        if (${IS_PREVIEW}) 
                                                {
                                                var creative = http://creative.com/static.js
                                                }
                                        else
                                                {
                                                var creative = http://creative.com/${dynamic_ad_markup}
                                                }
                                        </script>
                                        <script type="text/javascript" src="http://creative.com/loadjs.js">
                                        </script>"
        "width": "320",
        "height": "50",
        "template": {
            "id": 7
        }
    }
}
```

- Please refer to this [link](selecting-the-correct-template-for-your-creative.md) to identify which template ID needs to be used.
- Please refer to the example script skeleton in the content field of the creative JSON above.

The `if` condition exists for our creative audit process, allowing your code to determine whether the creative is being audited, and displaying an auditable static version of the creative.

The `else` condition exists for live impressions where an auction is triggered and your bidder has been given a chance to respond to a Xandr bid request.

In your bid response, you will be given an opportunity to pass in the value of the custom macro `${dynamic_ad_markup}`.

Depending on the protocol you are using, your bid response will look similar to below.

``` 
Xandr protocol
 
{
    "bid_response": {
        "responses": [
            {   "creative_id": 1,
                "auction_id_64": 486730670703283200,
                "price": 1,
                "custom_macros": [
                    {
                        "name": "dynamic_ad_markup",
                        "value": "dynamic.js"
                    }
                ],
                "member_id": 1
            }
        ]
    }
}
```

``` 
OpenRTB protocol
 
{
    "id": "5461124730276536244",
    "seatbid": [
        {
            "seat": "1",
            "bid": [
                {
                    "adid": "1",
                    "price": 1,
                    "ext": {
                        "appnexus": {
                            "custom_macros": [
                                {
                                    "name": "dynamic_ad_markup",
                                    "value": "dynamic.js"
                                }
                            ]
                        }
                    }
                }
            ]
        }
    ]
}
```

In real auctions these custom macros values will replace the macro placeholders.

The resulting creative content will look similar to below.

``` 
<script type="text/javascript" language="javascript">
if (${IS_PREVIEW}) 
{
var creative = http://creative.com/static.js
}
else
{
var creative = http://creative.com/dynamic.js
}
</script>
<script type="text/javascript" src="http://creative.com/loadjs.js">
</script>
```

Since the `dynamic.js` value is completely controlled by your bidder, you can choose to pass us a different value such as "more_dynamic.js".

**Please keep in mind that even if you are using the custom macros to dynamically render creatives, all renderings for a given creative ID must have the same brand, language and size.**

## Related topics

- [Creative Service](creative-service.md)
- [Xandr Macros](xandr-macros.md)
- [Creative Macro Check Service](creative-macro-check-service.md)
- [Creative - FAQ](creative---faq.md)
