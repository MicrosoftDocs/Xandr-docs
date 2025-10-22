---
title: Tag Parser Service
description: Use the Tag Parser service to parse ad tags from Atlas, Mediamind, or DoubleClick files, but base64-encode the file first.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Tag Parser service

When you receive a file of ad tags from Atlas, Mediamind, or DoubleClick, or when you format a list of ad tags using the AppNexus template, you can use the Tag Parser Service to parse out the name, size, and content of each tag in the file. Note that you must base64-encode the file to parse it with this service.

> [!NOTE]
> The Xandr UI uses this service as part of the bulk creative upload feature.

## REST API

| HTTP Method | Endpoint | Description |
|:---|:---|:---|
| `POST` | `https://api.appnexus.com/tag-parser-job`<br>(tags JSON) | Parse a file of tags from `Atlas`, `Mediamind`, `DoubleClick`, or `AppNexus`. |

## JSON fields

The JSON-formatted file can contain one of more arrays of the following fields. See the [example](#examples) below for formatting.

| Field | Type | Description |
|:---|:---|:---|
| `type` | enum | The ad server that provided the file. Possible values: <br> - `"atlas"` <br> - `"mediamind"` <br> - `"doubleclick"` <br> - `"doubleclick_txt"` <br> - `"appnexus_excel"`<br><br>**Required On**: `POST` |
| `file` | string | The base64-encoded Atlas, Mediamind, or DoubleClick file.<br>**Required On**: `POST` |

The response will include the name, width, height, and content of each tag in the file.

## Examples

### Parse a file of tags from `DoubleClick`

The data in this example is for demonstration only. It does not represent an actual file of tags from `DoubleClick`.

```
$ cat tags

{
    "tag_parser_jobs": [
       {
          "type": "doubleclick",
          "file": "fAAAAAMAAAAEAAAABQAAAAYAAAAHAAAACAAAAAkAAAAKAAAACwAAAAwAAAANAAAA
           DgAAAA8AAAAQAAAAEQAAABIAAAATAAAAFAAAABUAAAAWAAAAFwAAABgAAAAZAAAAGgAAABs
           AAAAcAAAAHQAAAB4AAAAfAAAAIAAAACEAAAAiAAAAIwAAACQAAAAlAAAAJgAAACcAAAAoAA
           AAKQAAACoAAAArAAAALAAAAC0AAAAuAAAALwAAADAAAAAxAAAAMgAAADMAAAA0AAAANQAAA
           DYAAAA3AAAAOAAAADkAAAA6AAAAOwAAADwAAAA9AAAAPgAAAD8AAABAAAAAQQAAAEIAAABD
           AAAARAAAAEUAAABGAAAARwAAAEgAAABJAAAASgAAAEsAAABMAAAATQAAAE4AAABPAAAAUAA
           AAFEAAABSAAAAUwAAAFQAAABVAAAAVgAAAFcAAABYAAAAWQAAAFoAAABbAAAAXAAAAF0AAA
           BeAAAAXwAAAGAAAABhAAAAYgAAAGMAAABkAAAAZQAAAGYAAABnAAAAaAAAA..."
       }
    ]
}

$ curl -b cookies -c cookies -X POST -d @tags 'https://api.appnexus.com/tag-parser-job'

{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 1110,
        "start_element": null,
        "num_elements": null,
        "tag_parser_job": {
            "id": 1110,
            "status": "finished",
            "tags": [
                {
                    "name": "Tag 1",
                    "width": 728,
                    "height": 90,
                    "content": "<IFRAME SRC=\"https://example.adserver.net/N5956.124505.4370930011621/
                     B3941858.2;sz=120x600;ord=[timestamp]?\" WIDTH=120 HEIGHT=600 MARGINWIDTH=0
                     MARGINHEIGHT=0 HSPACE=0 VSPACE=0 FRAMEBORDER=0 SCROLLING=no BORDERCOLOR='#000000'>
                     <SCRIPT language='JavaScript1.1' SRC=\"https://example.adserver.net/adj/N5956.124505.
                     4370930011621/B3941858.2;abr=!ie;sz=120x600;ord=[timestamp]?\">  </SCRIPT>
                     ..."
                },
                {
                    "name": "Tag 2",
                    "width": 160,
                    "height": 600,
                    "content": "<IFRAME SRC=\"https://example.adserver.net/N5956.124505.4370930011621/
                     B3941858.2;sz=120x600;ord=[timestamp]?\" WIDTH=120 HEIGHT=600 MARGINWIDTH=0
                     MARGINHEIGHT=0 HSPACE=0 VSPACE=0 FRAMEBORDER=0 SCROLLING=no BORDERCOLOR='#000000'>
                     <SCRIPT language='JavaScript1.1' SRC=\"https://example.adserver.net/adj/N5956.124505.
                     4370930011621/B3941858.2;abr=!ie;sz=120x600;ord=[timestamp]?\">  </SCRIPT>
                     ..."
                },
                {
                    "name": "Tag 3",
                    "width": 300,
                    "height": 250,
                    "content": "<IFRAME SRC=\"https://example.adserver.net/N5956.124505.4370930011621/
                     B3941858.2;sz=120x600;ord=[timestamp]?\" WIDTH=120 HEIGHT=600 MARGINWIDTH=0
                     MARGINHEIGHT=0 HSPACE=0 VSPACE=0 FRAMEBORDER=0 SCROLLING=no BORDERCOLOR='#000000'>
                     <SCRIPT language='JavaScript1.1' SRC=\"https://example.adserver.net/adj/N5956.124505.
                     4370930011621/B3941858.2;abr=!ie;sz=120x600;ord=[timestamp]?\">  </SCRIPT>
                     ..."
                }
            ]
        }
    }
}
```
