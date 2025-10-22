---
title: Creative Upload Service - File Format
description: In this article, learn about the Creative Upload service, their authorization, and file format with thorough examples.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Creative Upload service - File format

The Creative Upload service provides the ability to upload a file and get a **media asset object** in return.

> [!NOTE]
> Media assets that are not associated to a creative can be cleaned up at any time.

## Format overview

The creative upload service is a multi-part form post. There are a few parameters required to construct the post.

The following table describes the ordering of the forms that compose the post:

| [Authorization](#authorization) | [Form Type](#form-type) | [Form File Upload](#form-file-upload) | [AppNexus API](#appnexus-api) |

## Authorization

| Name | Type | Description | Example |
|:---|:---|:---|:---|
| `Authorization` | string | The token received when authenticated to AppNexus API. | `"hbapi:108172:05866d06f6964:nym2"` |

For more information, see [API Authentication](04---api-authentication.md).

### Form type

Use the first form to define the **type** of file you are looking to upload.

| Name | Type | Description | Example |
|:---|:---|:---|:---|
| `form` | string | Define the type of file you are looking to upload. | `--form "type=video"` |

### Accepted file types

| Type | Value |
|:---|:---|
| `html` | "zip". |
| `video` | "webm","mkv","flv","vob","ogv","ogg","avi","mov","qt","wmv","rm","asf","mp4","m4p","m4v","mpg","mp2","mpeg","mpe","mpv","m2v","m4v",<br>"3gp","3g2","f4v","f4p","f4a","f4b", "swf". |
| `audio` | "aac","webm","mkv","flv","vob","ogv","ogg","avi","mov","qt","wmv","rm","asf","mp3","mp4","m4p","m4v","mpg","mp2","mpeg","mpe","mpv",<br>"m2v","m4v","3gp","3g2","f4v","f4p","f4a","f4b", "swf", "wav". |
| `image` | "jpeg", "jpg", "gif", "png", "swf". |
| `default` |  |

> [!NOTE]
> .mov videos will play in all browsers after the video finishes transcoding, however, there may be a delay in previewing.

### Form file upload

Use the next form to define the **path** to the file you want to upload.

| Name | Type | Description | Example |
|:---|:---|:---|:---|
| `form` | string | Define the path to the file you want to upload. | `--form "file=@/Folder1/Folder2/Downloads/IMG_0332.JPG"` |

### AppNexus API

Define the **URL** to the AppNexus API and point to the `creative-upload` end point. Member ID is required.

| Name | Type | Description | Example |
|:---|:---|:---|:---|
| `URL` | string | Define HTTP protocol and the `creative-upload` endpoint. | `"https://api.appnexus.com/creative-upload?member_id=123"` |

## Example

The following example illustrates a scenario derived from a real use case.

A client is uploading an image file to member 123.

| Field | Value |
|:---|:---|
| `Authorization` | `hbapi:139072:5761726637ada:nym2` |
| `Form Type` | `image` |
| `Form File Upload` | `Folder1/Folder2/IMG_0332.JPG` |
| `AppNexus API` | `https://api.appnexus.com/creative-upload?member_id=12` |

### A client is uploading an image file to member 123

```
curl -X POST -H "Authorization: hbapi:139072:5761726637ada:nym2" --form "type=image" --form "file=@/Folder1/Folder2/IMG_0332.JPG" "https://api.appnexus.com/creative-upload?member_id=123"
```

```
"response":{  
      "status":"OK",
      "count":0,
      "start_element":0,
      "num_elements":0,
      "dbg_info":{  
         "instance":"05.media-asset-pipeline.prod.nym2",
         "db":"",
         "warnings":[  

         ],
         "start_microtime":1492716035.805,
         "time":5,
         "version":"",
         "output_term":"media-asset"
      },
      "media-asset":[  
         {  
            "id":1536691,
            "parent_media_asset_id":null,
            "member_id":123,
            "advertiser_id":null,
            "publisher_id":null,
            "file_name":"IMG_0332.JPG",
            "size_in_bytes":79400,
            "cdn_uploaded_on":null,
            "cdn_url":"http://vcdn.adnxs.com/p/creative-image/1b/ee/3d/95/1bee3d95-7042-4e10-b0bf-7f43e2e4322a.JPG",
            "cdn_secure_url":"https://vcdn.adnxs.com/p/creative-image/1b/ee/3d/95/1bee3d95-7042-4e10-b0bf-7f43e2e4322a.JPG",
            "created_on":"2017-04-20 19:20:35",
            "last_modified":"2017-04-20 19:20:35",
            "deleted":false,
            "media_asset_status":[  
               {  
                  "id":1536687,
                  "media_asset_id":1536691,
                  "error_message":null,
                  "local_path":"1b/ee/3d/95/1bee3d95-7042-4e10-b0bf-7f43e2e4322a.JPG",
                  "cdn_upload_attempt_count":0,
                  "created_on":"2017-04-20 19:20:35",
                  "last_modified":"2017-04-20 19:20:35",
                  "deleted":false,
                  "status":"on_shared_storage"
               }
            ],
            "media_asset_image":{  
               "id":1005450,
               "media_asset_id":1536691,
               "height":480,
               "width":640,
               "created_on":"2017-04-20 19:20:35",
               "last_activity":"2017-04-20 19:20:35",
               "deleted":false
            },
            "media_asset_video":null,
            "media_asset_html5":null,
            "asset_type":"image",
            "mime_type":"image/jpeg"
         }
      ]
   }
   }
```

## Related topics

- [Creative Service](creative-service.md)
- [Creative VAST Service](creative-vast-service.md)
- [Creative HTML Service](creative-html-service.md)
