---
title: Bidders - Verifying Segment Uploads
description: Explore upload success, confirm file status, and ensure essential parameters validate successful uploads.
ms.date: 10/28/2023
---

# Bidders - Verifying segment uploads

There are a few ways to confirm that your uploads are successful.

- When checking the status of your file, you will receive a status report that contains the following useful parameters

  | Parameters | Description |
  |---|---|
  | `num_valid` | The number of valid user-segment pairs in the file. |
  | `num_valid_user` | The total number of valid user IDs in the file. Each user can be resolved in up to three regions. Each resolved region counts as one. Therefore the total number of valid users can exceed the number of distinct user-segment pairs. |
  | `num_invalid_user` | The total number of invalid user IDs in the file. |
  | `segment_log_lines` | The number of unique valid users added to each segment. The format is `[SEGMENT ID]-[NUMBER OF USERS]`.<br>**Note**: This field is limited to 999 lines in your file. If you have more than 999 segments in the job, some of them will not be shown. |

- Use the [Segment Loads API Report](../digital-platform-api/segment-loads-report.md) to see the number of valid user IDs that have been loaded into a segment over a given time period.

- Spot check a few user IDs to confirm they have been added to the appropriate segments using the below URLs. If you don't see the user in one geo, be sure to check the other geo.  

  US: `https://ib.nym1.adnxs.com/cookie?member_id=MEMBER_ID&amp;dongle=DONGLE&amp;uid=USER_ID`
  
  EU: `https://ib.ams1.adnxs.com/cookie?member_id=MEMBER_ID&amp;dongle=DONGLE&amp;uid=USER_ID`
  
  Asia: `https://ib.sin1.adnxs.com/cookie?member_id=MEMBER_ID&amp;dongle=DONGLE&amp;uid=USER_ID`
  
- If you have access to the Xandr UI, use the Segment Inventory Overlap report to gauge how many impressions you
  can expect to see by segment, seller, and country or region. Note that you’ll need to wait a few days after creating new segments before data will show up in this report.
