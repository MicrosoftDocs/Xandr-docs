---
title: Microsoft Invest - Creative Character Specifications
description: This page talks about valid and invalid VAST characters present in the VAST url as well as in the 3rd party segments attached to the creative.   
ms.date: 09/11/2025
---

# Microsoft Invest - Creative character specifications 

There are character specifications that you should keep in mind when uploading creatives on to the Microsoft Advertising platform.

For creatives, ensure that there is no invalid or unsupported character present in the VAST url as well as in the 3rd party segments attached to the creative. For example,

- This is the set of valid VAST characters:

    `ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789-._~:/?#[]@!$&'()*+,;=.`
- This is a set of common invalid characters:

    `|, <, >, ^, {,}.`

Additionally:

- If there are curly brackets `{ }` present in the VAST url or segment, then they **must** have `$` in front of the bracket.
- Ensure that there is no double `%` present in the VAST url or segment.

The following table provides the character limit for each field that is available from the Creative screens within the UI:

| Field Name | Creative Type | Corresponding Screen | Character Limit |
|--|--|--|--|
| **Search** | All | **- Creative Manager**<br>**- Creative UI > Create New**<br>**- Creative UI > Edit**<br>**- Creative Templates**<br>**- Native Assembly > Create New**<br>**- Native Assembly > Edit** | No Limit |
| **Create New Folder** | All | **- Creative Manager**<br>**- Creative UI > Create New**<br>**- Creative UI > Edit** | 255 |
| **Name** | All | **- Creative Manager**<br>**- Creative UI > Create New**<br>**- Creative UI > Edit**<br>**- Creative Templates > Details** | 400 |
| **Duplicate Name** | All | **Creative Templates** | 30 |
| **Media Type** | All | **Creative Templates > Details** | No Limit |
| **Template Code** | All | **Creative Templates > Details** | 100 |
| **Macro** | All | **Creative Templates > Details > Custom Macros** | 30 |
| **Size** | All | **- Creative Manager**<br>**- Creative UI > Create New**<br>**- Creative UI > Edit** | 32,000 |
| **Landing Page URL** | All | **- Creative Manager**<br>**- Creative UI > Create New**<br>**- Creative UI > Edit** | 2000 |
| **Trackers > Custom Pixels** | All | **- Creative Manager**<br>**- Creative UI > Create New**<br>**- Creative UI > Edit** | No Limit |
| **Brand URL** | All | **- Creative Manager**<br>**- Creative UI > Create New**<br>**- Creative UI > Edit** | No Limit |
| **External Identifier** | All | **- Creative Manager**<br>**- Creative UI > Create New**<br>**- Creative UI > Edit** | 100 |
| **- Title**<br>**- Custom Title 1 - 5**<br>**- Body Text**<br>**- Custom Body 1 - 5**<br> **- Sponsored By**<br>**- Call to Action**<br>**- Custom Call to Action 1 - 5**<br>**- Display URL**<br>**- Custom Display URL 1 - 5**<br>**- Price**<br>**- Sales Price**<br>**- Rating**<br>**- Likes**<br>**- Downloads**<br>**- Phone**<br>**- Address**<br>**- Additional Description**<br>**- Social URL**<br>**- Custom Social URL 1 - 5** | Native | **- Creative UI > Create New**<br>**- Creative UI > Edit**<br>**- Native Assembly > Create New**<br>**- Native Assembly > Edit** | 32,000 |
| **Segment Pixel (Name)** | VAST (video, audio) | - **Creative Manager** <br> - **Creative UI** > **Create New** <br> - **Creative UI** > **Edit** | 64 |

## Related topics

- [Creative Guidelines and Specifications](creative-guidelines-and-specifications.md)
- [Add a Creative](add-a-creative.md)
- [Add Creatives in Bulk](add-creatives-in-bulk.md)
