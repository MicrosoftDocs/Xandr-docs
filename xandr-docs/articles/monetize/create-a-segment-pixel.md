---
Title : Create a Segment Pixel
Description : A segment pixel marks a user as belonging to a certain target audience
ms.date: 10/28/2023
based on the web pages they visit, the actions they take (such as making
a purchase), or data such as gender or location.
---


# Create a Segment Pixel



A segment pixel marks a user as belonging to a certain target audience
based on the web pages they visit, the actions they take (such as making
a purchase), or data such as gender or location.

Step 1: Get started

Navigate to the Segments screen
(Advertisers
\>  Segment Pixels).



<b>Important:</b> Segment pixels can be
created at the advertiser level (that is, they're only viewable and
targetable by the specific advertiser), or the member level (available
for targeting to all advertisers). (You can move a segment from
advertiser level to member level by changing the `advertiser_id` to
`"null"` via the <a
href="xandr-api/segment-service.md"
class="xref" target="_blank">Segment Service</a>.)



Click the + New button. This opens the
Create New Segment window.

Step 2: Enter the segment pixel details

1.  In the Details section, enter
    a name that communicates the purpose of the segment pixel.
2.  Click + Advanced Options: Code if
    you wish to enter a segment code. You may wish to refer to your
    segments by "codes" so they match your internal naming system. You
    can assign a code at the time of creation or afterwards. Codes are
    case sensitive, so if the code on the segment is lower case, then
    the code in your pixel querystring must also be lower case). Codes
    can include the following characters:  
    - alphanumeric
    - underscores (\_)
    - hyphens (-)
3.  Select a **Type**: "Pixel", "Query String", or "Query String Key
    Value". Consult
    <a href="query-string-targeting-via-placement-tags-and-segments.md"
    class="xref">Query String Targeting via Placement Tags and Segments</a>
    for more information about the "Query String" and "Query String Key
    Value" parameters.
4.  In the Max Usersync Pixels field,
    enter the number of user sync pixels that are allowed on the pixel.
    - User sync pixels are pixels that Xandr
      fires on the back of the segment pixel to sync our user IDs with
      yours. This is done to improve reach and audience targeting,
      however, you may want to consider limiting them so as to not
      affect page load performance. User sync pixels make it possible
      for Xandr to recognize users even when
      they're viewing pages that don't contain
      Xandr ad tags. Why is this important?
      Buyers benefit from being able to target by segment and frequency,
      and sellers benefit by monetizing their inventory.
5.  Keep user in segment: select
    either 180 days (maximum amount of
    time allowed) or enter an amount of time in
    Minutes,
    Hours, or
    Days (maximum is 180 days) to keep
    a user in the segment.

Step 3: Add a piggyback pixel

Piggybacking allows you to chain one or more pixels to the new segment
pixel. Whenever this pixel fires, the call will be propagated to any
piggybacked pixels.



<b>Important:</b> Add piggyback pixels with
the following in mind:

1.  If you are using the feature that adds users to segments when they
    view or click on a creative ("On click, add user to the following
    segments"), piggyback pixels for these segments will NOT fire.
2.  Image pixels can only piggyback off other image pixels, and
    JavaScript pixels can only piggyback off other JavaScript pixels.
3.  Image pixels can have only one piggyback pixel. If you need to
    piggyback multiple pixels, be sure to use a JavaScript pixel.
4.  There are no character limits to piggybacked pixel URLs in
    Monetize, but browser/server URL limits may
    apply.



On the Piggyback Pixels tab, you can input the URL of an image or
JavaScript pixel to piggyback off the segment pixel.




