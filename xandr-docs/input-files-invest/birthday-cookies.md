---
Title : Birthday Cookies
Description : The first time a user without one of our cookie visits a website where
we serve ads, we set a cookie. We also add that user to the
---


# Birthday Cookies



The first time a user without one of our cookie visits a website where
we serve ads, we set a cookie. We also add that user to the
"Xandr Birthday Cookie" segment. This segment
appears in Invest DSP as "cookie_birthday
(shared)" and its segment ID is 1.

This segment is not owned by any particular member; instead, we expose
the birthday cookie segment to all members of the platform. In other
words, it is a shared segment that any member can use. This document
describes several example use cases for the birthday cookie segment; it
also provides links to further documentation on segments, targeting, and
conversion attribution.

Use Cases for Sellers

Platform members do not have access to other members' segments, except
in cases where there is a special arrangement. Even if a member does not
have access to segments shared by external data providers or other
platform members, the birthday cookie segment can serve as a useful
heuristic when a seller is deciding how to set yield management price
floors.

For example, even though you may not know what other segments a
particular user is part of, you can guesstimate that a user who has been
a member of the "cookie_birthday (shared)" segment for more than a week
is probably rich in segment data, and thus more valuable to advertisers.
Based on this information, you can configure your yield management floor
rules to reflect the higher value of impressions served to this user.
Conversely, you may drop floors for users whose "birthdays" are more
recent.

Use Cases for Buyers

Here are two buy-side use cases for the birthday cookie:

- As a buyer, it is often in your interest to target users who don't
  clear their cookies. This is especially true if you are running a
  performance ad campaign. In this case you may want to target users who
  have been members of the birthday cookie segment for more than a day,
  since that implies that they do not clear browser cookies, and thus
  conversions from these users are more likely to be attributed
  correctly.
- On the other hand, a buyer may wish to do the opposite: target users
  who have been members of the birthday cookie segment for very short
  periods of time—say, less than a day—on the chance that these users
  may be undervalued as a result of allegedly belonging to fewer
  segments.



<b>Tip:</b> For instructions on how to
implement segment targeting, see
<a href="segment-targeting.md" class="xref"
title="You can target users within segments by using Boolean expressions. Users get added to segments after they&#39;ve viewed or clicked a particular creative.">Segment
Targeting</a>.



Related Topics

- <a href="reporting-guide.md" class="xref">Reporting Guide</a>
- <a href="working-with-segments.md" class="xref">Working with
  Segments</a>
- <a href="segment-targeting.md" class="xref"
  title="You can target users within segments by using Boolean expressions. Users get added to segments after they&#39;ve viewed or clicked a particular creative.">Segment
  Targeting</a>
- <a href="conversion-attribution.md" class="xref">Conversion
  Attribution</a>




