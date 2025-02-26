---
title: Video Content Targeting
description: When a publisher is integrated with video taxonomy, video content can be targeted on a deal. You can target video inventory based on criteria such as the network on which the content is shown, the genre of the content, content duration, the type of program, and delivery type.  
ms.date: 10/28/2023
---

# Video content targeting

For publishers that have adopted video taxonomy and provide Microsoft Advertising with information about the content where ads reside, Deal line items can target video inventory based on criteria such as the network on which the content is shown, the genre of the content, content duration, the type of program, and delivery type (live or Video on Demand).

> [!NOTE]
> Video content targeting requires content metadata integration. Please contact your Microsoft account manager for enablement. If you are not integrated with video content metadata, values passed in content object fields will not be transmitted to DSP partners.

If a publisher is integrated with video taxonomy, video content can now be precisely targeted on a deal. Targeting is based on available detail about the specific video content, including the network on which it is shown, the type of programming, the subject matter, the scheduled airtime, and more. In order for Video Content data to be targetable based on this information, the publisher must set up a Video Taxonomy implementation with Microsoft Advertising. If you're a video publisher and would like to implement this functionality, please contact your account manager.

If you're a deal curator, you can set up curated deals targeting these settings. However, before the data is targetable, sellers you plan to include must first integrate with Microsoft Advertising video taxonomy. If you target this data without ensuring that a contributing seller will provide matching data, you will not see any delivery on the deal. The best practice for curators is to work directly with sellers that have already integrated video taxonomy.

The following categories of information can be targeted using Video Content targeting:

| Category | Description | Targetable Values |
|--|--|--|
| Video Content Duration | The length of the content | - Long-form (greater than or equal to 8 minutes)<br> - Short-form (less than 8 minutes) |
| Video Content Genre | The genre of the program during which the ad will play | Genre categories such as Cooking, Horror, News, or Football. |
| Video Content Network | The network on which the content is shown | - Network names, such as Fox, BBC, Discovery. |
| Video Content Rating | The publisher-identified audience group for which the content is rated. | - All<br> - Children<br> - Teens<br> - Young adults<br> - Adults |
| Video Delivery Type | The type of streaming content delivery | Live, Video on Demand (VOD) |
| Video Program Type | The format of the program during which the ad will play | - Clip<br> - Event<br>- Movie<br> - Series<br> - Show<br> - Special |
