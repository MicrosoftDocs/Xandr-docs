---
title: Add a Microsoft Outlook Creative via the API
description: This article provides specifications for Outlook creatives and shows you how to add them to the system via the creative service.
ms.date: 10/22/2025
ms.service: publisher-monetization
ms.subservice: digital-platform-api
ms.author: shsrinivasan
---

# Add a Microsoft Outlook creative via the API

Microsoft Outlook creatives show up in the right-hand sidebar of the free [outlook.com](https://www.microsoft.com/) webmail service after a user securely logs in. This page provides specifications for Outlook creatives and shows you how to add them to our system via the [Creative Service](./creative-service.md).

> [!NOTE]
> Outlook creatives must pass our SSL audit and the Microsoft Creative Acceptance Policy audit.

## Specifications

This section defines the fields of the [Creative Service](./creative-service.md) that are required for Outlook creatives. These fields must be passed in the JSON object on `POST`. See [Step 1](#step-1-create-a-json-file-with-your-creative-details) below for formatting details.

:::image type="content" source="./media/specifications.png" alt-text="Screenshot that shows the required fields for Outlook creatives.":::

| Field | Type | Required? | Description/Requirements |
|:---|:---|:---|:---|
| `secure_content` | string | Yes, if adding a hosted creative | **For hosted creatives**: The image for the secure Outlook creative. Clicking on the image takes the user to the Landing Page URL.<br> - File must be in one of the following formats: JPG, PNG, GIF.<br> - File must be base64-encoded.<br> - Image must be 100x72 pixels (see `width` and `height` below). If the image is any other dimension, it will be scaled proportionally when rendered to fit within 100x72.<br> - Must not be flash.<br> - Must not include any animation.<br> - Initial load size must be less than 40 KB. |
| `content` | string | Yes, if adding a hosted creative | **For hosted creatives**: The image for the *non-secure* Outlook creative. Although only the secure image will get served to [outlook.com](https://www.microsoft.com/) inventory, you are required to add a non-secure version as well.<br> - File must be in one of the following formats: JPG, PNG, GIF.<br> - File must be base64-encoded.<br> - Image must be 100x72 pixels (see `width` and `height` below). If the image is any other dimension, it will be scaled proportionally when rendered to fit within 100x72.<br> - Must not be flash.<br> - Must not include any animation.<br> - Initial load size must be less than 40 KB. |
| `media_url_secure` | string | Yes, if adding a third-party creative | **For third-party creatives**: The URL of image for the secure Outlook creative.<br> - URL must be secure (https).<br> - File must be in one of the following formats: JPG, PNG, GIF.<br> - Image must be 100x72 pixels (see `width` and `height` below). If the image is any other dimension, it will be scaled proportionally when rendered to fit within 100x72.<br> - Must not be flash.<br> - Must not include any animation. |
| `media_url` | string | Yes, if adding a third-party creative | **For third-party creatives**: The URL of image for the non-secure Outlook creative.<br> - File must be in one of the following formats: JPG, PNG, GIF.<br> - Image must be 100x72 pixels (see `width` and `height` below). If the image is any other dimension, it will be scaled proportionally when rendered to fit within 100x72.<br> - Must not be flash.<br> - Must not include any animation. |
|`width` | int | Yes | The width of the image for the Outlook creative.<br><br>Width must be 100 pixels. Even if the actual image is not 100x72, you still must set this field to 100 to serve properly. |
| `height` | int | Yes | The height of the image for the Outlook creative. <br><br>Height must be 72 pixels. Even if the actual image is not 100x72, you still must set this field to 72 to serve properly. |
| `file_name` | string | Yes, if adding a hosted creatives | **For hosted creatives**: The name of the image file and the file extension (.jpg, .png, or .gif).<br><br> Filename can be a maximum of 1000 characters. |
| `click_url` | string | Yes | The URL where users will be redirected when they click the Outlook ad.<br> - URL can be a maximum of 1024 characters.<br> - URL must begin with "http://" or "https://". |
| `template` | object | Yes | The Xandr rendering template for Outlook creatives.<br><br> The `id` field in this object must be set to `3033` ([outlook.com](https://www.microsoft.com/) versaTiles One-Tile). |
| `allow_ssl_audit` | boolean | Yes | Whether or not the creative will be submitted to our secure audit as well as Microsoft Creative Acceptance Policy audit.<br><br> This must be set to `true` because Outlook creatives must pass both our SSL and Microsoft Acceptance Policy audits in order to serve on [outlook.com](https://www.microsoft.com/) inventory, which is secure. |
| `custom_macros` | array of objects | Yes (some parts are optional) | The headline, description, flex tile label, and impression tracking pixels for the Outlook creative. The headline and description are required, whereas the flex tile label and impression tracking pixels are optional.<br><br>The `HEADLINE` macro defines the text that displays above the image. <br><br>Requirements:<br> - Maximum of 25 characters including spaces.<br> - Must not contain newline characters.<br> - Must not include 2 consecutive punctuation marks. <br> - Must not consist entirely of capital letters.<br> - Must not start with punctuation.<br>Must not include double spaces.<br> - Must not include more than 2 consecutive 1 character words.<br> - Must not include special characters like < > * \ ^ ~ _ = { } [ ] \| < >.<br><br>The `DESCRIPTION` macro defines the text that displays under the image. <br><br>Requirements:<br> - Maximum of 90 characters including spaces, with no word having more than 20 characters.<br> - Must not include 2 consecutive punctuation marks. <br> - Must not consist entirely of capital letters.<br> - Must not start with punctuation.<br> - Must not include double spaces.<br> - Must not include more than 2 consecutive 1 character words.<br> - Must not include special characters like < > * \ ^ ~ _ = { } [ ] \| < ><br><br>The `FLEX_LABEL` defines the optional, additional description for the Outlook creative. Requirement:<br> - Maximum of 20 characters.<br> - Using `PIXEL_URL` and `PIXEL_URL2` macros, you can add two third-party impression tracking pixels to an Outlook creative for recording impressions in an external system. You must be sure to use these macros instead of the `pixels` array.<br><br> Requirements:<br> - Final destination URL of each pixel must be secure (https) and contain a valid SSL/TLS certificate.<br> - URL of each pixel must not be more than 1024 characters. |

## Auditing requirements

- [SSL Audit](#ssl-audit)
- [Microsoft Creative Acceptance Policy Audit](#microsoft-creative-acceptance-policy-audit)

### SSL audit

Since [outlook.com](https://www.microsoft.com/) consists of secure inventory, Outlook creatives must pass our SSL audit in order to serve. When you add an Outlook creative to Xandr, opt into secure audit by setting `allow_ssl_audit` to `true`. For details about checking the state of the secure audit, see [Check the Audit Status of an Outlook Creative](#check-the-audit-status-of-the-outlook-creative).

### Microsoft creative acceptance policy audit

All creatives serving on [outlook.com](https://www.microsoft.com/) inventory must pass our platform audit and the Microsoft Creative Acceptance Policy audit, for which Xandr charges a standard audit fee. When you submit an Outlook creative to Xandr's secure audit, the creative is submitted to the Microsoft Creative Acceptance Policy audit by default. There's no additional option to set. For details about checking the state of the Microsoft audit, see [Check the Audit Status of an Outlook Creative](#check-the-audit-status-of-the-outlook-creative).

## Step 1. Create a JSON file with your creative details

For details about the fields to include in your JSON, see [Specifications](#specifications) above. Note that this example is for adding an Outlook creative hosted by a third-party.

```
$ cat outlook_creative
{
   "creative": {
      "name": "Outlook Creative",
      "media_url":"http://creative.com/123",
      "media_url_secure":"https://creative.com/123",
      "width": 100,
      "height": 72,
      "click_url": "https://www.testing.com",
      "file_name": "photo 1.JPG",
      "allow_ssl_audit": true,
      "template": {
         "id": 3033
      },
      "custom_macros": [
         {
            "code": "HEADLINE",
            "value": "This is the headline of the Outlook creative."
         },
         {
            "code": "DESCRIPTION",
            "value": "This is the description of the Outlook creative."
         },
         {
            "code": "FLEX_LABEL",
            "value": "This is the optional, additional description for the Outlook creative."
         },
         {
            "code": "PIXEL_URL",
            "value": "https://pixel-url.com"
         },
         {
            "code": "PIXEL_URL2",
            "value": "https://pixel-url2.com"
         }
      ]
   }
}
```

## Step 2. `POST` the JSON file to the creative service

```
$ curl -b cookies -c cookies -X POST -d @outlook_creative 'https://api.appnexus.com/creative?advertiser_id=52408'
{
    "response": {
        "status": "OK",
        "count": 1,
        "id": 706145,
        "start_element": 0,
        "num_elements": 100,
        "creative": {
            "name": "Outlook Creative",
            "brand_id": 1,
            "media_url": "https://creative.com/123",
            "id": 706145,
            "code": null,
            "code2": null,
            "member_id": 1066,
            "state": "active",
            "click_track_result": "not_tested",
            "advertiser_id": 50544,
            "publisher_id": null,
            "format": null,
            "width": 100,
            "height": 72,
            "click_url": "https://www.testing.com",
            "flash_click_variable": null,
            "no_iframes": false,
            "content": null,
            "original_content": null,
            "file_name": "photo 1.JPG",
            "track_clicks": true,
            "audit_status": "pending",
            "macros": null,
            "profile_id": null,
            "audit_feedback": null,
            "is_prohibited": false,
            "is_suspicious": false,
            "created_on": "2013-11-20 19:28:12",
            "flash_backup_url": null,
            "last_modified": "2013-11-20 19:28:12",
            "is_control": false,
            "allow_audit": true,
            "is_expired": false,
            "creative_upload_status": null,
            "backup_upload_status": null,
            "use_dynamic_click_url": false,
            "media_subtypes": [
                "banner_breakout",
                "popunder",
                "popup",
                "banner"
            ],
            "size_in_bytes": 0,
            "google_audit_status": "pending",
            "google_audit_feedback": null,
            "msft_audit_status": "pending",
            "msft_audit_feedback": null,
            "msft_external_audit_status": "pending",
            "msft_external_audit_feedback": null,
            "is_self_audited": false,
            "no_adservers": false,
            "text_title": null,
            "text_description": null,
            "text_display_url": null,
            "click_action": "click-to-web",
            "click_target": "https://www.testing.com",
            "ssl_status": "pending",
            "allow_ssl_audit": true,
            "media_url_secure": null,
            "content_secure": "https://creative.com/123",
            "original_content_secure": null,
            "flash_backup_url_secure": null,
            "is_hosted": false,
            "content_source": "standard",
            "lifetime_budget_imps": null,
            "daily_budget_imps": null,
            "enable_pacing": null,
            "allow_safety_pacing": null,
            "lifetime_budget": null,
            "daily_budget": null,
            "landing_page_url": null,
            "thirdparty_creative_id": null,
            "thirdparty_campaign_id": null,
            "facebook_audit_status": null,
            "facebook_audit_feedback": null,
            "custom_request_template": null,
            "language": {
                "id": 1,
                "name": "English"
            },
            "pop_values": null,
            "brand": {
                "id": 1,
                "name": "Unknown",
                "category_id": 8
            },
            "template": {
                "id": 3033,
                "name": "Outlook.com versaTiles One-Tile",
                "media_subtype_id": 52,
                "format_id": 4
            },
            "thirdparty_page": null,
            "custom_macros": [
                {
                    "code": "DESCRIPTION",
                    "value": "This is the description of the Outlook creative."
                },
                {
                    "code": "FLEX_LABEL",
                    "value": "This is the optional, additional description for the Outlook creative."
                },
                {
                    "code": "HEADLINE",
                    "value": "This is the headline of the Outlook creative."
                },
                {
                    "code": "PIXEL_URL",
                    "value": "https://pixel-url.com"
                },
                {
                    "code": "PIXEL_URL2",
                    "value": "https://pixel-url2.com"
                }
            ],
            "segments": null,
            "folder": null,
            "campaigns": null,
            "competitive_brands": null,
            "competitive_categories": null,
            "pixels": null,
            "mobile": null,
            "sla": "0",
            "sla_eta": "2013-11-21 09:29:12",
            "currency": "USD"
        }
    }
}
```

## Next steps

### Check the audit status of the Outlook creative

Once you've added an Outlook creative to our system, you can check where it is in the Xandr's Secure Platform and Microsoft Acceptance Policy audits. For more details, see [Check the Audit Status of an Outlook creative](check-the-audit-status-of-an-outlook-creative-via-the-api.md).

### Create an Outlook campaign

You can use the Campaign Service and the Profile Service to set up a campaign that targets [outlook.com](https://www.microsoft.com/) inventory. For more details, see [Create an Outlook Campaign via the API](./create-an-outlook-campaign-via-the-api.md).

## Related topics

- [Buying Microsoft Outlook.com Inventory](./buying-microsoft-outlook-com-inventory.md)
- [Create an Outlook Campaign via the API](./create-an-outlook-campaign-via-the-api.md)
