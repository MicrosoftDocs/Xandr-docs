---
title: Serve Default Creatives Instead of PSAs
description: Explore default creatives over PSAs, emphasizing benefits, sustained ad revenue, user engagement in absence of suitable targeted ads.
ms.date: 10/28/2023
---

# Serve default creatives instead of PSAs

Many publishers need to minimize or eliminate public service announcement (PSA) delivery to ensure delivery to passback tags. Following the instructions below will eliminate PSA delivery in almost all cases.

## 1. Make sure the creative is secure

If your default creative is not SSL audited and your placement is run as secure (`https`), then a PSA will show instead of your default creative. Even if you are certain that you exported your tags as non-secure, some partners will automatically add the `https`. If that happens, you will serve PSAs. If you do NOT want to serve PSAs, you must submit your creative for SSL audit or ensure that partners are not running your tags with `https`.

To submit your creative for SSL audit,

1. Navigate to **Publishers** \> **Placement Manager**, then select the placement to which you want to add a secure default creative by clicking anywhere in the row. This displays the placement details and any default creatives already assigned to the placement.

1. In the **Default Creatives** pane, click **Add**. This opens the **Add Default Creative** dialog. Be sure to check the **Allow SSL** box.

1. If you upload a file directly to Microsoft Monetize, ensure the creative will be eligible to serve on secure inventory.

1. If you input a third-party creative, be sure to add both the standard and secure tag.

1. Once an SSL enabled creative has been uploaded it will be automatically checked to ensure it is able to serve on secure inventory. If there is an issue and the creative is not eligible for secure pages you will receive an email notification detailing the issue. If you receive such an email update the creative accordingly.

## 2. For sizeless placements, set a default creative for every size

If you have a sizeless placement and do not have a default creative set up for a particular size, then you will serve a PSA for that size. You can prevent this by uploading a default creative for all sizes that you want to use.

1. To see what size creatives a sizeless placement is serving, run a Publisher or Network Analytics Report with filter by `Placement` and group by `Size` criteria.

1. Make sure the date range is at least a month to ensure you capture the most possible sizes.

1. Once you know all the sizes that are serving for the placement, upload default creatives for each, following the procedure outlined in Step 1 above.

   > [!NOTE]
   > Full instructions for uploading default creatives can be found in [Assign a Default Creative to a Placement](assign-a-default-creative-to-a-placement.md).

## 3. Set the direct advertisers trust level to maximum

If your publisher Ad Quality setting has a trust level other then Maximum, this may block default creatives from serving.

To update your Ad Quality settings in Microsoft Monetize,

1. click **Publishers** and choose **Ad Quality** from the menu that appears.

1. Select the publisher you want to work with.

1. Under **Buyers** \>  **Default advertisers trust** you can see the current setting.

1. If it's set to anything other then **Maximum**, click the **pencil**, update the trust level, and apply your changes.

## Related topics

- [Create a Placement](create-a-placement.md)
- [Default PSAs](default-psas.md)
- [Assign a Default Creative to a Placement](assign-a-default-creative-to-a-placement.md)
