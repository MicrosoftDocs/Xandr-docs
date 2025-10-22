---
title: Helpful JSON Tools for APIs
description: Learn about a few tools and tricks when using the Impression Bus APIs.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Helpful JSON tools for APIs

These are tricks we use when using the APIs.

## `jq`

`jq` is a lightweight and flexible command line JSON parser. It supports colored terminal output, and filtering for JSON documents.

```
# API Call
$ curb -H 'Authorization: xxx' 'https://api.adnxs.com/segment' | jq '.response.segments[] | {id, short_name}'
 
# API Response Example
{
  "id": 1,
  "short_name": "cookie_birthday"
}
{
  "id": 123,
  "short_name": "creative_macro_test_seg"
}
{
  "id": 456,
  "short_name": "In-Market Users"
}
```

JQ can be downloaded and installed from: [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/)

## `json_reformat`

`json_reformat` formats your output nicely without reordering the fields, and is easily installed via most standard Linux Distros

```
 $ curl -b cookies -c cookies 'https://api.adnxs.com/creative' | json_reformat  
```

If it doesn't work for you, try `yum install yajl`. If you are using a mac and do not have yum, you can use macports to install `json_reformat`. Make sure you have xcode and macports downloaded and installed and then run `sudo port install yajl`. If you get an error message, follow the instructions given.

## Verify a JSON

This is a nice JSON verifier: [https://www.jsonlint.com/](https://www.jsonlint.com/).

## `JSONView`

From Firefox: Normally when encountering a JSON document (content type "application/json"), Firefox simply prompts you to download the file. With the JSONView extension, JSON documents are shown in the browser similar to how XML documents are shown. The document is formatted, highlighted, and arrays and objects can be collapsed. Even if the JSON document contains errors, JSONView will still show the raw text.

- [https://addons.mozilla.org/en-US/firefox/addon/10869/](https://addons.mozilla.org/en-US/firefox/addon/10869/)
- [https://chrome.google.com/extensions/detail/chklaanhfefbnpoihckbnefhakgolnmc](https://chrome.google.com/extensions/detail/chklaanhfefbnpoihckbnefhakgolnmc)
