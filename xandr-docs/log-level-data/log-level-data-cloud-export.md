---
title: Log Level Data - Cloud Export
description: In this article, find information about Cloud Export, Cloud Export setup, manifest files, and troubleshooting.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: log-level-data
ms.author: shsrinivasan
---

# Log level data - Cloud export

> [!IMPORTANT]
>
> - Do not manually create any manifest- or feed-related paths. Doing so will cause your export to fail to verify due to object-level ACLs. The necessary paths will be automatically created by Xandr.
> - Xandr provides bulk exports of Log Level Data (LLD) using client-specific keys (as set up using the procedures on this page). Data is exported via SSL file transfers to the client's cloud storage location (see below for options). The security of those client buckets/containers is the sole responsibility of the client.

Cloud Export is a feature used to automatically transfer Log-Level Data (LLD) to cloud storage. Xandr supports data transfer to Amazon S3 buckets, Google Cloud Storage buckets, and Microsoft Azure Blob Storage containers. Data begins transferring as soon as batch data becomes available. This setup provides faster enablement and a simpler workflow for Xandr clients (e.g., no need to poll the siphon service as with the Log-Level Data service).

## Cloud export setup

### Prerequisites

Please confirm the following prior to proceeding to setup.

1. The LLD feeds you plan to consume should already be enabled for your Xandr seat (member ID). If that is not the case, contact your Account Representative to subscribe to Log-level data.
1. Only the *protobuf*, *protobuf-delimited*, and *avro* formats are supported by Xandr Cloud Export at this time.
1. You must have *Network Admin* privileges to perform the steps below.

## Setup

Please follow the procedures in the sections below for the cloud vendor you'd like to export to. Xandr currently supports the following through the Xandr UI:

- [Amazon S3](log-level-data-cloud-export.md#amazon-s3)
- [Microsoft Azure Blob Storage](log-level-data-cloud-export.md#microsoft-azure-blob-storage)
- [Google Cloud Storage](log-level-data-cloud-export.md#google-cloud-storage)

> [!NOTE]
> If you use a firewall or other IP-restricting security features, add all of these IP addresses and ranges to your allowlist:
>
> IP addresses: **68.67.155.230**, **68.67.155.231**, **68.67.135.70**, **68.67.135.71**
>
> IP ranges corresponding to addresses/subnet masks: **185.83.140.64/28**, **68.67.146.64/28, 43.250.0.160/28**, **68.67.156.64/28**

### Amazon S3

1. Create an [Amazon S3 bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-bucket.html) which will serve as a drop box for log-level data from the Xandr Cloud Export system.

1. Select **Log-Level Data** from the **Network** (or **Reporting**) menu in the Microsoft Invest or Microsoft Monetize UI.

1. Click **Manage** in the **Cloud Export** column of the feed for which you want to create an S3 export. The **Amazon S3** section will be displayed.

1. Click **New** to set up a new export or **Configure** to edit an existing export. The **Cloud Export to: Amazon S3** page will be displayed.

1. **Setup**. Enter the information in the table below and click **Save**:

    | Setting | Description |
    |---|---|
    | **Bucket** | Name of the [Amazon S3 bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/creating-bucket.html) created in step 1. |
    | **Manifest path** | Root for manifest files (e.g., */manifests*). This file path does not support macros. |
    | **Feed Path** | Feed path with macros (e.g., */feeds/%FEED_NAME%/%YEAR%/%MONTH%/%DAY%/%HOUR%/%TIMESTAMP%*) |
    | **Notification Email** | Comma-separated list of emails. If Cloud Export can no longer access your bucket, your export will be deactivated and you will be notified by email. |
    | **Format** | Data format for log-level data files (e.g., *protobuf* ) |
    | **Server-side Encryption** | The server-side encryption applied to uploaded LLD files: <br> - None - do not apply server-side encryption <br> - [SSE-S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingServerSideEncryption.html) - apply server-side encryption with Amazon S3-managed encryption keys <br> - [SSE-KMS](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingKMSEncryption.html) - apply server-side encryption with AWS KMS-managed encryption keys. You must grant the Xandr AWS user [access to your key](https://aws.amazon.com/blogs/security/share-custom-encryption-keys-more-securely-between-accounts-by-using-aws-key-management-service/). <br> Selecting SSE-S3 or SSE-KMS will override any [default bucket encryption settings](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-encryption.html) for the uploaded files. |

> [!WARNING]
> Do not manually create any manifest- or feed-related paths. Doing so will cause your export to fail to verify due to object-level ACLs.
> The necessary paths will be automatically created by Xandr.

1. **Authorization**. For each Xandr member seat, Xandr creates a unique AWS user to upload data to S3 buckets. Xandr generates a suggested [bucket policy](https://docs.aws.amazon.com/AmazonS3/latest/userguide/example-bucket-policies.html) to [apply](https://docs.aws.amazon.com/AmazonS3/latest/userguide/add-bucket-policy.html) to your bucket that allows our AWS user access to your bucket. This policy can be used as-is, but if you already have a policy applied to your bucket, you will have to merge our policy statements with yours.

1. **Verification**. Once you apply a policy to your bucket, you must verify your permissions before your S3 Cloud Export can be activated. Click **Verify** (on the **Cloud Export to: Amazon S3** page) to run a series of tests that mimic actions that occur during an actual export. Once your export is verified, it is active. Data from the feed will automatically be exported to your S3 bucket (starting in the next hour).

### Microsoft Azure Blob Storage

1. Create an [Azure storage account](/azure/storage/common/storage-account-create) which will host one or more storage containers.

1. Create an [Azure Blob storage container](/azure/storage/blobs/storage-blobs-introduction) inside your storage account which will serve as a drop box for log-level data from the Xandr Cloud Export system.

1. Select **Log-Level Data** from the **Network** (or **Reporting**) menu in the Xandr UI.

1. Click **Manage** in the **Cloud Export** column of the feed for which you want to create an Azure Blob storage export. The **Microsoft Azure Blob Storage** section will be displayed.

1. Click **New** to set up a new export or **Configure** to edit an existing export. The **Cloud Export to: Microsoft Azure Blob Storage** page will be displayed.

1. **Setup**. Enter the information in the table below and click **Save**:

    | Setting | Description |
    |---|---|
    | **Storage Account** | Name of the [Azure storage account](/azure/storage/common/storage-account-create) created in step 1. |
    | **Container** | Name of the [Azure Blob storage container](/azure/storage/blobs/storage-blobs-introduction) created in step 2. |
    | **Manifest Path** | Root for manifest files (e.g., */manifests*). This file path does not support macros. |
    | **Feed Path** | Feed path with macros (e.g., */feeds/%FEED_NAME%/%YEAR%/%MONTH%/%DAY%/%HOUR%/%TIMESTAMP%*) |
    | **Notification Email** | Comma-separated list of emails. If Cloud Export can no longer access your container, your export will be deactivated and you will be notified by email. |
    | **Format** | Data format for log-level data files (e.g., *protobuf*) |

1. **Authorization**. Generate a [shared access signature (SAS)](/azure/storage/common/storage-sas-overview) for the storage account with the following permissions:

    - Allowed services - **Blob**
    - Allowed resource types - **Container**, **Object**
    - Allowed Permissions - **Read**, **Write**, **Delete**, **List**, **Add**, **Create**
    - Start and expiry date/time - **Select expiry date in the distant future**
    - Allowed protocols - **HTTPS only**
    - After you create the SAS token, paste it in the **SAS Token** field in the Xandr UI and click **Save**.

1. **Verification**. Once you give us your **SAS token**, you must verify your SAS permissions before your Azure Blob Storage Cloud Export can be activated. Click **Verify** (on the **Cloud Export to: Microsoft Azure Blob Storage** page) to run a series of tests that mimic actions that occur during an actual export. Once your export is verified, it is active. Data from the feed will automatically be exported to your Azure container (starting in the next hour).

### Google Cloud Storage

1. Create a [Google Storage Bucket](https://cloud.google.com/storage/docs/creating-buckets) which will serve as a drop box for log-level data from the Xandr Cloud Export system.

1. Select **Log-Level Data** from the **Network** (or **Reporting**) menu in the Xandr UI.

1. Click **Manage** in the **Cloud Export** column of the feed for which you want to create a Google Cloud Storage export. The **Google Cloud Storage** section will be displayed.

1. Click **New** to set up a new export or **Configure** to edit an existing export. The **Cloud Export to: Google Cloud Storage** page will be displayed.

1. **Authorization**. Navigate to [Cloud Storage console](https://console.cloud.google.com/storage), select your bucket, and click **SHOW INFO PANEL**. Add our Google member `prod-lld-gcs-{XANDR MEMBER ID}@appnexus-cloud-export.iam.gserviceaccount.com` to your bucket permissions and assign it [Cloud Storage IAM Role](https://cloud.google.com/storage/docs/access-control/iam-roles) (This role has the full admin access). An example of Google member for Xandr member ID 123456 is: `prod-lld-gcs-123456@appnexus-cloud-export.iam.gserviceaccount.com`

1. **Setup**. Enter the information in the table below and click **Save**:

    | Setting | Description |
    |---|---|
    | Bucket | Name of the [Google Storage Bucket](https://cloud.google.com/storage/docs/creating-buckets) created in step 1. |
    | Manifest Path | Root for manifest files (e.g., */manifests*). This file path does not support macros. |
    | Feed Path | Feed path with macros (e.g., */feeds/%FEED_NAME%/%YEAR%/%MONTH%/%DAY%/%HOUR%/%TIMESTAMP%*) |
    | Notification Email | Comma-separated list of emails. If Cloud Export can no longer access your bucket, your export will be deactivated and you will be notified by email. |
    | Format | Data format for log-level data files (e.g., *protobuf*) |

    > [!WARNING]
    > Do not manually create any manifest- or feed-related paths. Doing so will cause your export to fail to verify due to object-level ACLs.
    >
    > The necessary paths will be automatically created by Xandr.

1. **Verification**. Once you give our Google member the **Storage Admin** role in your bucket, you must verify your permissions before your Google Storage Cloud Export can be activated. Click **Verify** (on the **Cloud Export to: Google Cloud Storage** page) to run a series of tests that mimic actions that occur during an actual export. Once your export is verified, it is active. Data from the feed will automatically be exported to your Google Cloud Storage bucket (starting in the next hour).

## Failures and export deactivation

If the export fails, Xandr automatically runs verification tests to ensure that the failure was not caused by a permissions issue.

- If the failure was caused by a permissions issue, your export will be deactivated and you will be notified via email. You will then need to re-verify your export. A successful verification will reactivate your export.
- If the failure was not caused by permissions issues, the export will automatically be re-tried.

> [!NOTE]
> If Xandr deactivated your cloud export due to a permissions issue, once the export has been re-verified and re-enabled, we will only backfill up to a maximum of 3 days of feed data.

## Feed path macros

Macros can be used within feed paths to customize the feed output location by data hour, feed timestamp, and other metadata. Supported macros are listed below:

| Macro | Description |
|---|---|
| %DAY% | Data day (dd) |
| %FEED_NAME% | Name of the feed |
| %HOUR% | Data hour (HH) |
| %MONTH% | Data month (MM) |
| %TIMESTAMP% | Feed processing timestamp (yyyyMMddHHmmss) <br><br> **Note**: Since directories are overwritten when data is copied and Xandr can sometimes reprocess data, the %TIMESTAMP% macro is required for feed paths. |
| %YEAR% | Data year (yyyy) |

## Manifest files

Manifest files help keep track of the files uploaded by the Cloud Export service. Since cloud object stores (e.g., Amazon S3, Azure Blob Storage, Google Cloud Storage) are eventually consistent, a source of truth (i.e., which files should exist) is required for downstream consumers. The manifest file is a JSON object written to a pre-configured location in your bucket. It is specified in the [JSONSchema](https://json-schema.org/) format. We recommend that all accessing of paths (e.g., for data processing, purging, etc.) be done by first referencing the manifest files. The manifest files contain important information about data age, status, and format.

### File naming and paths

Manifest files are created when the feed begins processing for a given hour. The files will be created in the path location you specified. Manifest file names contain the name of the feed, a timestamp denoting the hour of the data (the range of time it covers), and a processing timestamp. A manifest file is created for each feed, member (seat) ID, hour of data, and feed run. Xandr automatically reprocesses data as needed. The files are also given suffixes indicating the status of the associated feed job.

- If a manifest file has a suffix of "*-failed*" or "*-processing*", it indicates that the feed was not successfully processed.
- If a manifest file has no suffix, it indicates that the feed's data is ready for ingestion.

### General format

`{feed_name}-{seat_id}-{YYYYMMddHH}-{yyyyMMddHHmmss}.json[-{suffix}]`

### Status: "Processing"

|   |   |
|---|---|
| **Suffix** | -processing |
| **Example** | standard_feed-998-2017013109-20170131132522`.json-processing` |

### Status: "Failed"

> [!NOTE]
> Since failures can occur from unrecoverable situations that make it impossible to change the manifest file's suffix, it is possible that a manifest file suffix is changed from “processing” to “failed” sometime later (e.g., during the next successful run). For example, if a Cloud Export process fails because of a change to the bucket's access policy, it will no longer be able to write to that bucket (and the export will be deactivated). The manifest's file suffix will remain "-processing" until the export is reactivated and runs successfully.

|   |   |
|---|---|
| **Suffix** | -failed |
| **Example** | standard_feed-998-2017013109-20170131132522`.json-failed` |

### Status: "Successful"

|   |   |
|---|---|
| **Suffix** | None |
| **Example** | standard_feed-998-2017013109-20170131132522`.json` |

### Feed processing workflow

It is useful to understand how Feed jobs interpret manifest files in order to build your downstream logic. The process is as follows:

1. The manifest path is scanned for entries with the “-processing” suffix. Entries with this suffix indicate a previous run that experienced a fatal error. These entries are renamed with a “-failed” suffix (e.g., *json-processing* > *.json-failed*).  
1. A manifest file is generated and written to the bucket with a “-processing” suffix.
1. The feed data is written to the bucket.
1. If the write process fails, the manifest file will be renamed to include a “-failed” suffix (e.g., *.json-failed*). If the write process is completed successfully, the “-processing” suffix is simply removed (e.g., *.json-processing* > *.json*), indicating a completed run.

### Manifest file schema

The schema for the manifest file is described in the well-known [JSONSchema](https://json-schema.org/) format. Xandr recommends code-generating classes from the JSONSchema we provide. A project that achieves this for Java is [jsonschema2pojo](https://www.jsonschema2pojo.org/).  

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "description": "Schema for the cloud export feed file manifest",
  "type": "object",
  "required": [
    "hour",
    "files",
    "feed_type",
    "path",
    "processed_on",
    "feed_properties",
    "seat_id"
  ],
  "properties": {
    "hour": {
      "description": "Timestamp for the data in yyyy-MM-dd HH:mm:ss",
      "type": "string"
    },
    "files": {
      "description": "array of object describing the exported files",
      "type": "array",
      "items": {
        "$ref": "#/definitions/feed_file"
      }
    },
    "feed_type": {
      "description": "name of the feed",
      "type": "string"
    },
    "path": {
      "description": "fully qualified destination location",
      "type": "string"
    },
    "processed_on": {
      "description": "completion timestamp of feed (yyyyMMddHHmmss)",
      "type": "string"
    },
    "feed_properties": {
      "description": "data format related information",
      "type": "object",
      "$ref": "#/definitions/feed_properties"
    },
    "seat_id" : {
      "description" : "the Xandr seat id that these files belong to",
      "type" : "integer"
    }
  },
  "definitions": {
    "feed_file": {
      "type": "object",
      "required": [
        "checksum",
        "name"
      ],
      "properties": {
        "checksum": {
          "type": "string"
        },
        "name": {
          "type": "string"
        }
      }
    },
    "feed_properties": {
      "type": "object",
      "required": [
        "compression_type",
        "container_format",
        "checksum_type",
        "data_format"
      ],
      "properties": {
        "compression_type": {
          "description": "type of compression used on the files (BLOCK level compression for sequence files)",
          "type": "string",
          "enum": [
            "DEFLATE",
            "GZIP",
            "SNAPPY",
            "NONE"
          ]
        },
        "container_format": {
          "description": "container format of the data",
          "type": "string",
          "enum": [
            "AVRO",
            "SEQUENCE",
            "NONE"
          ]
        },
        "data_format": {
          "description": "format of the data",
          "type": "string",
          "enum": [
            "protobuf",
            "protobuf-delimited",
            "avro"
          ]
        },
        "checksum_type": {
          "description": "type of checksum",
          "type": "string",
          "enum": [
            "MD5"
          ]
        }
      }
    }
  }
}
```

### Manifest file example

```
{
  "hour" : "2017-02-09 16:00:00",
  "files" : [ {
    "checksum" : "ccd5774e8fc785b4df3d63627f992c4b",
    "name" : "998-10-ccd5774e8fc785b4df3d63627f992c4b-998"
  }, {
    "checksum" : "c8c442ff5eb24237573faa2d60a689b1",
    "name" : "998-11-c8c442ff5eb24237573faa2d60a689b1-998"
  } ],
  "feed_type" : "standard_feed",
  "path" : "/standard_feed/2017/02/09/16/20170209220747",
  "processed_on" : "20170209220747",
  "feed_properties" : {
    "compression_type" : "SNAPPY",
    "container_format" : "SEQUENCE",
    "data_format" : "protobuf",
    "checksum_type" : "MD5"
  },
  "seat_id" : 998
}
```

## Failures/Partial loads

Feed job failures can cause partial data loading. To avoid consuming partially loaded data, use the manifest file names to determine what to consume.

- Do not consume files which will have a suffix of “*-processing*” or “*-failed*”. These are incomplete data sets.
- Only consume data from paths corresponding to completed loads (i.e., manifest files with a *.json* extension but no additional suffix).

## Purging

When purging old data from your bucket, the manifest files should be used for determining when data is eligible for purging. Only purge those files that are no longer relevant (e.g., older than a week).

> [!NOTE]
> To improve directory performance, manifest files older than 30 days will be moved to an /archive folder located within the manifest file path. As a precaution, if you have any procedures/scripts that refer to the manifest file path directly, you should amend them to also look in the **/archive** folder for manifest files older than 30 days.

## Reprocessing

Feeds re-processed for a given hour will never overwrite old data. Xandr will reprocess data when inconsistencies are detected. When a feed job is reprocessed, there will be two (or more) manifest files corresponding to the same data hour. However, the processing timestamps and paths will differ between runs. The file with the latest timestamp will be the corrected one.

## Client data loss

Xandr does not re-export data that has already been successfully exported. To mitigate situations in which you may have accidentally deleted successfully exported data, we recommend you leverage your cloud provider’s backup or versioning features.

## Troubleshooting

### Uniqueness criteria for configurations

Your Cloud Export configuration must be unique, which means:

- For **Manifest paths**:
  - For **Microsoft Azure**, if the **Destination** (**Storage Account** and **Container**) combined and **Path** are the same, the **Member ID** and **Feed**  *must be different*.
  - For **all other configurations**, if the **Bucket** and **Path** are the same, the **Member ID** and  **Feed**  *must be different*.
- For **Feed paths**, if the **Destination** and **Resolved Feed path** are the same, the Member ID  *must be different* and the **Feed** and **Format** *must be the same*.

### Verification issues

The section below describes a few common issues that you may encounter when getting verification set up.

Possible failed verify actions:

- [Checking for manifest files in GLACIER](#checking-for-manifest-files-in-glacier)
- [Checking meta-information access on manifest files](#checking-meta-information-access-on-manifest-files)
- [Creating prefix at `<path>`](#creating-prefix-at-path)

#### Checking for manifest files in GLACIER

**Potential Cause**: Archiving of manifest files is not properly set up

**Applies to**: Amazon S3

**Solution**:

Please ensure that all lifecycle rules are set up to move manifest objects to Glacier only if they are not in the manifests path (manifests/archive is fine).

#### Checking meta-information access on manifest files

**Potential Cause**: You are revoking object-level access for non-archived manifests

**Applies to**:

- Amazon S3

**Solution**:
For each object, `aws s3api get-object-acl --bucket <bucket> --key <object>` should yield the following as one of the grants for each non-archived manifest object:

```
{
   "Grantee": {
    "Type": "CanonicalUser",
    "DisplayName": "aws-slld",
    "ID": "669331f902bdea32b620b6e6c85123d153b5b30c8318b101d2fd202bc3906fe1"
    },
    "Permission": "FULL_CONTROL"
},
```

- Google Cloud Storage

**Solution**:
For each object, `gsutil acl get <object>` should yield the following as one of the grants for each non-archived manifest object:

```
{
    "email": "prod-lld-gcs-<member>@appnexus-cloud-export.iam.gserviceaccount.com",
    "entity": "user-prod-lld-gcs-<member>@appnexus-cloud-export.iam.gserviceaccount.com",
    "role": "OWNER"
}
```

#### Creating prefix at `<path>`

**Potential Cause**: You have already applied authorization to your bucket or container but have manually created any manifest or feed "folders".

**Applies to**: All Cloud Export configurations

**Solution**:

Manually created objects have different ACLs that may deny access to the Cloud Export system. Please delete any manually created manifest or feed objects. The Cloud Export system will create necessary objects on its own.
