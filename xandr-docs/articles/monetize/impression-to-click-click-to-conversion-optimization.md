---
Title : Impression-to-Click, Click-To-Conversion Optimization
Description : This guide only applies to the legacy line item. If you are using the
ms.date: 10/28/2023
---


# Impression-to-Click, Click-To-Conversion Optimization



This guide only applies to the legacy line item. If you are using the
augmented line item (ALI), see
<a href="optimization-guide-ali.md" class="xref">Optimization Guide -
ALI</a>.

The optimization team is excited to announce the release of a new
enhancement to our optimization logic: impression-to-click,
click-to-conversion optimization, or "imp-to-click" for short.
Imp-to-click only affects managed and cross-net campaigns with
post-click CPA goals. This enhancement works by looking at both
click-through rate and conversion rate, as opposed to just conversion
rate. Using imp-to-click, we estimate conversion rates as follows:

``` pre
predicted conversion rate = (predicted click-through rate) * (predicted click-to-conversion rate)
```

The advantage of doing this is that we can make accurate click-through
rate predictions much sooner than we can accurate conversion rate
predictions.

This enhancement improves the speed of learn for both new publishers and
campaigns by quickly killing off campaigns with poor click-through rates
that are unlikely to perform, thus allowing publishers to allocate
impressions to campaigns with a higher chance of success and campaigns
to focus their learning on publishers where they are more likely to be
successful.

One thing to be aware of is that imp-to-click does have the potential to
initially bias too much toward campaigns with unusually high
click-through rates (relative to their overall conversion rate), but as
more accurate click-to-conversion rate data is accumulated for these
campaign, the biasing will go away.




