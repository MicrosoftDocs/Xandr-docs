---
title: Microsoft Monetize - Working with Segments
description: Explore segment pixels capturing user data (webpages, actions, gender, location) for segment assignment. Reduce character count.
ms.date: 10/28/2023
---

# Microsoft Monetize - Working with segments

Segment pixels use information about a user, such as webpages they visit, actions they take, or qualities such as gender, location, and wealth, to assign that user to a group called a segment. Segment data is written to and extracted from the server-side cookie store via segment pixels.

If you're new to the concept of pixels, we recommend you read a little more about Cookies, which are text files associated with specific domains that live in your browser and contain information such
as how many times you have been served a particular ad by the domain adserver.com, or what's in your shopping cart from myfavoritestore.com.

Microsoft Advertising segment pixels look something like this:

```
https://ib.adnxs.com/seg?add=1,2,4
```

where 1, 2, 4 are Microsoft Advertising segment IDs.

For example, let's say ProStarr Sportswear wants to target users that have purchased from their online store in the past. They can put a segment pixel on their checkout page. When a user checks out, the pixel fires and "Segment 123" is written into the server-side cookie store. When the user visits some other page, say mysite.com, the cookie is read, and ProStarr knows that this user is in Segment 123.

To remove users from a segment, use this syntax:

```
https://ib.adnxs.com/seg?remove=1,2,4
```

These segment pixel calls to `/seg` will always return a 1x1 invisible GIF, unless a piggyback pixel redirect parameter is
included. (To learn more about redirect parameters, see [Segment Pixels: Advanced](segment-pixels-advanced.md).)

## Network- vs. Advertiser-level segments

Networks can create segment pixels that are attached to a specific advertiser, or they can create network-wide
segment pixels that are available for targeting to all the network's advertisers. An advertiser-level segment is only available to that advertiser's campaigns. You can move a segment from advertiser-level to Network-level by changing the `advertiser_id` to `null` via the API.

## Server side cookie storage

We store all cookie data server side in our [Server Side Cookie Store](server-side-cookie-store.md). This way it is accessible for all impressions. Soon we will enable access to our customers cookie store data at any time, outside of
ad calls. Customers can also traffic in offline user data to our cookie store so that it can be usable during ad calls. Please see [Pass in User Data Offline](pass-in-user-data-offline.md) for details.

## Segment load reporting

These metrics are associated with each segment over the selected time period. You can change the time period using the dropdown menu.

In addition to "standard" segments, QuickStats are also available for the following segment types:

- Segments shared with other members.
- Segments uploaded via the API's [Batch Segment Service](../digital-platform-api/batch-segment-service.md).

| Metric | Description |
|---|---|
| **Name** | This is the segment name. |
| **ID** | This is the segment Microsoft Advertising ID. |
| **Data Provider** | This is the data provider name. |
| **Price** | This column displays the price a buyer has paid for a segment. It allows the buyer to toggle between these two options:<br> - CPM (default)<br> - % Media Cost |
| **Active Users** | This is the count of active users in a segment over a 24-hour period. |
| **Daily Loads** | The average number of times a user is added to a segment. (This is also known as 'segment fires'.)<br>This allows you to see growth and reduction of segments. |

> [!NOTE]
> The contextual segments (from contextual or real-time data providers) will not show loads in this report. This is because contextual segments do not actually involve a pixel being fired. Instead, they are added to an impression in real time.

## Max usersync pixels

You can set a maximum number of [user syncs](user-id-syncing-with-external-partners.md) that can happen on your segment pixel. If you are using multiple pixels in a single call (for example, to add a user to 2 segments in a single pixel call), the LOWEST max usersync pixel value will be honored.

## Related topics

- [Segment Pixels: Advanced](segment-pixels-advanced.md): More advanced manipulation of segment pixels
- [Segment Targeting](segment-targeting.md): Targeting the segments that you have created through pixels
- [User ID Syncing with External Partners](user-id-syncing-with-external-partners.md): User ID syncing between
  Microsoft Advertising and its platform partners
- [Create a Segment Pixel](create-a-segment-pixel.md)
