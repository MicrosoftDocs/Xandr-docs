---
title: Bidders - Add a Creative
description: In this article, find information about registering a creative using the Creative Service.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Bidders - Add a creative

All creatives must be registered in the Xandr system with the [Creative Service](creative-service.md). Buyer members use the Creative Service to register creatives they would like to serve on publisher inventory, while sellers can use the Creative Service to register default creatives that are served when an ad call results in no bid or a bid lower than the specified reserve price.

Creatives that are entered into the Xandr system are manually audited for content and are continuously audited for malware through our automated Sherlock system. The creative audit applies the criteria of various inventory partners to determine where the creative can serve. For example, some supply partners allow longer animations than others.

> [!TIP]
> Please read the [Creative Standards and Auditing](creative-standards-and-auditing.md) section in its entirety before submitting creatives in the production environment to confirm that they meet the requirements of Xandr and our partners.
> [!NOTE]
> A creative must click through to a separate window for it to pass the human audit.

Until a creative passes all required human and computer audits, it can only run on inventory that accepts unaudited creatives (a small percentage of the available inventory). This process should take no more than one business day. When your creative is audited,  notification is sent through an [Audit Notify Request](audit-notify-request.md) to the address specified in the [Bidder Service](bidder-service.md). If a creative fails the audit, the auditor's feedback will be included in the Audit Notify Request. For bidders in the sand environment, test creatives will be unaudited. The seller member should set up a TinyTag to accept unaudited creatives for testing (see the next step in the Getting Started guide).

> [!TIP]
> When a creative (1) has not run and (2) has not been modified for 15 consecutive days, it is expired. This means that it is set to inactive and the `is_expired` flag on the creative is set to true. Creatives cannot win after they have expired. As of March 2018, expired creatives will be automatically reactivated if your bidder resumes bidding with the creative.

These are some of the parameters for the Creative Service:

- Media URL - The URL of the creative (e.g. `https://ad.doubleclick.net/adi/N5047.Yahoo/B2653924.18;sz=728x90;amt_paid=${PRICE_PAID};custom_val=${SAMPLE_CUSTOM_MACRO_1}`).
  - Note - this includes one standard Xandr macro - `${PRICE_PAID}` , which is automatically completed with the actual amount paid for the impression - and one custom macro `${SAMPLE_CUSTOM_MACRO_1}`.
  - To use the custom macro, you must specify the value in the [Bid Response](incoming-bid-response-from-bidders.md).
  - Please see here for the list of all the [Xandr Macros](xandr-macros.md).

- Template - The format of the creative. Please review [this page](selecting-the-correct-template-for-your-creative.md) when selecting a template.

- Width - The standard width of the tag (e.g. 728)

- Height - The standard height of the tag (e.g. 90)

- Brand - The name of the creative's advertiser brand (for creatives being used as defaults within TinyTags, you can simply put `"NO_AUDIT"`)

  ```
  $ cat creative
  {
  "creative" : {
    "media_url" : "https://ad.doubleclick.net/adi/N5047.Yahoo/B2653924.18;sz=728x90;amt_paid=${PRICE_PAID};custom_val=${SAMPLE_CUSTOM_MACRO_1}",
    "width":728,
    "height":90,
    "template":{
                  "id":1
      }
    }
  }
  ```

  Add a creative using the POST method:

  ```
  $ curl \-b cookies \-c cookies \-X POST \-d @creative "https://api.adnxs.com/creative/5"
  {
  "response":{
       "status":"OK",
       "id":7
     }
  }
  ```

  Then to verify that the added creative exists:

  ```
  $ curl \-b cookies \-c cookies  "https://api.adnxs.com/creative/5"
  {
  "response": {
    "status":"OK",
    "creatives": [{
      "id":7,
      "active":true,
      "member_id":5,
      "code":null,
      "brand_id":1,
    }

  "media_url":"https:\/\/ad.doubleclick.net\/adi\/N5047.Yahoo\/B2653924.18;sz=728x90;amt_paid=${PRICE_PAID};custom_val=${SAMPLE_CUSTOM_MACRO_1}",
      "audit_status":"pending",
      "allow_audit":true,
      "size_in_bytes":378,
      "last_checked":null,
      "not_found":0,
      "added_by_bidder":7,
      "campaign":null,
      "placement":null,
      "format":"url-html",
      "width":728,
      "height":90,
      "click_url":"",
      "pixel_url":"",
      "no_iframes":false,
      "content":null,
      "track_clicks":false,
      "is_expired" : false,
           "template":{
                  "id":1
           }
      {
      "is_prohibited" : false,
      "passed_sherlock_audit" : false,
      "last_activity":"2009-01-26 19:24:48"
    }]
   }
  }
  ```
