---
Title : Video Player Targeting
Description : <b>Note:</b> This topic applies to Deals. For
ms.date: 10/28/2023
---


# Video Player Targeting







<b>Note:</b> This topic applies to Deals. For
non-Deals line items, see
<a href="video-targeting.md" class="xref">Video Targeting</a>.





You can target video inventory based on the playback method, player
size, position, creative duration, and framework.

In the Targeting section of a
line item or campaign, click the
Edit button next to **Video**.

You can target video creatives in any or all of the following ways:

- <a href="video-player-targeting.md#ID-00005144__p_nqr_55q_gkb"
  class="xref">Target video inventory by position</a>
- <a href="video-player-targeting.md#ID-00005144__p_tfd_w5q_gkb"
  class="xref">Target video inventory by playback method</a>
- <a href="video-player-targeting.md#ID-00005144__p_lmn_w5q_gkb"
  class="xref">Target video invemtory by player width</a>
- <a href="video-player-targeting.md#ID-00005144__target-by-framework"
  class="xref">Target video inventory by framework</a>
- <a
  href="video-player-targeting.md#ID-00005144__target-by-creative-duration"
  class="xref">Target video inventory by creative duration</a>



<b>Note:</b> You should avoid using both VAST
creatives and in-banner or interstitial video creatives within the same
video campaign. An in-banner or interstitial video creative will not
serve when you target by position. Setting any of the three video
targeting parameters (i.e., **Playback Method**, **Player Size**, or
**Position**) will restrict inventory to only those that satisfy the
specified parameters and thus significantly limit your delivery
potential.

By default, you will target all playback methods, player sizes, roll
positions, allowed creative durations, and video frameworks. However,
you can narrow your targeting.



Target Video Inventory by Position or Context

The options available to target inventory by position, also called
context:

- **Instream** - Video ads are embedded within a video player.
  - **Pre-roll** - Inventory that hosts video creatives that play before
    the user selected video of choice.
  - **Mid-roll** - Inventory that hosts video creatives that play in the
    middle of the user selected video of choice.
  - **Post-roll** - Inventory that hosts video creatives that play after
    the user selected video of choice.
  - **No roll position defined** - Target inventory where no position
    information has been provided.
- **Outstream** - Video ads are embedded within the body of a web page.

Target Video Inventory by Playback Method

You can target inventory that accepts creatives with the following
playback methods:

- **Auto-play, sound on** - Video creative starts playing with sound on
  as soon as the page loads.
- **Auto-play, sound off** - Video creative starts playing with sound
  off as soon as the page loads. Sound comes on when the user clicks on
  the creative.
- **Auto-play, sound unknown** - Video creative starts playing as soon
  as the page loads, but no sound information is specified.
- **Click-to-play** - Video creative is static on the page till the user
  clicks to play.
- **Mouse-over** - Video starts playing when the user moves the mouse
  over the creative.
- **No playback method provided** - Target inventory where no initiation
  method information is provided (e.g., YouTube inventory).



<b>Note:</b>

- For maximum delivery and reach, we recommend that you include **No
  initiation method provided** in your targeting since some inventory
  (such as Google Ad Manager) is not classified.
- Playback method targeting is not available for Google Ad Manager
  (181).



Target Video Inventory by Player Width

Player inventory is available across all supply types (web, mobile web,
and app). The following player sizes are available to target:

- **Large -** primarily large-format web and CTV inventory (minimum
  width of 640 pixels)
- **Medium -** includes most smartphone player inventory for mobile apps
  (minimum width of 320 pixels, maximum width of 639 pixels)
- **Small -** primarily in-banner inventory (maximum width of 319
  pixels)
- **No player width provided**



<b>Tip:</b> For maximum delivery and reach, we
recommend that you include **No player width provided** in your
targeting, because some inventory (such as Google Ad Manager) is not
classified.



You can either click the graphic to make a selection or check the
appropriate checkbox.

Target Video Inventory by Framework

Publishers set Video Frameworks on the placement or on the query string
of the request. You can target Video Frameworks on the deal line item
using the expected frameworks of the creatives that will serve through
this deal. That way, only impressions with the allowed Video Frameworks
will be included. For example, a deal targeting VPAID 2.0 will only
include requests that allow VPAID 2.0 creatives to serve.



You can target the following video frameworks:

- VPAID 1.0
- VPAID 2.0
- MRAID-1
- ORMMA
- MRAID-2



Target Video Inventory by Creative Duration

Publishers set Maximum Creative Duration on the placement or on the
query string of the request. You can target creative duration on the
deal line item using the expected duration of the creatives that will
serve on the deal line item. That way, only impressions with a Maximum
Creative Duration higher than the Deal Creative Duration will be
included. For example, a deal targeting a creative duration of 60
seconds will only include requests that allow ads of 60 seconds or
greater to render.

You can target video inventory by creative duration by specifying the
number of seconds duration.




