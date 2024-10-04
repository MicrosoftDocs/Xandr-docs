---
title: Microsoft Invest - Test Client-Side Impression Tracking
description: Learn the detailed steps and best practices to ensure accurate and reliable client-side impression tracking in your campaigns.
ms.date: 10/28/2023
---

# Microsoft Invest - Test client-side impression tracking

Microsoft Advertising only allows impressions to be counted client-side for requests generated through the **/ssmob** call.

## Implementation approach

Microsoft Advertising appends an impression tracking pixel to the ad response.

### Implementation options

| Default |Separate Field (optional) |
|:---|:---|
| Impression pixel appended to the end of the creative content in response. | Impression pixel sent in a separate field of the JSON response. |

#### View the default response when client-side impression tracking is enabled

The response shown below is the default returned by Microsoft Advertising.

> [!NOTE]
> With client side impression tracking enabled, the "content" field now has an impression tracking pixel appended.

The pixel starts at `</script><img src=\"https://nym1.mobile.adnxs.com/it?`

```
{ "status": "ok", "ads": \[ { "type": "banner", "width": 320, "height": 50, "content": "type=\"text/javascript\">document.write('<a href=\https://nym1.mobile.adnxs.com/it?e=wqT_3QKEBPBC-wEAAAIA1gAFCIqU_aMFEKzoiML42uKdChjZt5O-vs35olQgASotCXsUrkfheoQ_EXsUrkfheoQ_GQAAAAAAAPA_IRESACkRCbAwiejUATjkFEDkFEgCUOqQ5whYwI4cYBJotfIBcAB45eMDgAEBigEDVVNEkgEBBvBAmAHAAqABMqgBAbABALgBBcABA8gBAtABANgBAOABAPABAIoCOnVmKCdhJywgMzcyMDg5LCAxNDE3NjI4MTcwKTsBHCxyJywgMTg0NjY5MjI2HgDwipICnQEhOFNQRTdnaVZ4dHNDRU9xUTV3Z1lBQ0RBamh3d0FEZ0FRQVJJNUJSUWllalVBVmdBWUpFQ2FBQndBSGdBZ0FFQWlBRUFrQUVCbUFFQm9BRUJxQUVEc0FFQXVRRjdGSzVINFhxRVA4RUJleFN1Ui1GNmhEX0pBYkd6X0R3dDFQMF8yUUVBQUEBAyREd1AtQUJBUFVCAQ40QUEuLpoCHSFZQWJLUEE2oACwd0k0Y0lBUS7CAhZodHRwOi8vd3d3LmRzbnJtZy5jb20v2AIA4AL08hnqAhxoCSFAYXBwcy5tb2JpbGUuYWRueHMBKHiAAwCIAwGQAwCYAxagAwGqAwCwAwC4AwDAA5AcyAMA&dlo=1&referrer=https%3A%2F%2Fapps.mobile.adnxs.com\%22){width="\"1\"" height="\"1\""}" } \] } 
```

#### View the separate field response when client-side impression tracking is enabled

An example of a response with client side impression tracking enabled and leveraging the Separate Field implementation option.

> [!NOTE]
> There is a field in this response named "imptracker" where the impression tracking pixel will be returned.

```
{ "status": "ok", "ads": \[ { "type": "banner", "width": 320, "height": 50, "content": "<script type=\"text/javascript\">document.write('<a href=\"https://nym1.mobile.adnxs.com/click?exSuR-F6hD97FK5H4XqEPwAAAAAAAPA_exSuR-F6hD97FK5H4XqEPyw0QojXijsK2dvE52vmRVQKSn9UAAAAAAk0NQBkCgAAZAoAAAIAAABqyBkBQAcHABIAAQBVU0QAVVNEAEABMgA1eQAA5fEBBQMCAQIAAJIAZCGhmgAAAAA./cnd=%21YAbKPAiVxtsCEOqQ5wgYwI4cIAQ./referrer=https%3A%2F%2Fapps.mobile.adnxs.com/clickenc=https%3A%2F%2Fwww.appnexus.com%2F\" target=\"_blank\"><img width=\"320\" height=\"50\" style=\"border-style: none\" src=\"https://cdn.adnxs.com/p/bf/7c/a2/50/bf7ca2500111608c8eeead50b3738d2a.jpg\"/></a>');document.write('<scr' + 'ipt src=\"https://cdn.adnxs.com/ANX_async_usersync.js\"></scr'+'ipt>');</script>",", "imptracker": "https://nym1.mobile.adnxs.com/it?e=wqT\_3QLlAajcAAAAAgDWAAUIsr79owUQjNaPqOv\_1Y9xGPKMvdDzgfK3eyABKi0JAAAABQIAEQUGDAAAABkBBRAAAPA\_IQkJCAAAKREJ8JAwjYzuATjkFEDlAUgCUIGipAFY2YEhYBVotfIBcAB4AIABAZIBA1VTRJgBwAKgATKoAQGwAQC4AQXAAQHIAQDQAQDYAQDgAQDwAQDYAgDgAvTyGeoCHGh0dHA6Ly9hcHBzLm1vYmlsZS5hZG54cy5jb22AAwCIAwGQAwCYAxagAwGqAwCwAwC4AwDAA5AcyAMA&dlo=1&referrer=https%3A%2F%2Fapps.mobile.adnxs.com" } \] } 
```

## Steps to follow

Ask your publishers if they are **parsing** the ad response. If the answer is **no**, there is no further action required.

If the answer is **yes,** then you must append the parameter **&tmpl_id=21** to the **/ssmob** tag. This will leverage the **Separate Field** implementation option.

Additionally, if the publisher is parsing, it is critical that you **test** the **Separate Field** option prior to the breaking change. By testing, you can ensure that your publisher does not experience any issues in recording transacted impressions.

## Parsing and its importance

Parsing is an action taken by the publisher's server that divides out the response provided by Microsoft Advertising into different pieces prior to delivering the content.

For example, a publisher may separate out the creative image and landing page from the Microsoft Advertising "content" field prior to delivering. This is a common tactic for publishers that have feature phone inventory or do not support JavaScript.

It has been found that most publishers that parse can **not** support a response where the pixel is appended to the end of the "content" field (Default Implementation). This occurs because the publisher parses the "content" and drops the impression tracking pixel. This results in impression volumes dropping to zero within Microsoft Advertising.

## Test instructions

In order to test the client-side impression tracking functionality, you simply need to append the parameter **&cs=1** to the **/ssmob** tag.

Example Tag to Test with **Separate Field** Option:

```
https://mobile.adnxs.com/ssmob?id=12345&size=320x50&cs=1&tmpl_id=21&format=json 
```

## Verify testing without parsing a publisher

You can definitely test even if a publisher doesn't parse, and it is highly encouraged to ensure that publishers do not face any issues at scale prior to the full launch of the client side impression tracking functionality.

Example Tag to Test with **Default** Option:

```
https://mobile.adnxs.com/ssmob?id=12345&size=320x50&cs=1 
```

## Define success metrics for the test

You and your publisher will count the same number of impressions delivered.

If your publisher records **zero** impressions despite sending Microsoft Advertising ad requests during a test, reach out to your Microsoft Advertising representative.
