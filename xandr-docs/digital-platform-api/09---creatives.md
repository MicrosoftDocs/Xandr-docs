---
title: Digital Platform API - Creatives
description: In this article, learn how a creative is associated with a campaign and explore the necessary fields with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Digital Platform API - Creatives

For any campaign to serve, it must have valid creatives associated with it. All creative must be registered via the API, but doing this can be tricky. The way creatives should be uploaded is highly dependent on the format of the creative.

> [!NOTE]
> Regardless of the creative format, there are a few considerations:
>
> - In order to purchase real-time inventory, creatives must be opted into the audit process but setting `"audit_status"` to `"pending"` and setting `"allow_audit"` to `"true"`.
> - Once the audit for the creative is complete, the various audit status and feedback fields will be populated with critical information regarding the audit result. These fields are `"audit_status"`, `"audit_feedback"`, `"google_audit_status"`, `"google_audit_feedback"`,`"msft_audit_status"`, `"msft_audit_feedback"`.
> - The `"content"` and `"original_content"` fields serve slightly different purposes. The `"content"` field is what is actually served by the impression bus on an ad call and may contain escaped characters in order to be served properly. The `"original_content"` field is used by the UI for displaying and modifying the `"content"`. For this reason, the values of the `"content"` and `"original_content"` fields may be slightly different.
> - Every creative must be associated with a single advertiser. This is set via the `"advertiser_id"` parameter.
> - In order to track clicks on a given creative, you must include the click URL macro (`"${CLICK_URL}"` or `"${CLICK_URL_ENC}"`) and set the `"track_clicks"` field to `true`.

## HTML and JavaScript returned by a URL

HTML or JavaScript returned by a URL (`"format"` values of `"url-html"` and `"url-js"`, respectively) are relatively straight-forward formats to use for creatives. Generally, URLs do not contain characters that would normally conflict the JSON syntax. Registering creatives of this format is relatively straightforward. Refer to the example below for the `"url-html"` format. The `"url-js"` format is very similar, so a single example is presented.

### Example for the `"url-html"` format

Make a file containing JSON and add the correct values. Necessary fields include format, width, height, audit status, and media URL.

```
$cat creative
{
  "creative": {
    "name": "HTML returned by a URL",
    "advertiser_id": 1234,
    "format": "url-html",
    "width": 300,
    "height": 250,
    "audit_status": "pending",
    "track_clicks": true,
    "media_url": "http://ad.adserver.com/show_ad.php?ad_id=123456&width=300&height=250&click=${CLICK_URL}&random=${CACHEBUSTER}"
  }
}
```

Then to create the new creative, send a `POST` request to the API.

```
$ curl -b cookies -c cookies -X POST --data-binary @creative 'https://api.appnexus.com/creative?advertiser_id=1234'
{
  "response":{
    "status": "OK",
    "id": 123456
  }
}
```

## Hosted Flash and images

Hosted Flash and image formats (`"format"` values of `"flash"` and `"image"`, respectively) are a bit more difficult to create via the API. The image for Flash file must be base-64 encoded and included in the `"content"` field. Once uploaded to the API, we will begin transferring this creative to our CDN (content delivery network). After the creative has been fully transferred to the CDN, the creative `"content"` will be changed to null and the `"media_url"` will be changed to point to the creative's location on the CDN. The `"format"` field will stay either `"image"` or `"flash"`, depending on the original value. The example below shows how to upload an image creative. The image we use for the sample is located here: [https://dummyimage.com/300x250](https://dummyimage.com/300x250).

### How to upload an image creative?

From the terminal, you can obtain the base-64 encoding for a file with the command below.

> [!NOTE]
> If the output of base64 contains text wrapping, the line returns will need to be removed.

```
$ base64 300x250.gif
R0lGODdhLAH6AOMAAMzMzAAAAJmZmbKysjMzM39/f2ZmZkxMTBkZGQAAAAAAAAAAAAAAAAAA
AAAAAAAAACwAAAAALAH6AAAE/hDISau9OOvNu/9gKI5kaZ5oqq5s675wLM90bd94ru987//A
oHBILBqPyKRyyWw6n9CodEqtWq/YrHbL7Xq/4LB4TC6bz+i0es1uu9/wuHxOr9vv+Lx+z+/7
/4CBgoOEhYaHiImKi4yNjo+QkZKTlJWWl5iZmpucnZ6foKGio6SlpqeoqaqrrK2ur7CxsrO0
tba3uLm6u7y9vr/AwcLDxMXGx8jJysvMzc7P0NHS09TV1tfY2drb3N3e3+Dh4uPk5ebn6Onq
6+zt7u/w8fLz9PX29/j5+vv8/f7/AAMKHEiwoMGDCBMqXMgwoICHECNKnChgAAgBBg4QIHDg
gAEB/icwauToEaSaASJHdixg8gNKijAjhhC5sePHIgIC6NzJs6fPAAQ6DDjwcyeCAxZBDC2q
82jSMQIOIGDa1MDTDQaoUm2pYSlTp0JyaqUaFOvYnQU+ZD0bIG0YAVPZBkDANcNauTvrXrg7
1u0PsXh5ls1AFO+BDoXlHgbDV65fwoHzbkjMdrEPwJGBaqDMEwGBuD4NTC7qGXRP0V8ay9Vb
gfPqzaQ/F0XdY0CB27hz6yYQOkMBnwgeAyhgWidrCb97Bq9A3OfxK3wJfHxqm7fyDdZ1EtDN
PfdV5sCFN+/5nIhq2heKW7bAGUEG9ZA7p55rVYNq4RWyB1hfAj6G9ky4/oaeBcntNBgG+rV1
QYHaYdcTfljc5gFnB1pg2oAjMKiZBglCOISADvL0nQUD9FShBAmOWEGJgrnBIk8aXIhCihu8
2CASrnk4gY37dZAgiT3xh2BPK6golA/FGQmAaTp6wKOQF/x4RIIKbqBhkxNcCR5PWCL3YAo5
YcjBZ0rSwJmSX5qgJQdrEkFllwBw5uRprREpFJ0h7SRmBtYhUKYMZ2aQZgly3snTnjwM8KYH
+rnngWkVNvoBpHkeymhnf8JA4wU8luejfI+2KMQAxVXZgWlQDmlUBah+IKkJmOmE6AQJ+rlD
cRl0ekKrl64aBKk+wTkBnojZOaylExpbQqwB/sxaa6Yv8Hjijj0NYJtUUyFwVAGZEstBoT8A
S55S3polIrXIdtAYtBswu+ezPGiIaKyuBakkj7NWsC4QGjbl2QHctjsoB/tKEKuwABRcabq0
KsfuC5tewOxYdGFwsFrV8nsWUhlc7IGGLXncAcgquEsBvPGaqEG/bKkoMpvj/sDyTxVLPLCV
MQPwMs48eXpRbwCgzENx5bF8lAFISwWczVx+QLLMctlqwc4r50y1bzmD6ZNGDvvQ2LQUaEgA
a/dNfXPVPQNh7doPFWBAqRtWcDUGT+t8NtZpszAxppf59GdUHXmEtq8UzL1g1kYIQKVehhNo
9d10I641aQ9HW1y+/iJEbDDkh+etRIJCNq5vxps37YHCetNcuQvi7pQqrDeLTgHqSPDoKAX4
YnyuBLmfTnoLrbvuQ/Bxs/DkiuXa97sSgVYQ5AfgSvB8sjCyTqVOr89AvNQuTE+B998qqwTt
S4r6KeESUNprU9ZTlT0M268OgvoU0D8mqExoOOKrp5qPIv4csF8KFKWcreEgfjIA3//QtwEB
JoF85ONUuSIIJIahgICYYtb7VgCXriWQJ0KiIPIsmIToZYlzYUNcmwZnHBagTIM06BcB5DeT
5K0Qb5Jpgmlu5zz/8Ul80vOhqnbiQg+WDoQyUA3YWsAZ1qjsftXLnwIb5jmLTTFokpPb/hVJ
ILQJwPAFrtngAH0yxBZqgF4+EBaPAnCcWHGPRERjmlHuFccUdLFwBjQelTB3Rldt0Y10zOIN
6FOeDgrxZCZSEfGWmKAZcqo4SwzBHbW4xREY0nQl+Ex9clUqJTVSkZD8QWdKwjYDXK+QPzlA
RQCAknopaWKqtEgrf0JDCzTmjVYUZAjWCJTA+fKXgTNSdrZVEWsJoADXmxUsVzlLv4kyM12a
mVawJE2qICx8TWEXZq55xsxUEZGRiaSXIsPNF0DTd3iBk2qmycS5VE4s5eyYN3NogetpRYwJ
C0w8XQA3pjjyA5ekSs06ENCv+GwEm7zIPnM5z+PU6yvXLChp0A5qg6j0symqJAEy/RnPjRZl
O1CZpxk5ZUqBgjRD9gTKQmlwTLch7Ta1XNExkWYAllxwpi+lqB9s49KaBuymPbVpQ4ZK1KIa
9ahITapSl8rUpjr1qVCNqlSnStWqWvWqWM2qVrfK1a569atgDatYx0rWspr1rGhNq1rXyta2
uvWtcI2rXOdK17ra9a54zate98rXvvr1r4ANrGAHS9jCGvawiE2sYhfL2MY69rGQjaxkJ0vZ
ylr2spjNrGY3y9nOevazoA2taEdL2tKa9rRbjQAAOw==
```

Make a file containing JSON and add the correct values. Necessary fields include format, width, height, audit status, and content.

> [!NOTE]
> Line returns and extra spaces have been included in the example below to improve readability. In practice, line returns are not valid in JSON syntax.

```
$cat creative
{
  "creative": {
    "name": "Image",
    "advertiser_id": 1234,
    "format": "image",
    "width": 300,
    "height": 250,
    "audit_status": "pending",
    "track_clicks": true,
    "content": "R0lGODdhLAH6AOMAAMzMzAAAAJmZmbKysjMzM39/f2ZmZkxMTBkZGQAAAAAAAAAAAAAAAAAA
                AAAAAAAAACwAAAAALAH6AAAE/hDISau9OOvNu/9gKI5kaZ5oqq5s675wLM90bd94ru987//A
                oHBILBqPyKRyyWw6n9CodEqtWq/YrHbL7Xq/4LB4TC6bz+i0es1uu9/wuHxOr9vv+Lx+z+/7
                /4CBgoOEhYaHiImKi4yNjo+QkZKTlJWWl5iZmpucnZ6foKGio6SlpqeoqaqrrK2ur7CxsrO0
                tba3uLm6u7y9vr/AwcLDxMXGx8jJysvMzc7P0NHS09TV1tfY2drb3N3e3+Dh4uPk5ebn6Onq
                6+zt7u/w8fLz9PX29/j5+vv8/f7/AAMKHEiwoMGDCBMqXMgwoICHECNKnChgAAgBBg4QIHDg
                gAEB/icwauToEaSaASJHdixg8gNKijAjhhC5sePHIgIC6NzJs6fPAAQ6DDjwcyeCAxZBDC2q
                82jSMQIOIGDa1MDTDQaoUm2pYSlTp0JyaqUaFOvYnQU+ZD0bIG0YAVPZBkDANcNauTvrXrg7
                1u0PsXh5ls1AFO+BDoXlHgbDV65fwoHzbkjMdrEPwJGBaqDMEwGBuD4NTC7qGXRP0V8ay9Vb
                gfPqzaQ/F0XdY0CB27hz6yYQOkMBnwgeAyhgWidrCb97Bq9A3OfxK3wJfHxqm7fyDdZ1EtDN
                PfdV5sCFN+/5nIhq2heKW7bAGUEG9ZA7p55rVYNq4RWyB1hfAj6G9ky4/oaeBcntNBgG+rV1
                QYHaYdcTfljc5gFnB1pg2oAjMKiZBglCOISADvL0nQUD9FShBAmOWEGJgrnBIk8aXIhCihu8
                2CASrnk4gY37dZAgiT3xh2BPK6golA/FGQmAaTp6wKOQF/x4RIIKbqBhkxNcCR5PWCL3YAo5
                YcjBZ0rSwJmSX5qgJQdrEkFllwBw5uRprREpFJ0h7SRmBtYhUKYMZ2aQZgly3snTnjwM8KYH
                +rnngWkVNvoBpHkeymhnf8JA4wU8luejfI+2KMQAxVXZgWlQDmlUBah+IKkJmOmE6AQJ+rlD
                cRl0ekKrl64aBKk+wTkBnojZOaylExpbQqwB/sxaa6Yv8Hjijj0NYJtUUyFwVAGZEstBoT8A
                S55S3polIrXIdtAYtBswu+ezPGiIaKyuBakkj7NWsC4QGjbl2QHctjsoB/tKEKuwABRcabq0
                KsfuC5tewOxYdGFwsFrV8nsWUhlc7IGGLXncAcgquEsBvPGaqEG/bKkoMpvj/sDyTxVLPLCV
                MQPwMs48eXpRbwCgzENx5bF8lAFISwWczVx+QLLMctlqwc4r50y1bzmD6ZNGDvvQ2LQUaEgA
                a/dNfXPVPQNh7doPFWBAqRtWcDUGT+t8NtZpszAxppf59GdUHXmEtq8UzL1g1kYIQKVehhNo
                9d10I641aQ9HW1y+/iJEbDDkh+etRIJCNq5vxps37YHCetNcuQvi7pQqrDeLTgHqSPDoKAX4
                YnyuBLmfTnoLrbvuQ/Bxs/DkiuXa97sSgVYQ5AfgSvB8sjCyTqVOr89AvNQuTE+B998qqwTt
                S4r6KeESUNprU9ZTlT0M268OgvoU0D8mqExoOOKrp5qPIv4csF8KFKWcreEgfjIA3//QtwEB
                JoF85ONUuSIIJIahgICYYtb7VgCXriWQJ0KiIPIsmIToZYlzYUNcmwZnHBagTIM06BcB5DeT
                5K0Qb5Jpgmlu5zz/8Ul80vOhqnbiQg+WDoQyUA3YWsAZ1qjsftXLnwIb5jmLTTFokpPb/hVJ
                ILQJwPAFrtngAH0yxBZqgF4+EBaPAnCcWHGPRERjmlHuFccUdLFwBjQelTB3Rldt0Y10zOIN
                6FOeDgrxZCZSEfGWmKAZcqo4SwzBHbW4xREY0nQl+Ex9clUqJTVSkZD8QWdKwjYDXK+QPzlA
                RQCAknopaWKqtEgrf0JDCzTmjVYUZAjWCJTA+fKXgTNSdrZVEWsJoADXmxUsVzlLv4kyM12a
                mVawJE2qICx8TWEXZq55xsxUEZGRiaSXIsPNF0DTd3iBk2qmycS5VE4s5eyYN3NogetpRYwJ
                C0w8XQA3pjjyA5ekSs06ENCv+GwEm7zIPnM5z+PU6yvXLChp0A5qg6j0symqJAEy/RnPjRZl
                O1CZpxk5ZUqBgjRD9gTKQmlwTLch7Ta1XNExkWYAllxwpi+lqB9s49KaBuymPbVpQ4ZK1KIa
                9ahITapSl8rUpjr1qVCNqlSnStWqWvWqWM2qVrfK1a569atgDatYx0rWspr1rGhNq1rXyta2
                uvWtcI2rXOdK17ra9a54zate98rXvvr1r4ANrGAHS9jCGvawiE2sYhfL2MY69rGQjaxkJ0vZ
                ylr2spjNrGY3y9nOevazoA2taEdL2tKa9rRbjQAAOw=="
  }
}
```

Then to create the new creative, send a `POST` request to the API.

```
$ curl -b cookies -c cookies -X POST --data-binary @creative 'https://api.appnexus.com/creative?advertiser_id=1234'
{
   "response":{
      "status": "OK",
      "id": 123456
   }
}
```

## Raw HTML and JavaScript

Raw HTML and JavaScript  (`"format"` values of `"raw-html"` and `"raw-js"`, respectively) can be complicated by certain characters within the HTML or JavaScript which will conflict with the JSON syntax. All special characters, double-quotes in particular, should be `"escaped"` with a backslash ("\\"). The example below shows how to upload a simple HTML creative.

> [!NOTE]
> Any line returns must be encoded as "\r\n" since including actual line returns results in invalid JSON syntax.

### How to upload a simple HTML creative?

Make a file containing JSON and add the correct values. Necessary fields include format, width, height, audit status, and content. Because of the way that we write our raw HTML creatives, the HTML must be wrapped in a JavaScript document.write() call.

```
$cat creative
{
  "creative": {
    "name": "Raw HTML",
    "advertiser_id": 1234,
    "format": "raw-html",
    "width": 300,
    "height": 250,
    "audit_status": "pending",
    "track_clicks": true,
    "content": "document.write('<a href=\\\"http://www.advertiser.com/landingpage\\\" _target=\\\"blank\\\"><img src=\\\"http://dummyimage.com/300x250\\\" height=\\\"250\\\" and width=\\\"300\\\" /></a>');",
    "original_content": "<a href=\"http://www.advertiser.com/landingpage\" _target=\"blank\"><img src=\"http://dummyimage.com/300x250\" height=\"250\" and width=\"300\" /></a>"
  }
}
```

Then to create the new creative, send a `POST` request to the API.

```
$ curl -b cookies -c cookies -X POST --data-binary @creative 'https://api.appnexus.com/creative?advertiser_id=1234'
{
   "response":{
      "status": "OK",
      "id": 123456
   }
}
```

## HTML in an IFRAME

To create an HTML creative that is served in an IFRAME tag (`"format"` value of `"iframe-html"`), it is very similar to creating a raw HTML creative. The primary difference is that the HTML is **not** wrapped in a JavaScript document.write() call. The example below illustrates how to create an IFRAME HTML creative.

### How to create an IFRAME HTML creative?

Make a file containing JSON and add the correct values. Necessary fields include format, width, height, audit status, content, and original content.

```
$cat creative
{
  "creative": {
    "name": "Iframe HTML",
    "advertiser_id": 1234,
    "format": "iframe-html",
    "width": 300,
    "height": 250,
    "audit_status": "pending",
    "track_clicks": true,
    "content": "<a href=\"http://www.advertiser.com/landingpage\" _target=\"blank\"><img src=\"http://dummyimage.com/300x250\" height=\"250\" and width=\"300\" /></a>",
    "original_content": "<a href=\"http://www.advertiser.com/landingpage\" _target=\"blank\"><img src=\"http://dummyimage.com/300x250\" height=\"250\" and width=\"300\" /></a>"
  }
}
```

Then to create the new creative, send a `POST` request to the API.

```
$ curl -b cookies -c cookies -X POST --data-binary @creative 'https://api.appnexus.com/creative?advertiser_id=1234'
{
   "response":{
      "status": "OK",
      "id": 123456
   }
}
```

## Associate creatives with campaigns

There are two methods for associating creatives and campaigns:

1. Using the campaign service.
1. Using the creative service.

### Campaign service

To associate multiple creatives to a single campaign, `PUT` a request to the campaign service, updating the `"creatives"` field. The example below illustrates the syntax.

> [!NOTE]
> The API call has been abbreviated for readability.

```
$ cat campaign
{
  "campaign": {
    "id": 6553,
    "creatives":[
      {"id": 123456},
      {"id": 123457},
      {"id": 123458},
      {"id": 123459}
    ],
    ...
  }
}
```

### Creative service

To associate a creative to multiple campaigns, `PUT` a request to the creative service, updating `"campaigns"` field. The example below illustrates the syntax.

> [!NOTE]
> The API call has been abbreviated for readability.

```
$ cat creative
{
  "creative": {
    "id": 123456,
    "campaigns":[
      {"id": 6553},
      {"id": 6554},
      {"id": 6555},
      {"id": 6556}
    ],
    ...
  }
}
```
