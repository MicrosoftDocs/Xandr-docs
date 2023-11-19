---
Title : Object Limits - FAQ
Description : This page provides answers to frequently asked questions about object
ms.date : 10/28/2023
limits.
---


# Object Limits - FAQ



This page provides answers to frequently asked questions about object
limits.



<b>Note:</b> You can use the <a
href="object-limit-service.md"
class="xref" target="_blank">Object Limit Service</a> to view your
limits and proactively monitor your usage.



>

## What is an Object?

Xandr considers an object to be those elements used in an auction such
as creatives and domains in a domain list. You can see the complete list
in <a
href="api-usage-constraints.md"
class="xref" target="_blank">API Usage Constraints</a>.



>

## Why is there a limit on Objects?

We store all Objects in memory on our impression bus servers. This is
done to ensure the lookup for those objects at auction time is minimized
to ensure the auction runs as fast as possible.



>

## How can I determine what my Object Limits are?

Xandr provides a read-only API service (<a
href="object-limit-service.md"
class="xref" target="_blank">Object Limit Service</a>) that can be used
to see what your limits are. Note that default limits differ depending
on whether you are a bidder (`user_type` is "bidder") or a member under
a bidder (`user_type` is "member").

Here is an example:

**View your limits and current usage for all object types**

``` pre
$ curl -b cookies -c cookies 'https://api.adnxs.com/object-limit'

{
    "response": {
        "status": "OK",
        "count": null,
        "start_element": null,
        "num_elements": null,
        "object-limits": [
            {
                "object_type": "profile",
                "limit": null,
                "mapping_limits": {
                    "inventory_source_targets": 500,
                    "content_category_targets": 300,
                    "platform_content_category_targets": 300,
                    "postal_code_targets": 4000,
                    "segment_targets": 400,
                    "publisher_targets": 300,
                    "site_targets": 100,
                    "placement_targets": 250,
                    "segment_group_targets": 400
                },
                "count_active": null,
                "count_inactive": null,
                "count_total": null
            },
            {
                "object_type": "domain_list",
                "limit": null,
                "mapping_limits": {
                    "domains": 30000
                },
                "count_active": null,
                "count_inactive": null,
                "count_total": null
            },
            {
                "object_type": "creative",
                "limit": 16000,
                "mapping_limits": [

                ],
                "count_active": 0,
                "count_inactive": 0,
                "count_total": 0
            }
        ],
        "dbg": {
         ... 
        }
    }
}
```



>

## How will I know that I am approaching my limit for an object?

We send you an email notification when you reach 85% of your limit for
an object, another when you reach 95% of your limit, and a third email
when you reach 100% of your limit.



>

## How can I receive notifications when I am approaching the limit?

You can add your email address to the `object_limit_notify_email` field
in the Bidder object. This can be done using the <a
href="bidder-service.md"
class="xref" target="_blank">Bidder Service</a>. You can add multiple
emails to this field using a comma-separated list.

You will receive an email notification when you reach 85% of your limit
for an object, another when you reach 95% of your limit, and a third
email when you reach 100% of your limit.



>

## What if I reach my limit for an object?

When you approach or reach your limit for domain lists or profile
target, you should remove inactive, unused, or unnecessary objects.

- To remove domains from a domain list, use the <a
  href="domain-list-service.md"
  class="xref" target="_blank">Domain List Service</a>, to update the
  `domains` array.
- To remove a certain target from a profile, use the <a
  href="enhanced-bidder-profiles.md"
  class="xref" target="_blank">Enhanced Bidder Profiles</a> to update
  the relevant targeting field.

When you approach or reach your limit for creatives, you should remove
<u>non-expired</u> creatives. Non-expired creatives have the
`is_expired` field set to `false`. Note that removing expired creatives
will not impact your creative count.

- To remove a creative, you make a DELETE call to the <a
  href="creative-service.md"
  class="xref" target="_blank">Creative Service</a>.

If you need help identifying objects to delete, please contact support
for assistance.



>

## How can I get my Object Limits adjusted?

In exceptional cases, a limit may be temporarily lifted by a small
amount at the discretion of our engineering team. Please contact your
Xandr representative to discuss this option or
<a href="https://help.xandr.com/" class="xref" target="_blank">open a
support case</a>.



>

## Related Topics

- <a href="faqs.md"
  class="xref" target="_blank">FAQs</a>






