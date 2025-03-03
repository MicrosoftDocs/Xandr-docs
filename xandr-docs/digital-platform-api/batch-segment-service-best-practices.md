---
title: Digital Platform API - Batch Segment Service Best Practices
description: In this article, find information about the recommended best practices regarding Batch Segment Service (BSS) and answers to some frequently asked questions regarding BSS.
ms.date: 10/28/2023
ms.custom: digital-platform-api
---

# Digital Platform API - Batch Segment Service best practices

The Batch Segment Service (BSS) allows you to send bulk feeds of external segment data to Xandr. Using BSS, you can easily integrate your first, second, or third-party audience data to create dynamic, configurable segments for sophisticated user targeting and increased ROI.

## Best practices

- Read the [FAQs](#faqs) below. Chances are your question is answered there.

- Keep your cookie mapping fresh and user match rate high by collecting UIDs as frequently as possible.

    Xandr expires UIDs on a rolling basis such that the user IDs that haven't been seen for the longest period of time are removed from our database to make room for new user IDs. If you upload UIDs that are very old, chances are you will have a high percentage of invalid user IDs in your status report.

- Batch your files as much as possible (between 100 to 300 MB).

    Your data will be uploaded more quickly in a few large files rather than a large amount of very small files.

- Dedupe your files.

    You'll be able to keep the size and processing time down by removing any duplicate user/segment combinations from your files.

- Compress your files.

    Gzip is the only compression method supported by this service. By compressing your files, you'll be able to upload more data more quickly.

- Avoid sending the full segment membership in every file.

    Instead, you only need to send the changes in segment membership (the deltas) since the last upload. This will greatly reduce the size of your files and speed up the upload process.

- Use the upload URL immediately.

    After requesting an upload URL, be sure to use it within 5 minutes, or you'll need to request a new URL. You cannot reuse old URLs.

- To optimize your daily BSS upload limit, ensure that you are sending user data into segments that exist or that were created on the Xandr platform.

    Sending data to invalid, deleted, or non-existent segments on the Xandr platform would count toward your total daily BSS upload limit. This can lead to false assumptions about why certain segments do not scale and why segments have low utilization. Take a look at the `error_log_lines` data field when you [view your file upload history](troubleshooting-bss-uploads.md#view-your-file-upload-history). It will list all the invalid segment IDs that were passed in the uploads.

- Avoid uploading your largest files during peak hours (10 am-10 pm EST in the US, 10 am-10 pm CET in Europe).

    During peak hours, more files are in the queue, and your file may take longer to be processed. If you can, schedule your uploads to happen overnight. Per the SLA, uploads could take up to 24 hours.

- Check the [status report](../bidders/uploading-segment-data-using-bss.md#check-the-job-status).

    Checking the status report will allow you to catch and correct errors and upload more accurate data.

- Confirm it worked.

    After your data has been processed, you can spot-check a few user IDs using the cookie viewer. If you don't see the segments in one geography, check the other - chances are your user is in another geo.

  - US: `https://ib.nym1.adnxs.com/cookie?member_id=MEMBER_ID&amp;dongle=DONGLE&amp;uid=USER_ID`
  - EU: `https://ib.ams1.adnxs.com/cookie?member_id=MEMBER_ID&amp;dongle=DONGLE&amp;uid=USER_ID`
  - Asia: `https://ib.sin1.adnxs.com/cookie?member_id=MEMBER_ID&amp;dongle=DONGLE&amp;uid=USER_ID`

- Include the job ID in support requests.

    If you're experiencing technical issues, remember to include all relevant job IDs when submitting your request on our [Customer Support Portal](https://support.ads.microsoft.com).

> [!NOTE]
> Be sure to wait approximately 20 minutes before trying to add users to any newly created segments (to allow these segments to be propagated to all servers). As a best practice, try to minimize the creation of new segments, reuse existing segments where possible, or use segment `"values"` to further subdivide users within existing segments. These practices will ensure successful user uploads to segments. For details on creating segment `"values"`, see [Segment Targeting](profile-service.md).

## FAQs

- **I have completed the upload jobs. However, I see that there are errors.**

    If you encounter errors, you may reference the [BSS Troubleshooting](troubleshooting-bss-uploads.md) document to diagnose potential cause.

- **How long after my upload until the data is available for targeting?**

    Your segment data begins to be available for targeting as soon as your job hits the `'validating'` phase. The data is fully ingested and ready for targeting once your job has hit `'completed'`. The time until your job hits `'completed'` depends on the size of your file and the number of other files in the queue.

    > [!NOTE]
    > Allow up to 24 hours for uploads to process (per the Xandr SLA).

- **Will there be a "fired" timestamp on these users for segment age targeting?**

    If you choose to include the TIMESTAMP field in your files, then you'll specify the timestamp for every user/segment combination. If you do not include TIMESTAMP, then the timestamp will be the time at which the data was written to our server-side cookie store, which is usually around the "completed time" you see in your status report.

    > [!NOTE]
    > The time is in the UTC time zone.

- **What if I have some users in the US and some in Europe?**

    Xandr maintains three separate cookie stores in the US, Europe, and Asia. However, you do not need to upload separate files for each geography. The Batch Segment system will automatically determine which geo the user is in and send the data to that cookie store database. If the user is in multiple geographies, the data will be sent to each geo the user exists in.

- **Why am I limited to only 999 error lines?**

    The 999 error lines provided are not meant to be a comprehensive list of all errors. Instead, they should be used as a diagnostic tool to diagnose problems with your file and then correct them.

- **Why are some jobs missing when I view my entire job history?**

    When you view your complete file upload history, every single file you've ever uploaded will be included. However, our API limits responses to 100 objects via pagination. You can view additional objects by appending one of these to the API call:

    `&start_element=101`

    `&sort=last_modified.desc`

    You can read more about pagination in [Throttling, Pagination, and Filtering](05---throttling-pagination-and-filtering.md).

- **If I include the `VALUE` field, do I have to list a value for every single user/segment combination?**

    Yes, you do. However, if you do not wish to assign a value, you can enter `0` as the value.

- **How often can I push batch segment uploads?**

    Our systems can handle a maximum of one upload per minute (per member). Any upload interval larger than one minute will work properly.

- **I received a notification, 'Attempting to exceed daily byte upload limit'. Can I continue to upload data files?**

    Be aware of your daily BSS limit size. If you receive an error message from our system, stop your file upload jobs immediately. Continuing your file upload with repeated error messages could lead to system delays. Wait an hour and then try your file upload again.

- **Should I compress upload files before submitting them through the API Batch Segment Service?**

    Yes! As a best practice, you should always compress upload files before pushing them through the Batch Segment Service. The gzip compression standard is supported.

- **Should I always push my complete audiences every time I upload to segments through the API Batch Segment Service?**

    As a best practice, you should only upload full audiences through the API Batch Segment Service when you are uploading the audience for the first time or when the audience has expired from its respective segment. Besides those two cases, you should always upload modifications (deltas) to your existing audiences. Batch Segment uploads do not refresh the time to live of cookies in the Xandr cookie store (they can only refresh the time that the cookies are associated with a particular set of segments).

- **Should I sort the UIDs in my batch segment upload files?**

    Sorting your file by user ID helps our system process your file more quickly.

- **How can I see a job's user match rate?**

    The user match rate of a job is the percentage of IDs our system had seen before, divided by the total amount of identifiers uploaded. This can be a useful metric to get an indication of the quality of data that has been uploaded. Internal teams at Xandr also use this metric to assess the quality of the data uploaded. The formula to calculate the match rate is:

    user match rate = `num_valid_user` / (`num_valid_user` + `num_invalid_user`)

- **I don't think this is working. Can you help?**

    Sure! Submit a case through our [Microsoft Advertising Customer Support Portal](https://support.ads.microsoft.com). Note that while the job status reports are kept with 30 days of jobs history, we only save the actual file of data for 3 days. Please be sure to submit your case as soon as possible after uploading so that we can look at the data you uploaded.

- **Why do I see some IDs in LLD that were not uploaded via BSS?**

   Targeting uploaded IDs will also target related IDs linked to the same user. As a result, you may see IDs that were not uploaded in LLD. When this occurs, the ID was linked to the same user as the uploaded ID via a related device ID.

## Related topics

- [Batch Server-Side Segmentation](batch-server-side-segmentation.md)
- [Initial BSS Account Setup](initial-bss-account-setup.md)
- [Troubleshooting BSS Uploads](troubleshooting-bss-uploads.md)
