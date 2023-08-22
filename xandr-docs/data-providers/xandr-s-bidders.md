# <span class="ph">Xandr</span>'s Bidders

<div class="body">

<div class="section">

## <span class="ph">Xandr</span>'s Bidders

Bidders receive full details of every auction on the bid request. These
details include;:

- Auction ID
- <span class="ph">Xandr</span> User ID
- Referrer URL
- IP Address
- Segment information for all owned segments
- Segment information for segments which have been shared by a data
  provider

Use of this information is entirely reliant upon targeting logic built
into the bidder's architecture.

Below is a sample bid request containing the information mentioned
above. Note the fields "auction_id_64", "user_id_64", "segments", "url"
and "ip_address":

``` pre
{
   "bid_request":{
      "members":[
         {
            "id":6
         },
         {
            "id":12
         }
      ],
      "allow_exclusive":false,
      "debug_requested":false,
      "tags":[
         {
            "id":13,
            "sizes":["728x90"],
            "position":"unknown",
            "inventory_source_id": 476,
            "auction_id_64":8984480746668973511,
            "tag_format":"iframe",
            "reserve_price":1.000,
            "ad_profile_id":382
         }
      ],
      "bid_info":{
         "user_id_64":2987961585469200312,
         "no_flash":false,
         "no_cookies":false,
         "ip_address":"96.246.152.18",
         "inventory_audits": [
             {
                 "auditor_member_id": null,
                 "intended_audience": "young_adult",
                 "inventory_attributes": [2,3,6,7],
                 "content_categories": [39]
             }
         ],
         "user_agent":"Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US;rv:1.9.0.3) Gecko/2008092414 Firefox/3.0.3",
         "accepted_languages": "en-US,en;q=0.8",
         "country":"US",
         "region":"NY",
         "city": "New York",
         "postal_code": 10014,
         "dma":501,
         "time_zone":"America/New_York",
         "url":"https://www.foodandwine.com/recipes/",
         "domain":"foodandwine.com",
         "selling_member_id":3,
         "within_iframe":false,
         "total_clicks":0,
         "segments":[
            {
               "id":103,
               "member_id":6,
               "code":"PotentialCarBuyer",
               "last_seen_min":21108407
            }
         ]
      }
   }
}
```

</div>

</div>

<div class="related-links">

<div class="familylinks">

<div class="parentlink">

**Parent topic:**
<a href="segment-usage-by-buyers.html" class="link">Segment Usage by
Buyers</a>

</div>

</div>

</div>
