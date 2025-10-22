---
title: Bidders - BSS Avro File Format
description: In this article, learn step-by-step instructions on how to prepare the audience files using the AVRO file format and onboard the data into the platform.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidders
ms.author: shsrinivasan
---

# Bidders - BSS Avro file format

## BSS AVRO file format

This document covers how to prepare your audience files using the AVRO file format and onboard the data into the platform. **AVRO is required to upload audiences containing extended ID’s and publisher-provided ID’s**, and the legacy BSS file format does not support newer user ID types.

- Segments can be created through the [segment service](../digital-platform-api/segment-service.md).
- Audience files can be uploaded to segments through the [batch segment service](../digital-platform-api/uploading-segment-data-using-bss.md).

## Best practices

- Recommended file size: 100-300mb per file
- Recommended file compression: deflate
- Recommended delivery method: [Passive Segment Upload](../digital-platform-api/passive-segment-upload-using-aws-s3.md) (reach out to your Account Manager for access).
- Updating segments: Instead of sending the full audience memberships again, you can upload only the changes for existing segments. This will reduce the data size and the chance of reaching your daily upload limits.

## Overview of steps

1. [Understanding the User-segments record](#user-segments-record)
1. [Install the AVRO tools library](#installing-the-avro-tools-library)
1. [Download the Xandr AVRO schema file](#download-the-xandr-avro-schema)
1. [Generate your AVRO audience file](#generate-your-avro-audience-file)

## User-segments record

A user record has two top level elements:

- User ID (uid)
- Array of segments

### User ID types

Only one id type can be uploaded per uid record (e.g. Xandr User ID, IFA, Device ID, eid)

| User ID Type | Description |
|---|---|
| `AppNexus/Xandr User ID (ANID)` | Xandr ID, also known as user_id_64. |
| `Device ID` | Similar utility as ifa (Identifier for Advertising). It indicates the Mobile device type being onboarded. The device_id record consists of two fields:<br> - domain (enum): Possible values are idfa, sha1udid, md5udid, openudid, aaid, windowsadid, rida, tifa, vida, and lgudid.<br> - id (string) |
| `Identifier for Advertising (or IFA)` | Identifier for Advertising - indicates the device type being onboarded. The ifa record consists of two fields:<br> - **type** (string): Type of ID.<br> - **id** (string): IFA ID, representing the IFA in UUID format.<br><br>For supported ifa types, see [device extension object](outgoing-bid-request-to-bidders.md).  |
| `External ID` | External ID - indicates Member defined identifier being onboarded. The external_id record consists of two fields:<br> - **member_id** (int): Member ID of the member who owns the external_id.<br> - **id** (string): corresponding value of the member_id. |
| `Extended ID's(eid) or Publisher-provided ID's(PPID)` | Extended ID - indicates the type of universal ID or publisher ID being onboarded. The eid record consists of two fields:<br> - **source** (string): Source of the ID.<br> - **id** (string) - Publisher or industry ID.<br><br>Today these are the only two available for audience onboarding. |

#### Java library example

##### `AppNexus/Xandr User ID (ANID)`

```

{"uid":
{"long":12345},
"segments":
[{"id":123,
"code":"",
"member_id":0,
"expiration":0,
"timestamp":0,
"value":0}]}

```

##### `Device ID`

```

{"uid":
{"device_id":
{"id":"958cba26-f338-43f3-8bb0-ed821582daae",
"domain":"idfa"}},
"segments":
[{"id":123,
"code":"",
"member_id":0,
"expiration":0,
"timestamp":0,
"value":0}]}

```

##### `Identifier for Advertising (or IFA)`

```

{"uid":
{"ifa":
{"id":"99136473264876328",
"type":"atif"}},
"segments":
[{"id":123,
"code":"",
"member_id":0,
"expiration":0,
"timestamp":0,
"value":0}]}

```

##### `External ID`

```

{"uid":
{"external_id":
{"id":"clientid1",
"member_id":958}},
"segments":
[{"id":123,
"code":"",
"member_id":0,
"expiration":0,
"timestamp":0,
"value":0}]}

```

##### `Extended ID's(eid) or Publisher-provided ID's(PPID)`

```

{"uid":
{"eid":
{"source":"liveramp.com",
"id":"123123123"}},
"segments":
[{"id":123,
"code":"",
"member_id":0,
"expiration":0,
"timestamp":0,
"value":0}]}

```

#### Python library example

##### Python library example: `AppNexus/Xandr User ID (ANID)`

```
{'uid': 64,
'segments':
[seg1]}
```

##### Python library example: `Device ID`

```

{'uid': {'id': 
'qweqeqweq', 
'domain': 'idfa'}, 
'segments': [seg1]}

```

##### Python library example: `Identifier for Advertising (or IFA)`

```

{'uid': {'id': 
'qweqeqweq', 'type': 
'atif'}, 'segments': 
[seg1]}

```

##### Python library example: `External ID`

```

{'uid': {'id': 
'extid1', 
'member_id': 914}, 
'segments': [seg1]}

```

##### Python library example: `Extended ID's(eid) or Publisher-provided ID's(PPID)`

```

{'uid': {'id': 
'qweqeqweq', 
'source': 
'liveramp.com'}, 
'segments': [seg1]}

```

### Segments object

You can upload to multiple segments within the same uid record by creating an array of segment objects.

| File | Type | Description |
|:---|:---|:---|
| `id` | int | Xandr segment ID. |
| `code` | string | Xandr segment code. |
| `member_id` | int | Member ID of the segment. Required when code is specified. |
| `expiration` | int | Segment expiration in minutes. Set to:<br> - `0` for maximum expiration (180 days).<br> - `-1` for segment removal.<br> - `-2` for default member expiration. |
| `timestamp` | long | Segment activation time in seconds from epoch. It specifies when segment becomes 'live'. Set to 0 to activate the segment immediately. |
| `value` | int | Segment value. |

## Installing the AVRO tools library

- Java library

  ```
  Curl -o http://archive.apache.org/dist/avro/avro-1.10.1/java/avro-tools-1.10.1.jar
  ```

- Python library

  ```
  python3 -m pip install avro
  ```

## Download the Xandr Avro schema

You can download the Xandr Avro Schema from [here](https://download.microsoft.com/download/4/0/0/40099106-6f9f-4b38-8aac-0dc7567404db/xandr_schema.avsc).

## Generate your AVRO audience file

For examples using the Java and Python libraries, see below.

### Java example

#### Create an audience file

```
{"uid":{"long":12345},"segments":[{"id":123,"code":"","member_id":0,"expiration":0,"timestamp":0,"value":0}]}
{"uid":{"external_id":{"id":"clientid1","member_id":958}},"segments":[{"id":123,"code":"","member_id":0,"expiration":0,"timestamp":0,"value":0}]}
{"uid":{"ifa":{"id":"99136473264876328","type":"atif"}},"segments":[{"id":123,"code":"","member_id":0,"expiration":0,"timestamp":0,"value":0}]}
{"uid":{"device_id":{"id":"958cba26-f338-43f3-8bb0-ed821582daae","domain":"idfa"}},"segments":[{"id":123,"code":"","member_id":0,"expiration":0,"timestamp":0,"value":0}]}
{"uid":{"eid":{"source":"liveramp.com","id":"123123123"}},"segments":[{"id":123,"code":"","member_id":0,"expiration":0,"timestamp":0,"value":0}]}
```

#### Convert the audience file into AVRO

Run the following command:

```
java -jar avro-tools-1.10.1.jar fromjson --codec deflate --schema-file xandr_schema.avsc sample.json > sample.avro  
```

**Where:**

- xandr_schema.avsc = the supplied Xandr Avro schema file;
- sample.json = your audience file;
- and sample.avro = output AVRO file

### Python example

> [!NOTE]
>
> - Our examples are for the **Python Avro Library**, and are not to be confused with the **Fast Avro Library**.
>   - Python Avro library does not use uid union type names. Instead, it determines the uid type by full match of field names.
>
>     `{'uid': {'id': 'qweqeqweq', 'domain': 'idfa'}, 'segments': \[…\]}`
>   - The Fast Avro library uses hints to specify the exact type of uid similar to the Java library.
>
>     `{'uid': ('external_id', {'id':'exitd1', 'member_id': 914}), 'segments': \[{'expiration': 259200, 'id': 25815407}\]}`
> - `DataFileWriter.append()` accepts a python dictionary (dict) type, not a JSON.

#### Creating an AVRO audience file

##### Sample script using the Python Avro library

```
import avro.schema
from avro.datafile import DataFileReader, DataFileWriter
from avro.io import DatumReader, DatumWriter
  
# the supplied xandr schema
schema = avro.schema.parse(open("xandr_schema.avsc", "rb").read())
  
# output avro file 
writer = DataFileWriter(open("sample.avro", "wb"), DatumWriter(), schema, codec=’deflate’)
   
# segments
seg1 = {'id': 1000, 'code': '', 'member_id': 0, 'expiration': 0, 'timestamp': 0, 'value': 0}
   
# anid
writer.append({'uid': 64, 'segments': [seg1]})
   
# external id
writer.append({'uid': {'id': 'exitd1', 'member_id': 914}, 'segments': [seg1]})
   
# idfa
writer.append({'uid': {'id': 'qweqeqweq', 'domain': 'idfa'}, 'segments': [seg1]})
   
# eid (or ppid)
writer.append({'uid': {'id': 'qweqeqweq', 'source': 'liveramp.com'}, 'segments': [seg1]})
writer.append({'uid': {'id': 'qweqeqweq', 'source': 'netid.de'}, 'segments': [seg1]})
   
writer.close()
```
