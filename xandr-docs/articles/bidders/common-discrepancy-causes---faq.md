---
Title : Common Discrepancy Causes - FAQ
Description : - Your system and the Xandr system are not counting impression and spend
the same way.
---


# Common Discrepancy Causes - FAQ



- Your system and the Xandr system are not counting impression and spend
  the same way.
- Comparable figures are not from the same timezone.
- Creatives might be large and slow to load, introducing latency. This
  could result in users dropping off the web or app before all the
  counting pixels have been called.
- Counting pixels might be embedded in a lot of pixel containers,
  causing latency. Users might to drop off the web or app.
- Your creatives might not be compatible with older browser versions.
  Ensure your creatives are compatible with older versions of browsers
  or exclude those browsers from your buying.
- Creatives could have JavaScript compatibility issues. Ensure your
  creatives are not blocking JavaScript.
- Creatives could have daisy chain, multiple Iframe compatibility
  issues. Ensure your creatives are not relying on features that are not
  expected to work in multiple Iframes.
- There could be broken code on publisher page that doesn't correctly
  display the ad or call the attached pixels.
- All the creatives are not using cache busting macro ${CACHEBUSTER}.
- All the creatives are not using \<no_script\>.
- Flash creatives or DCO creatives are not using a default or backup
  image creative.
- Creatives are not used with the correct template_id. (See <a
  href="https://docs.xandr.com/bundle/xandr-bidders/page/selecting-the-correct-template-for-your-creative.html"
  class="xref" target="_blank">Selecting the Correct Template for Your
  Creative</a>.)
- Third-party provider (DCO , swapping, viewability, security) is
  avoiding the creative display outside campaign scope based on IP or
  latitude/longitude geo location.
- Load balancing feature used on bidder side and limitation of an "in
  silo" reconciliation that prevent the servers or services from
  properly reconciling the auctions won and price paid globally.
- Counting pixel server timeout.
- Counting pixel or creative servers hosted on a server that is slow to
  load or using CNAME.

<div id="common-discrepancy__section_rx3_mkm_4wb"
>

## Information to provide when opening a discrepancy case

- Discrepancy type: Impressions / Spend / Both
- Phase 1 reports
  - Impressions count
  - Spend
  - By seller id
  - By placement id
  - By tag id
  - By domain
  - By <a href="http://creative.id/" class="xref"
    target="_blank">creative.id</a> (the creative id of the Xandr
    creative object)
  - By creative.code (if used, should be the creative id from your side)
  - By Geo
  - By hours, on last 7 days






