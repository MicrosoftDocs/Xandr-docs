---
title: Sites and Placements
description: In this article, learn how to create a site and set up the placement by providing the necessary fields and details.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Sites and placements

Once the publisher is properly configured, we can begin building out the buy-side hierarchy. The sell-side hierarchy includes two levels under the publisher:

## Sites

In order to start the hierarchy, a site must be created. For any site, you should supply the following details:

- Publisher ID (`"publisher_id"`)
- Name (`"name"`)

### Sites: Example

Make a file containing JSON and the correct values.

```
$ cat site
{
  "site": {
    "publisher_id": 1234,
    "name": "Sports Site"
  }
}
```

Then to create the new site, send a `POST` request to the API.

```
$ curl -b cookies -c cookies -X POST --data-binary @site 'https://api.appnexus.com/site?publisher_id=1234'
{
   "response":{
      "status": "OK",
      "id": 5546
   }
}
```

## Placements

The next (and last) level of the hierarchy is to set up the placement. For any placement, you should supply the following details:

- Publisher ID (`"publisher_id"`).
- Site ID (`"site_id"`).
- Size (`"width"` and `"height"`) - **Optional (leaving these parameters out will create a `"sizeless"` tag)**.
- Ad Profile ID (`"ad_profile_id"`).
- Allow Reselling (`"exclusive"`) - **Optional (setting this to true will disable reselling)**.

### Placements: Example

Make a file containing JSON and the correct values.

```
$ cat placement
{
  "placement": {
    "publisher_id": 1234,
    "site_id": 5546,
    "name": "300x250 Placement",
    "width": 300,
    "height": 250,
    "ad_profile_id": 21345,
    "exclusive": false
  }
}
```

Then to create the new placement, send a `POST` request to the API.

```
$ curl -b cookies -c cookies -X POST --data-binary @placement 'https://api.appnexus.com/placement?publisher_id=1234&site_id=5546'
{
   "response":{
      "status": "OK",
      "id": 83843
   }
}
```
