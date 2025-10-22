---
title: FAQ - Supply Partner Integration Process
description: This article addresses the frequently asked questions on the process of integrating supply partners.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: supply-partners
ms.author: shsrinivasan
---

# FAQ - Supply partner integration process

## OpenRTB

### There are "2.4" and "Mobile 2.2" specs mentioned in the wiki. What is the difference? We (the SSP) are a mobile company. Which oRTB version should we use?

Xandr supports the OpenRTB 2.4 specification for receiving all media type impressions. For certain legacy mobile integrations, Xandr is still backwards-compatible with the OpenRTB 2.2 spec. For any new types of integrations, follow the [OpenRTB 2.4 specification](./openrtb-specs.md).

### What is the most current version of VPAID and MRAID you support?

Xandr video currently supports VPAID versions 1 and 2 and VAST 1, 2, and 3. We currently support MRAID version 2.0. for mobile. We are backwards-compatible with OpenRTB versions 2.2 and 2.3.

## Datacenters

### Where are your datacenters located?

Xandr currently runs five datacenters: LAX1 in Los Angeles, NYM2 in North Bergen, NJ, AMS3 in Amsterdam, the Netherlands, FRA1 in Frankfurt, Germany, and SIN3 in Singapore.

### How can I test latency to the different datacenters?

To test latency to the east coast data center (New York Metro), you can ping [jump.nym1.adnxs.net](https://jump.nym1.adnxs.net/). The West coast data center can be pinged with [jump.lax1.adnxs.net](https://jump.lax1.adnxs.net/) and the European data center is available at [jump.ams1.adnxs.net](https://jump.ams1.adnxs.net/).

### Your prerequisite checklist mentions global auction timeout limits and latency measurement to our (the SSPs) IPs. Can you please specify what type of testing will be performed for this activity?

Xandr has the ability to set variable maximal auction time for each SSP. For that purpose, we measure the top latency between SSP DCs and Xandr DCs across all regions. The result is used to set up the maximal auction time on Xandr before a bid response is considered as timed out towards the SSP. Let's say the maximal auction time on your platform is 100ms. We calculate 100ms - (top latency between DCs, e.g. 18ms) - 10ms buffer = 72 ms. The result is the defined maximal auction time on Xandr towards your SSP and slower bid responses are dropped before reaching your platform.

### We (the SSP) noticed that latency is very high and it seems that the tmax parameter is not respected at all. Are you guys using tmax? If so, does it need to be enabled or anything like that on your end?

The `tmax` value cannot be set dynamically on the bid request on the Xandr platform. It has to be set by Xandr's support for your member seat and for each of your datacenters individually. The `tmax` field is also highlighted in the [OpenRTB specs](./openrtb-specs.md) as being handled differently on the Xandr platform [here](./incoming-bid-request-from-ssps.md).

## Member IDs

### Is it possible to have our `MEMBER_ALIAS` and `MEMBER_ID`?

Yes. As it is a prerequisite for our standard process, request your `MEMBER_ALIAS` and `MEMBER_ID` from your Xandr contact.

### Where can we (the SSP) find our seat ID to provide to clients that want to bid on our platform? Is that something the is publicly available to everyone or is that something we can provide on a case-by-case basis to our advertisers?

The seat ID is also known as the member ID and gets assigned to each partner on Xandr's platform once the commercial contract is finalized. The seat/member ID remains the same throughout the lifetime of the partner object and can be referenced by other partners to adjust for example their Ad Quality settings, to target their campaigns specifically to the member ID, or to allowlist/blocklist certain seller/buyer members.

### `wseat` is supported, but how can I use it? What are possible values and where to find the mapping?

`wseat` field in the OpenRTB bid request contains an array of buyer seat IDs placed in allowlists (e.g., advertisers, agencies) that are allowed to bid on this impression. In the Xandr naming convention, seat IDs and member IDs are the same. Therefore, the `wseat` array has to be populated with valid member IDs that can be retrieved via the [Platform Member Service](../digital-platform-api/platform-member-service.md).

```
"wseat": [
    "958",
    "1417"
]
```

## Publisher IDs

### How should we (the SSP) define Inventory Relationships for publisher objects?

In order to create new publisher objects under the SSP member seat or modify the existing publisher setup, the API or UI requires you to
submit [Inventory Relationship](./inventory-relationship-faq.md) information. In many cases, the relationship is "*Single publisher sourced directly from publisher*". In that case, for instance, the required fields to be populated via the [Publisher Service](../digital-platform-api/publisher-service.md) are:

```
{
    "publisher": {
        "name": "Standard Publisher",
        "state": "active",
        "code": "4321",
        "reselling_exposure": "public",
        "expose_domains": true,
        "final_auction_type": "First Price",
        "inventory_relationship": "indirect_single_publisher",
        "inventory_source": "other",
        "inventory_source_name": "Publisher name for indirect_single_publisher",
        "contact": {
            "name": "The name of the point of contact for this publisher.",
            "phone": "contact phone number",
            "email": "CSPFeedback@appnexus.com"
        },
        "billing_dba": "Publisher name as in inventory_source_name",
        "billing_address1": "The street information of the billing address.",
        "billing_address2": "The street information of the billing address cont.",
        "billing_city": "The city of the billing address.",
        "billing_state": "The state of the billing address.",
        "billing_zip": "10010",
        "billing_country": "The country of the billing address."
    }
}
```

### So if we (the SSP) set reselling exposure to private, then we will not allow other members to resell our supply, right? However, we will still be able to participate in open auction and sell our inventory via deal IDs?

No. Inventory can be made targetable at the network and publisher levels. It can only be made buyable at the placement group level. Therefore, in order to allow buyers to target and purchase your inventory, you must take the following actions:

- Expose inventory for targeting by buyers: This is also known as "reselling exposure", and can be done for the entire network or per-publisher. This makes it targetable. For instructions on how to toggle this setting, see [Publisher Service](../digital-platform-api/publisher-service.md).

- Enable placement groups (and all of their placements) for resale: In order to be resold to other members, a placement group must be enabled for resale by setting it to participate in the RTB Marketplace. This makes it buyable. For instructions on how to toggle this setting, see [Site Service](../digital-platform-api/site-service.md).

### Can you please advise us (the SSP) on Publisher Name? Would you recommend we use the name, or an ID that represents the publisher in our internal system?

Xandr strongly suggests using the Publisher names that are clearly identifiable with the Publisher (`name` field described in [Use the API to Synchronize Your Inventory Structure](./use-the-api-to-synchronize-your-inventory-structure.md). Do not use your (the SSP's) internal IDs that are only known to your internal platform for Publisher naming. See an example inventory mapping structure below:

:::image type="content" source="../supply-partners/media/b.png" alt-text="Screenshot that shows an example inventory mapping structure.":::

### Is `publisher.is_oo` in the API important?

As described in the [Publisher Service](../digital-platform-api/publisher-service.md), documentation, if this parameter is set to `true`, the publisher is owned and operated by the network. This means the network gets 100% of the revenue. However, if both `is_oo` and `inventory_relationship` are specified, `inventory_relationship` will overwrite `is_oo` with the appropriate value based on the relationship.

### How should we implement `Ads.txt` / `App-Ads.txt` as part of our SSP integration?

Review the documentation on [Support for Ads.txt and App-Ads.txt](../industry-reference/xandr-support-for-ads-txt-and-app-ads-txt.md) and reach out to your publishers with the instructions in the "Publishers" section (or simply direct them to that page) along with your member ID so they can add you to their `ads.txt/app-ads.txt` file.

## Deal IDs

### Do we (the SSP) have to pre-register Deal IDs (PMP) on the Xandr platform prior sending them in the OpenRTB protocol?

In order to be able to sell Deal IDs on the Xandr platform, you have to pre-register them using the [Deal Service](../digital-platform-api/deal-service.md).

```
{
    "deal": {
        "active": true,
        "code": "5612",
        "name": "Standard Deal",
        "start_date": "2017-04-10 00:00:00",
        "type": {
            "id": 1
        },
        "buyer": {
            "id": 882
        }
    }
}
```

### Our (the SSP) `deal.id` will be `deal.code` in the Xandr system. Can you clarify how the SSP's `deal.id` will be referenced in the bid request? Or would it only contain the Xandr deal ID?

Deal IDs are referenced per `deal.code` similar to the way how inventory objects are mapped on Xandr. The SSP's `deal.id` is set to `deal code` on Xandr's platform via the [Deal Service](../digital-platform-api/deal-service.md) when the deal is created. The `pmp.deals` array on the OpenRTB bid request has to include the external SSP `deal.id`. Xandr reads the external `deal.id` from the bid request and maps it to the internal Deal ID object via the mapping provided in the `deal.code` field. See OpenRTB bid request example below (*referencing the deal object in the previous question*):

```
[...] "pmp":{"deals":[{"id":"5612" [...]
```

### Is it true that we will be required to pass the buyer member ID for each deal created between us (the SSP) and Xandr? What is the process here? Each agency who wants to buy publisher’s inventory via Deal ID needs to provide unique member seat ID?

Deals are created on the basis of a 1-to-1 relationship between the seller and the buyer. The deal seller member needs to know the buyer member ID in order to be able to create a deal in Xandr's platform.

## Endpoints

### Should I (the SSP) keep using the `&test=1` in the endpoint for production OpenRTB bid requests?

No. Do not use *`&test=1`* for production OpenRTB bid requests, with *`&test=1`* reporting data will NOT be generated.

### Is Xandr providing test endpoints to test the OpenRTB functionality before we (the SSP) potentially have signed the contract?

No. Xandr does not provide separate test or sandbox environments for standard OpenRTB integrations. Use the *`test=1`* on the production endpoint to indicate test traffic.

### Does my Xandr endpoint domain change when I upgrade to OpenRTB?

No. The only part that changes is the actual endpoint from `/CUSTOM_ENDPOINT` to `/openrtb2`. The correct new endpoints for the OpenRTB2 protocol are therefore:

```
https://MEMBER_ALIAS-useast.adnxs.com/openrtb2?member_id=MEMBER_ID
https://MEMBER_ALIAS-uswest.adnxs.com/openrtb2?member_id=MEMBER_ID
https://MEMBER_ALIAS-emea.adnxs.com/openrtb2?member_id=MEMBER_ID
https://MEMBER_ALIAS-apac.adnxs.com/openrtb2?member_id=MEMBER_ID
```

> [!NOTE]
> `MEMBER_ID` and `MEMBER_ALIAS` should be replaced with your individual partner member ID and alias, provided by your Xandr contact.

### Is it possible to call the win notice url from the ad markup for testing or auditing purposes without triggering Inventory Quality flags and mark the impression as test impression?

Absolutely. Use the following information in the header of the call to indicate that the `/ab` or `/openrtb_win` call is for testing purposes only:

```
curl -v --header 'X-is-test: 1' --header 'Host: ib.adnxs.com' 'https://nym1-ib.adnxs.com/ab?e=wqT_3QKoCfA8qAQAAAMA1gAFAQjQis3HBRCUvPSr_...&referrer=appnexus.com&pp=1'
```

> [!NOTE]
> Do not use IP addresses that don't resolve in domain lookup for this test configuration.

## User IDs

### Bid request contains invalid `"buyeruid"`. Do we need to fix this? If so, can you please provide documentation?

Yes. The `buyeruid` field contains the Xandr User ID that you are sending to us to indicate the user that you previously matched via the [usersync pixel](./user-id-mapping.md). The bid request object has to contain a valid user ID in the `buyeruid` field, in order to be considered as bid request with matched user data. Read more about the bid request user object in [Incoming Bid Request from SSPs](./incoming-bid-request-from-ssps.md).

### The standard user syncing with Xandr requires hosting of the user match table, correct? Would Xandr initiate the user sync? If so, what volume could we anticipate here?

Xandr standard OpenRTB SSP integrations require the SSP to store the user mapping in their own system. Typically, a 1x1 image pixel on the SSP pages calls the Xandr getUID service and returns Xandr UUIDs for storage. Format of the pixel can be found in [User ID Mapping](./user-id-mapping.md). The server that receives usersync calls from Xandr needs to be able to handle 1K-3K QPS.

### We (the SSP) are wondering if Xandr supports two-way user syncing?

Xandr does not support bi-directional usersync that involves storing SSP usersync mapping tables on the Xandr side. However, Xandr-initiated usersyncing is fully supported. It allows Xandr to drop SSPs usersync pixel across the entire universe of Xandr user IDs. The setup of the Xandr-initiated usersync pixel is part of the integration process.

### What is the best way to test and confirm user syncing is working as expected?

The easiest way to verify whether the `buyeruid` (Xandr User ID) is mapped correctly is to use the debug auction. By appending `&debug=1` to the bid request call, you should receive `status: success` output as below:

```
[COOKIESHEET] cookie source: provided uid
[COOKIESHEET]   mobile optout action: none
[COOKIESHEET]   get request:
[COOKIESHEET]       uid source: provided uid
[COOKIESHEET]       uid: 5160786676315026726
[COOKIESHEET]       status: success
[COOKIESHEET]   map request: none
[COOKIESHEET]   mobile request: none
```

### Does Xandr require `buyeruid` field to be populated with Xandr user IDs for In-App mobile inventory?

The `buyeruid` is not mandatory for In-App OpenRTB bid requests, however, it's best practice to always provide the `buyeruid` in order to ensure highest user match rates. Xandr tries to match mobile IDs first, and in case of no match, tries to match the `buyeruid`. If both values are provided, successfully matched mobile IDs take precedence over `buyeruid`.

### What are the interval parameters for the usersync pixel fires?

By default, Xandr defines for SSP usersync pixel fires the internal parameters `max_interval=432000` (5 days) and `min_interval=43200` (12 hours). Max Interval: maximum number of seconds that we will wait between syncs for that pixel. E.g. if we haven't fired pixel in 5 days, then include it in the algorithm to select usersync pixels to fire. Min Interval: the number of seconds we'll wait between retries of a sync pixel if we're not able to confirm that the sync happened properly (maybe we dropped the pixel but it didn't fire properly or the user navigated away quickly). E.g. if we just fired the pixel, don't try to sync it again for at least 12 hours.

### How long does Xandr store user data?

Currently the approximate Time To Live (TTL) for user data (Xandr user IDs) is 60 days.

### What is the difference between the `/getuid` and `/getuidnb` service?

In case the user does NOT have the Xandr ID stored in the Xandr cookie space and does NOT have sticky cookies:

- `/getuid` forwards with `UID=0`

- `/getuidnb` does NOT forward with `UID=0` (the SSP will not receive `0`
  values from non-sticky cookie environments)

## Bid requests

### OpenRTB bid requests have the `imp.tagid` field. Does Xandr expect that field to hold the corresponding `placement.id` accessible from the Placement Service? Or is it expected to be the `placement.cod`e value (also managed through the API Placement Service)?

`imp.tagid` would be the `placement.code` value in the [Placement Service](../digital-platform-api/placement-service.md). This should be the same value as the one you’ll be passing in `site.id` or `app.id` on the bid request.

### What is the inventory lookup sequence for the OpenRTB bid request object IDs?

Xandr matches the IDs provided in the OpenRTB bid requests using the following lookup sequence:

```
1. imp.tagid - used to lookup by placement code
2. bidrequest.app.id - used to lookup by placement code
3. bidrequest.site.id - used to lookup by placement code
4. use bidrequest.site.publisher.id or bidrequest.app.publisher.id to lookup publisher by code and try to get default publisher placement
```

### The bid request includes several mediatype objects. Which ones, if not all, will be sent to the buy side and ultimately transacted?

OpenRTB does support multi-format requests. However, bid responses are not clearly defined for multiple media types. As result, we support multi-format bid requests with hardcoded prioritization across media types. So for example, if a request comes in as native and video, it's transformed into just a video request when sent to the buy side. The order is:

1. `video`
1. `audio`
1. `banner`
1. `native`

### What happens to the bid request impression if a publisher is not mapped out in the inventory hierarchy of the member seat?

In that case the publisher source of impression appears incorrect and could result in being filtered. Xandr does not alter impression's properties in any way. However, supply sold in the Xandr open exchange is analyzed and vetted to ensure that inventory represents the most
direct, transparent, and efficient path to purchase for our buyers. Impressions that do not meet these requirements may be ineligible for RTB selling. Those impressions may be still sold via deals. If you're experiencing issues with delivery in the open marketplace, you may
consider setting up a deal with a specific buyer to monetize your inventory.

### Does Xandr respond to multiple impression in bid requests? Or do you only respond to one impression object per bid request?

We support multiple impression objects in one bid request as per [OpenRTB spec](./openrtb-specs.md). Each impression object runs its own auction and gets individual bids from buyers.

### What are Xandr's recommendations for typical native asset definitions on the native bid request?

In order to facilitate adoption and to maximize your seller reach across native buyers, recommendations are made for both minimum sizes and aspect ratios below:

| Field | Xandr's Guidelines |
|:---|:---|
| `Title` | 25-character maximum |
| `Body` | 300-character maximum |
| `Icon/Logo*` | 1:1 aspect ratio <br>**Note**: OpenRTB spec is merging the prior overlapping type 1 and type 2 as just type 1 - to be used for app icon, brand logo, or similar |
| `Image` | 1.91:1 aspect ratio (600 px min / 150 KB max) |
| `Sponsored By` | 40 character maximum (brand of advertisement) |

### The image asset in the native bid request is using type 1 for app icon, brand logo, or similar. Does Xandr support specific icon sizes, for example 50x50?

No. Xandr creative IDs currently do not carry information about the icon/logo size of the native creative submitted by the buyer. All native bid requests including img type 1 have to be declared as size `0x0`.

### In the native part of the request (`"native-request-native"` field) - I see that you are expecting a JSON-encoded string. Can you also accept a regular object?

The native field within the native.request node has to be a string. Since the Native 1.0 spec is technically a specification on its own and can be theoretically used outside of the OpenRTB2.3 spec, the native field contents cannot be part of the JSON structure and therefore, have to be 'escaped' in order to appear as a string.

### About the `tagid` inside the request impression, do we (the SSP) have to map all our placements on Xandr? Or could we just let this field remain empty, or replace the value with the `site.id`?

Yes, no and no! You must map all your inventory to Xandr placements. Do not leave the `tagid` field on the bid request empty, both fields, `tagid` and `site.id` map to the same `placement.code` field on the Xandr placement object.

### The default markup delivery method on Xandr is the `bid.adm` attribute on the bid response, which we (the SSP) currently don't support. Do you support the alternative ad markup delivery via the `bid.nurl` attribute?

Yes, we support ad markup served on the win notice. According to the OpenRTB spec, there are multiple standard methods for transferring markup from the bidder (Xandr) to the exchange (the SSP). The default ad markup delivery method on Xandr is via the `bid.adm` attribute. The alternative markup delivery method via win notice `bid.nurl` attribute will be chosen if the SSP provides the `BidRequestExtension` attribute on the [incoming bid request](./incoming-bid-request-from-ssps.md).

> [!NOTE]
> The alternative markup delivery method currently does not work for native media type.

```
"ext": { "appnexus": { "markup_delivery": 1 } }
```

### When Xandr is reading the referrer domains or URLs from the OpenRTB bid requests, is Xandr looking at the `domain` field or the `page` field?

We are looking at both fields to determine the referrer url or domain. The `page` field is preferred over the `domain` field [incoming bid request from SSPs](./incoming-bid-request-from-ssps.md).

### How does the Xandr response adhere to our publishers block list such as blocked domains, categories, or attributes? In other words, how do we make sure creatives serving through the OpenRTB integration does not violate our publisher block lists?

For that purpose, IAB introduced the bid request fields `wseat`, `bcat`, `badv` and `bapp` in the OpenRTB protocol. In addition to that, Xandr's platform allows a less dynamic form of Publisher block settings via the [Ad Profile Service](../digital-platform-api/ad-profile-service.md).

### Does the support of multiple imp objects on the bid request require a configuration on your end?

Xandr supports by default multiple `imp` objects on the bid requests. Each `imp` object is treated like a separate impression on the Xandr platform. The fact that multiple impressions are sent to Xandr included in the same bid request has no other implications than saving network resources and connection overhead.

## Xandr

### How does Xandr handle `0` and null edge cases when it comes to native asset values, e.g. `wmin/hmin`?

For example: if the native img asset fields `wmin/hmin` are set to `0` or `null` in the bid request, then Xandr treats them logically as if those fields were omitted on the bid request. The implication of that is that external bidders will see the same bid request sent to them without those fields, i.e. with those fields removed for efficiency purposes.

### What does the `private_auction` in the pmp of the bid requests actually mean and what are the implications of setting it to `1`, i.e. only bids for specified deals are accepted?

If we receive a private auction impression from an OpenRTB seller, we only submit bids that will be accepted in the third-party auction. The implication of the `pmp.private_auction=1` is: Xandr will **NOT** send the bid request to any other potential buying bidders that are not specified by the deals on that impression.

### Does Xandr send the `imp.bidfloor` field from the SSP OpenRTB bid request to external bidders?

Yes. Xandr receives and evaluates the impression-level floor price and passes the `imp.bidfloor` to external bidder buyers.

### We (the SSP) are seeing a portion of our bid requests returning an HTTP 400 malformed response. Why?

This is the current behavior for inactive placement, placement group or publisher and invalid banner sizes. HTTP 400 is returned if no valid impressions are found in the request.

## Bid responses

### What are the expected HTTP responses to bid requests?

Expected HTTP responses to bid requests are listed below:

- **200 OK**: a valid bid response has been returned.
- **204 NO CONTENT**: no bid has been returned.
- **400 MALFORMED**: the [incoming bid request](./incoming-bid-request-from-ssps.md) contains a `site.id`, `app.id`, `app.publisher.id`, or `site.publisher.id` that maps to an inactive publisher or placement object in the Xandr system. See [General Delivery Troubleshooting Step 2](./external-seller-troubleshooting.md) for more information.

### We (the SSP) require a `bid.adomain` parameter in all bids responses. Will all bid responses from Xandr contain a `bid.adomain` field populated? Is it possible to get the advertiser’s domain, even if it’s not in the openrtb `bid.adomain` field - but in some other field?

Xandr follows the OpenRTB spec very closely and does not define the domain field as required. However, all creatives have a brand associated with them, including the unknown brand (ID 1) - which is automatically assigned to new un-audited creatives. The unknown brand links to the adomain [appnexus.com](https://appnexus.com/). Thus, we expect all bid responses to include the adomain, except the ones that contain creatives that are associated with brands which do not have adomain associated with them (\<0.08% of all creatives) - due to internal policies or other reasons.

### What are NEX10-101 categories on the OpenRTB bid response?

Ignore those categories. They are redundant with our IAB categories and are going to be deprecated in the next couple of months!

### Can the `adm` field in the bid response be a regular object?

No. `adm` contains the ad markup that will be served to page or app. It cannot be a JSON structure.

### We (the SSP) have seen that the width and height in the response is 1x1. Do you return the exact width and height of the video ad size?

For non-banner media types: The width and height on the bid response does not represent the real size of the creative (or the ad markup), to be delivered to the publisher's page. For example: Video media-type creatives use multiple media files for delivery, and similar flexibility is offered for native image assets sizes. For those creatives, the exact width and height is transported on a deeper level of the creative object, which can be previewed using the following syntax:

```
Video: https://{DATACENTER}-ib.adnxs.com/cr?id={APN_CREATIVE_ID}&format=vast 
Native: https://{DATACENTER}-ib.adnxs.com/cr?id={APN_CREATIVE_ID}&format=json
```

### Do you want us (the SSP) to do something with the *iurl*? Is it relevant for video bid responses ? Does this URL have some expiry policy ? I've tried to login to one of the examples and it seems that the URL is invalid?

The *iurl* represents the creative preview on our platform, and is a static url (see syntax above), i.e. does not expire. You may use it for pre-auditing purposes, creative caching, etc. The `id` parameter represents the Xandr creative ID and is unique on our platform. For video creative preview, attach the 'vast' format parameter to the *iurl* to view the xml, e.g. `https://fra1-ib.adnxs.com/cr?id=48265354&format=vast`

### Is the auction price in the ad markup US dollars? I assume it is CPM, correct?

Xandr follows the OpenRTB spec here. The price uses the same currency and units as the bid, in most cases USD and CPM.

### How can we (the SSP) confirm during testing whether the bid request returns a no-bid or is syntactically incorrect?

Feel free to use the `debug=1` parameter as shown below on the manual call to run a general debug auction. <br><br>**Tip**: if absolutely no debug output is returned, then most likely something is wrong with the structure of the bid request or the placement is not working.

```
https://MEMBER_ALIAS-useast.adnxs.com/openrtb2?member_id=MEMBER_ID&debug=1
https://MEMBER_ALIAS-uswest.adnxs.com/openrtb2?member_id=MEMBER_ID&debug=1
https://MEMBER_ALIAS-emea.adnxs.com/openrtb2?member_id=MEMBER_ID&debug=1
https://MEMBER_ALIAS-apac.adnxs.com/openrtb2?member_id=MEMBER_ID&debug=1
```

### How should we pass the final price in the winning notification? We (the SSP) see that there is a macro `pp=$(AUCTION_PRICE)`. What encoding/format is needed?

If the `auction type` field on the bid request is defined as `at=2` (second-price auction) then the `${AUCTION_PRICE}` macro needs to be populated by the SSP in order to receive the second price. The settlement price should be using the same currency, units and format/encoding as the bid (typically USD currency and CPM).

> [!NOTE]
> Do NOT use any currency characters like `$` in the price populated into the `AUCTION_PRICE` macro. In general, do not use any other characters than the doubl number format specifies. If the CPM clearing price is for example `0.47` dollars, replace the `AUCTION_PRICE` as follows:

#### Correct `AUCTION_PRICE` macro replacement

```
pp=0.47
```

### Should we (the SSP) use encryption when we pass you the winning price? Can you confirm which encryption algorithms are supported?

We do not support encoding for the `AUCTION_PRICE` macro in standard integrations just yet.

### How should the rendering of the Xandr imptracker and clicktracker be implemented on the publisher's page? Can we implement our (SSP) imptracker to fire on the impression win event and Xandr imptracker on impression is visible event? Would that lead to discrepancies for clicks?

Yes, any differences in the implementation of the imptracker between your SSP and Xandr's firing event will lead to discrepant behavior. Clicks will also be impacted since they depend on the timing of the imptracker.

### We (the SSP) are now up and running with OpenRTB native. Do you have a field matching table so we can communicate to the buyers which OpenRTB fields correspond to which creative fields in Xandr?

Native buyers, platform buyers, and external DSPs have to pre-register native creatives according to the [Creative Service](../digital-platform-api/creative-service.md). (See the examples for more information.)

### Does the order of the bids in the bid response JSON follow a certain pattern, for example descending order based on bid price?

No, we don't guarantee any order in the bid response JSON array structure. We recommend you evaluate bids and apply your bid selection logic strictly after you parse the full JSON response.

### What are the timeout limits for the impression win notify calls?

The timeout limits for win notify calls vary for different media types, following timeouts apply for `/ab, /it` and `/openrtb_win` calls:

- `banner: 5 minutes`
- `native: 60 minutes`
- `video: 360 minutes`

### What are the timeout limits for click tracking?

For click tracking URL calls the aggregation look-back window after the impression is transacted on Xandr's platform is:

- `banner: 120 minutes`
- `native: 120 minutes`
- `video: 120 minutes`

> [!NOTE]
> Xandr click reporting will not count any click url calls made outside of the designated aggregation look-back window after the impression has been transacted on the platform. This is particularly important for click discrepancies where the SSP counts more clicks than Xandr reporting.

## Reporting

### What are the available reports and metrics on Xandr's platform, and how can we (the SSP) retrieve those reports?

The most common report type run by SSPs is the Network Analytics Report. This report provides information on what is generally serving, what's doing well, on both buy and sell side. All reports are obtained via the [Reporting API services](../digital-platform-api/reporting-services.md). Refer to the complete list of available [Report types](../digital-platform-api/report-service.md).

Here is an example of the API call sequence necessary to obtain a Network Analytics report for the last 7 days:

```
echo "AUTH to AppNexus API: "
curl -bc -cc -X POST -s -d '{"auth":{"username":"YOUR_USERNAME","password":"YOUR_PASSWORD"}}' "https://api.appnexus.com/auth"
{
    "response": {
        "status": "OK"
    }
}
 
echo "POST to report API service: "
curl -bc -cc -X POST -s -d '{ "report": { "report_type":"network_analytics", "columns":[ "hour", "seller_member_name", "buyer_member_name", "publisher_name", "publisher_id", "publisher_code", "imps", "clicks", "total_convs", "revenue", "ctr", "convs_rate" ], "report_interval":"last_7_days", "format":"csv" } }' "https://api.appnexus.com/report?member_id=MEMBER_ID"
{
    "response": {
        "report_id": "287efed55c091dc97e2c839580962cba",
        "status": "OK"
    }
}
 
echo "DOWNLOAD from report-download API service: "
curl -bc -cc -s "https://api.appnexus.com/report-download?id=287efed55c091dc97e2c839580962cba" 
hour,seller_member_name,buyer_member_name,publisher_name,publisher_id,publisher_code,imps,clicks,total_convs,revenue,ctr,convs_rate
2017-06-02 05:00,Member Inc.,Test Buyer,Example Publisher,777999,222333,0,0,0,0.000000,0.000000000000000000,0.000000000000000000
2017-05-31 13:00,Member Inc.,Test Buyer - Netherlands,Publisher Name AG,555777,100200,172,0,0,0.000000,0.000000000000000000,0.000000000000000000
```
