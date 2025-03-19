---
title: RTSS Best Practices
description: In this article, explore the best practices for the Real-Time Signals Service (RTSS).
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# RTSS best practices

> [!WARNING]
> **Beta Notice**
>
> - The Real-Time Signals Service is in Beta, and is subject to change in the future.
> - As we transition to open beta, **we will be adding a monthly charge for new and existing clients that use RTSS**. For more information, speak to your account manager.

The following best practices will help you be successful using RTSS.Following these best practices will help you effectively use RTSS.  

## Targeting  

- **Consolidate shared targeting features** – Features that are shared across multiple segments should be grouped into reusable segments to simplify management.  
- **Leverage feature-based reporting** – Reporting is available by querying feature targeting instead of querying by segment. Reducing the number of segments associated with each targeted feature improves organization and TTL management.  
- **Use shorter TTLs for better management** – We recommend using a **30-day TTL** for uploads to simplify segment management.  
- **Monitor TTL and expiry** – Since RTSS segments degrade over time, tracking TTL and expiry is crucial to maintain campaign performance.  
- **Refresh targeting features regularly** – To maintain accuracy, refresh targeting features predictably (for example, every **30 days** when using a **30-day TTL**).  
- **Use the expiry feature for control** – The expiry feature on file uploads provides more precise control over expiration dates.  
- **Upload deltas instead of full files** – To reduce upload and processing time, upload only changes instead of entire datasets.  
- **Use 8-character OLC symbols** – For **OLC targeting**, we recommend using 8-character symbols (~275m block) for better accuracy.  

## File preparation  

- **Use GZIP compression** – Compress **CSV bulk uploads** using **GZIP** to optimize performance.  
- **Ensure correct file format** – Save files in **UTF-8 (without BOM) encoding**. Use **Unix-style line endings** (line feed `\n`), and ensure the file does not contain a trailing line ending.  

## Uploading  

- **Handle API rate limits** – Use **3- to 5-second** retries to prevent throttling.  
- **Store data regionally** – Data uploaded to a specific **region** is not interoperable across regions. If RTSS is used globally, upload data separately to the required regions.  

## Campaign usage  

- **Exclusion targeting is not supported** – RTSS segments cannot be used for **exclusion targeting** in campaigns.  

## Regions supported  

RTSS operates across multiple regions. Since data uploaded to a specific region cannot be accessed in another region, upload data separately for each required region.  

### Available endpoints  

| **Region** | **Endpoint** | **Notes** |  
|-----------|-------------|----------|  
| **Global** | `https://api.appnexus.com/apd-api/` | Default endpoint resolves to either AMER/EMEA or APAC based on the uploader's origin. |  
| **Americas and EMEA** | `https://api.appnexus.com/apd-api-americas/`  **or**  `https://api.appnexus.com/apd-api-emea/` | Data published to AMER is replicated to EMEA. Uploading to one of these datacenters ensures availability in both regions. |  
| **APAC** | `https://api.appnexus.com/apd-api-apac/` | APAC datacenters are isolated from AMER/EMEA. Upload separately for APAC. |  

### Choosing the right endpoint  

- If you **don't need data in APAC**, use the **default endpoint**.  
- If you **need data everywhere, including APAC**, upload to **both** the **default** and **APAC endpoints**.  
- If you **regionalize your data**, upload to the **specific regional endpoint** where the data is needed.  

For guidance, contact your **account manager**.
