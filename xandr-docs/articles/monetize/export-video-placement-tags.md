---
Title : Export Video Placement Tags
Description : Note:
Xandr now supports a domain,
<a href="http://adnxs-simple.com/" class="xref"
---


# Export Video Placement Tags





Note:

Xandr now supports a domain,
<a href="http://adnxs-simple.com/" class="xref"
target="_blank">adnxs-simple.com</a>, which does not send or read
browser cookies on requests. Clients can leverage this cookie-free
domain when there is no consent to use personal data. Relevant calls
initiated by Xandr will automatically use this
domain when there is no consent or when cookies are not required for the
function. For more information, see <a
href="https://wiki.xandr.com/display/policies/Reinforcing+Privacy+Controls+Through+a+Cookie-Free+Domain"
class="xref" target="_blank">Reinforcing Privacy Controls Through a
Cookie-Free Domain</a> (login required).



This page focuses only on video placement tags. For more information and
complete workflows, see
<a href="onboarding-video-supply.html" class="xref">Onboarding Video
Supply</a>.

Step 1. Select the placements to export

Navigate to
Publisher
 \> Placement Manager,
check the boxes next to placements that you want to export, click the
More Actions button, and then select
Export Tags. This displays the
Export Placement Tags dialog.

Step 2. Modify the tag options

- Type - This field is set to
  Standard by default. However, the
  recommended setting is Secure.
- Use cachebuster - If the publisher
  uses a macro to dynamically ensure that the user's browser does not
  cache the placement URL, select this option and enter the cachebuster
  macro.
- Age - If your publisher uses a macro
  to dynamically add the age of the user to the ad call, select this
  option and enter the age macro.
- Gender - If your publisher uses a
  macro to dynamically add the gender of the user to the ad call, select
  this option and enter the gender macro. Note that we only evaluate the
  first letter of the value (m or f).
- Allowed size and
  Allow additional sizes - For video
  creatives, these settings should be left blank.

Step 3. Generate the tags

- Click the Get Tags button. The
  dialog refreshes to show the tags as well as your delivery options.
  Also, a preview displays below each tag that has default creatives.
- When you export the placement tag for a placement that allows VAST
  video creatives, the placement tag generated is a URL that
  automatically includes the `ptv` or `vmap` handler (depending on the
  placement), which ensures that ad calls will return the XML your
  publisher's video player uses to serve the desired creative. For `ptv`
  tags, the end result looks something like this:
  `https://ib.``adnxs``.com/ptv?id=5523324`. See
  <a href="create-and-customize-a-video-placement-tag.html" class="xref"
  title="Tag customization requires you to build on the root tag by identifying the correct handler for your implementation, then adding a combination of required and optional parameters.">Create
  and Customize a Video Placement Tag</a> for more detailed information.
  For vmap tags, the end result should look something like this:
  `https://ib.``adnxs``.com/vmap?id=11029144`.
  For an explanation of tag parameters you can use to further define
  your placement, see
  <a href="target-video-attributes-via-query-string-parameters.html"
  class="xref"
  title="If you use a tag solution for in-stream video, effectively targeting demand requires knowledge and careful implementation of the range of possible tag parameters.">Target
  Video Attributes via Query String Parameters</a>.
- Once you have the tag, the URL can simply be copied into the video
  player or trafficked via a publisher ad-server as part of a video
  demand waterfall. However, since the ad call will return an XML
  response and the `ptv` handler is not configured for server side
  calls, make sure the tag is fired from the video player, rather than
  placed directly on a web page or called server side.

Testing your placement tags

If your publisher isn't able to provide you with a test page, and you
are using a client-side tag, you can use an online VAST validator to
determine if the placement tag is functioning properly. There are
several available online, including the following:

- <a
  href="https://developers.google.com/interactive-media-ads/docs/vastinspector"
  class="xref"
  target="_blank">https://developers.google.com/interactive-media-ads/docs/vastinspector</a>
  (only supports https links or cut and paste of the VAST XML content
  directly)
- <a href="https://tagvalidator.videohub.tv/" class="xref"
  target="_blank">https://tagvalidator.videohub.tv/</a>
- <a href="https://demo.jwplayer.com/ad-tester/" class="xref"
  target="_blank">https://demo.jwplayer.com/ad-tester/</a>

VAST validators won't work for a server-side tag. To test a server-side
tag, you can use the following strategies:

- Change to the client-side version of the handler in order to see a
  response in the VAST validator.
- Paste the whole tag URL into a browser. If an XML response is
  returned, we're able to return an ad.

Recording impressions

VAST impressions are always recorded after serving, per the <a
href="https://www.iab.net/media/file/dig_vid_imp_meas_guidelines_final.pdf"
class="xref" target="_blank">IAB guidelines</a>. If you test VAST by
loading in a browser, you should not see any impressions recorded. It is
only when the VAST response is parsed by a video player and the
impression tag is called that the impression is recorded.




