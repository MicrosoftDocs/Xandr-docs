

# Native Video with AST



Native video gives publishers the ability to render ads on their site
from within their preferred video player. A video file is delivered to
the publisher, who then has control over how and where that ad is
played.

Working with native video is similar to working with any other type of
native creative in that the publisher is responsible for correctly
inserting the content provided by the bidder onto the site. However, in
place of the creative, a native bid response will contain a string that
has the full XML VAST for the video.



## AST Implementation

The AST implementation of native video closely mirrors the
<a href="https://iabtechlab.com/standards/openrtb-native/" class="xref"
target="_blank">standards set by the IAB</a>. 

When you define your AST tag, include the video specifications in the
native field:

``` pre
apntag.defineTag({
  native: {
    title: {required: true},
    ...
    video: {
      required: true,
      min_duration: 10000,
      max_duration: 60000
    },
    ...
  }
  ...
}
```

See <a href="define-tag.html" class="xref">Define Tag</a>for more
information on defining your AST tag.

The bid request must include the video object. Required fields in the
bid request video object are:

- min_duration: Minimum video ad duration in milliseconds.
- max_duration: Maximum video ad duration in milliseconds.

Here is an example of what you might see in the AST bid request:

``` pre
"native":{
    "renderer_id":1,
    "placement_type":"in-feed",
    "layouts":[
        {
            "video":{
            "required":true,
            "min_duration":10000,
            "max_duration":60000,
            "mime_type":[
                "video/mpt",
                "x-flv"
            ],
            "protocol":[
                "VAST_1.0",
                "VAST_2.0"
            ]
        }
    }
```

The bid response will include the VAST XML string for the video. For
example:

``` pre
{
        "version": "3.0.0",
        "tags": [
          {
            "uuid": "99999ccc-1111-4848-acac-fec7873fac6e",
            "tag_id": 123,
            ...
            "ads": [
              {
                "content_source": "rtb",
                "ad_type": "video",
                ...
                "rtb": {
                  "native": {
                    "video": {
                      "duration_ms":55000,
                      "playback_methods":["auto_play_sound_off"],
                      "frameworks":["vpaid_1_0","vpaid_2_0"],
                      "content": "<?xml version=\"1.0\" encoding=\"UTF-8\" standalone=\"yes\"?><VAST version=\"2.0\">..."
                    }
                  },
          ...
      }
```

Notice the content field in the
response. This field contains the VAST XML string for the full video
content. (The complete XML is not shown in this example. See the
<a href="https://www.iab.com/insights/vast-2-0-xml-samples-for-testing/"
class="xref" target="_blank">IAB VAST Test Examples</a> for full XML
examples of what would be returned in a response.)





## Video Players

Xandr Vast Player is a stand-alone video player
which knows how to play a single ad as delivered by VAST xml.  The
player is loaded via a Javascript script url and it supports an API
which is used to pass in the VAST xml and any other player options.  If
publishers using AST are also using the Native Assembly templates that
are provided, they are automatically opted into using
Xandr Vast Player. If they're writing their own
rendering logic from scratch, then they may choose to use another player
(like JW player). The Xandr Vast Player may be
given either a URL which returns a VAST xml document or it can be given
the VAST xml directly as a string. The player then parses the VAST xml,
selecting the most appropriate rendition from the xml to play. The
player then renders the selected rendition, using any player options
that were passed in to configure the playback.  The player is
responsible for monitoring the playback and user interaction and reports
any trackable event that was detected and for which tracking urls were
provided.



<div id="ID-00000b74__section_trv_1wx_xvb" >

## Related Topics

<a href="seller-tag.html" class="xref">Seller Tag</a>

<a href="ast-api-reference.html" class="xref">AST API Reference</a>






