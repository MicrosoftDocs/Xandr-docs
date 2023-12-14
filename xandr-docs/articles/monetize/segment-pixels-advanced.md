---
Title : Segment Pixels: Advanced
Description : Secure Pixels
ms.date: 10/28/2023
The UI allows you to create secure pixels, or
pixels to be placed on HTTPS pages. To do this manually, simply create a
---


# Segment Pixels: Advanced



Secure Pixels

The UI allows you to create secure pixels, or
pixels to be placed on HTTPS pages. To do this manually, simply create a
pixel as usual and then make two small changes:

1.  Replace "http" with "https".
2.  The sub-domain should be "ib.adnxs.com".



<b>Note:</b> Secure pixels **must** be placed
on a **secure** page. In addition, insecure pixels **must** be placed on
an **insecure** page.



Segment and Conversion Pixels in the Same Call

To record a conversion and add the user to a segment in one call, use
the conversion pixel syntax with "seg" as a querystring parameter:

``` pre
https://ib.adnxs.com/px?id=[ID]&seg=[segIDs] 
```

Example:

``` pre
https://ib.adnxs.com/px?id=532&seg=17523,12345 
```

With codes. (Note that when using codes the member parameter is
required, since codes are not unique.)

``` pre
https://ib.adnxs.com/px?id=532&seg_code=auto&member=234 
```

To record a conversion and remove the user from a segment in one call,
use the conversion pixel syntax with "remove" as a querystring
parameter:

``` pre
https://ib.adnxs.com/px?id=[ID]&remove=[Seg IDs]&t=2 
```

JavaScript Pixels

Some advertisers require JavaScript tags. Image pixels can only perform
one redirect, so parent pixels with multiple piggybacks must be
JavaScript. If a piggyback pixel is JavaScript, the parent pixel should
be JavaScript as well

An image pixel looks like this, with a t=2 parameter:

``` pre
<img src="media/seg?add=11837&t=2" width="1" height="1" /> 
```

A JavaScript pixel looks like this, with a t=1 parameter:

``` pre
<script src="https://ib.adnxs.com/seg?add=11837&t=1" type="text/javascript"></script> 
```

- You can choose a JavaScript pixel format in the
  UI.
- If the parameter `t=1` or `t=2` is not present, the pixel defaults to
  image.

Parameter List

These parameters can be auto-added through the
UI, in the pixel export screen.

<table class="table">
<thead class="thead">
<tr class="header row">
<th id="ID-00005312__entry__1" class="entry">Field</th>
<th id="ID-00005312__entry__2" class="entry">Meaning</th>
<th id="ID-00005312__entry__3" class="entry">Example</th>
</tr>
</thead>
<tbody class="tbody">
<tr class="odd row">
<td class="entry" headers="ID-00005312__entry__1"><code
class="ph codeph">add</code></td>
<td class="entry" headers="ID-00005312__entry__2">Comma-separated
segments to add for the user</td>
<td class="entry" headers="ID-00005312__entry__3"><pre
class="pre codeblock"><code>add=37,28,12</code></pre></td>
</tr>
<tr class="even row">
<td class="entry" headers="ID-00005312__entry__1"><code
class="ph codeph">add_code</code></td>
<td class="entry" headers="ID-00005312__entry__2">Comma-separated list
of segment codes to add for the user.

<b>Note:</b> Member parameter is required when
using codes. Codes are case-sensitive.
</td>
<td class="entry" headers="ID-00005312__entry__3"><pre
class="pre codeblock"><code>add_code=auto,travel&amp;member=3</code></pre></td>
</tr>
<tr class="odd row">
<td class="entry" headers="ID-00005312__entry__1"><code
class="ph codeph">remove</code></td>
<td class="entry" headers="ID-00005312__entry__2">Comma-separated
segments to remove for the user</td>
<td class="entry" headers="ID-00005312__entry__3"><pre
class="pre codeblock"><code>remove=14</code></pre></td>
</tr>
<tr class="even row">
<td class="entry" headers="ID-00005312__entry__1"><code
class="ph codeph">remove_code</code></td>
<td class="entry" headers="ID-00005312__entry__2">Comma-separated list
of segment codes to remove for the user.

<b>Note:</b> Member parameter is required when
using codes. Codes are case-sensitive.
</td>
<td class="entry" headers="ID-00005312__entry__3"><pre
class="pre codeblock"><code>remove_code=auto,travel&amp;member=3</code></pre></td>
</tr>
<tr class="odd row">
<td class="entry" headers="ID-00005312__entry__1"><code
class="ph codeph">member</code></td>
<td class="entry" headers="ID-00005312__entry__2">ID of member owning
segment id/code.</td>
<td class="entry" headers="ID-00005312__entry__3"><pre
class="pre codeblock"><code>member=5</code></pre></td>
</tr>
<tr class="even row">
<td class="entry" headers="ID-00005312__entry__1"><code
class="ph codeph">redir</code></td>
<td class="entry" headers="ID-00005312__entry__2">A redirect URL used to
piggyback another pixel</td>
<td class="entry" headers="ID-00005312__entry__3"><code
class="ph codeph">redir=</code> <a
href="https://ad.yieldmanager.com/pixel?id=1243" class="xref"
target="_blank"><code
class="ph codeph">https://ad.yieldmanager.com/pixel?id=1243</code></a></td>
</tr>
<tr class="odd row">
<td class="entry" headers="ID-00005312__entry__1"><code
class="ph codeph">value</code></td>
<td class="entry" headers="ID-00005312__entry__2">A user-defined field
with a positive integer value that can be targeted in a <span
class="ph">line item or campaign.
<p>The word "value" should not be implemented as a querystring
parameter. Instead, implement this as a colon (:) after the segment ID.
An example can be found in the column to the right.</p>

<b>Note:</b> If the user is being added to
multiple segments in the call, the "value" parameter will apply to all
the segments in the call. To apply values to individual segments in a
multi-segment call, instead put a ":" after the segment ID. For example:
<pre class="pre codeblock"><code> https://ib.adnxs.com/seg?add=[seg_id_1]:[seg1value],[seg_id_2]:[seg2value],[seg_id_3]:[seg3value] </code></pre>
<p>The maximum accepted value is 2147483647. (If a value above this is
included, there may be behavior unpredictability such as the pixel fire
not processing. Therefore, the user will not be added to the segment.
Other times, it will be processed, however the value set will be much
smaller than what was passed.)</p>

<p><strong>Value Use Scenario</strong>:</p>
<p>The value field can be utilized to indicate the likelihood of a user
doing something.</p>
<p>For example, we can use values to indicate the likelihood of a user
purchasing an iPhone:</p>
<p>add=1234:1 -&gt; (low)</p>
<p>add=1234:2 -&gt; (medium)</p>
<p>add=1234:3 -&gt; (high)</p>
<p>Instead of creating three different segments, you can utilize the
value field to differentiate the level of a user's interest to buy.</p>
<p>However, you would still have to identify how the values would be
determined/categorized (for instance, if a user placed the iPhone into
their shopping cart but they didn't actually buy it, that could equate
to value 3). You would have to subjectively distinguish what separates
one value from another.</p></td>
<td class="entry" headers="ID-00005312__entry__3"><pre
class="pre codeblock"><code>add=1234:65</code></pre></td>
</tr>
<tr class="even row">
<td class="entry" headers="ID-00005312__entry__1"><code
class="ph codeph">other</code></td>
<td class="entry" headers="ID-00005312__entry__2">A user-defined,
page-level segment modifier value. This should only be used for <a
href="segment-modifier-testing-guidelines.md" class="xref">Segment
Modifier Testing Guidelines</a> integrations (see Page-Level Modifiers
on that page).</td>
<td class="entry" headers="ID-00005312__entry__3">other=2</td>
</tr>
</tbody>
</table>

Examples

**Adding Segment Pixels using Segment ID**

``` pre
<img src="media/seg?add=1,2,4" width=1 height=1/> 
```

**Segment Pixels using Segment Code**

If using codes, your member id is required.

``` pre
<img src="media/seg?add_code=auto1,travel5&member=10" width=1 height=1/> 
```

**Adding and Removing Segments in One Call**

``` pre
<img src="media/seg?add=1,2,4&remove=3" width=1 height=1/> 
```

**Redirect to Another URL/Pixel**

``` pre
<img src="media/pixel?id=1243" width=1 height=1 /> 
```

Targeting Segment Values

This is how to target values in segments: - When you create a
line item or campaign, click the
Targeting tab. - In the
Targeted Segments window, go to
the **Value** selection. See the above table for the `value` definition.




