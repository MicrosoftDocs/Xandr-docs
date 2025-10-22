---
title: Log Level Data - Install and Configure Protocol Buffers
description: In this article, learn what protocol buffers is and find instructions for installation and configuration.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: log-level-data
ms.author: shsrinivasan
---

# Log level data - Install and Configure Protocol Buffers

Xandr Log-Level Data (LLD) is encoded using a binary interchange format called [Protocol Buffers](https://github.com/protocolbuffers/protobuf). Use the steps below to get started with protobuf and integrate LLD into your system.

## Protobuf installation and configuration

When subscribing to feeds using the Log Level Data Service, you may choose to receive your data in one of the available protobuf formats (highly recommended). The protobuf format allows for more streamlined schema changes and convenient ingestion of the data into big data systems.

The procedure below provides an example project that includes all feed schemas and demonstrates how to read Xandr protobuf files. The example project includes example binary files as well as source code that can be used as a starting point for ingestion.

1. Review the following Install dependencies. Be sure to complete the relevant tasks.
    1. Install the **protobuf compiler**. Use **one** of the following methods:
        - Use a package manager using one of the following commands:
          - For OSX, use the command: `brew install protobuf250`
          - For Ubuntu, use the command: `sudo apt-get install protobuf-compiler`
        - Build from source: [protobuf v2.5.0](https://github.com/protocolbuffers/protobuf/tree/v2.5.0).
    1. If you will be using **protobuf format** (not protobuf-delimited), install hadoop-client with native Snappy support.
    1. If you plan to use the **examples project**, install [Maven](https://maven.apache.org/). Maven is available via most package managers.
1. Download the example project (get the latest one from the **File Formats and Schemas** section of [Batch Log-Level Data](batch-log-level-data.md)) and unzip it.
1. Refer to the README file in the example project for further directions.
