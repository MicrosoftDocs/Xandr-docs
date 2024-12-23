---
title: Mobile App Lists
description: Use the Bidder UI to manage mobile app bundle ID lists for targeting or blocking app traffic using unique app identifiers from app stores.
ms.date: 10/28/2023
---

# Mobile App Lists

## Mobile app instance Bundle ID targeting

Mobile app instance bundle ID targeting is now available in the Bidder UI. These are lists that are created, managed, and targeted by the bidder. This functionality allows you to select the mobile app lists you want, or do not want.

A bundle ID is a string of characters that advertisers and ad platforms use to identify specific mobile apps, based on the operating system of the device. This is generally the application’s unique identifier on their relevant app stores. The mobile app bundle ID targeting alpha allows third-party bidders to target or block app traffic using app store domains and bundle IDs. Users can now log in to the Bidder UI or use the API to add, edit, or delete blocklists and allowlists using mobile app bundle IDs.

## Creating, Editing, and Deleting an App Bundle List

Follow these steps to add, manage, or delete an app bundle list using the UI:

1. Navigate to the **[Bidder UI](https://bidder.xandr.com/)**.
1. Select the **Bidder settings** tab.
1. Scroll down to the **App bundle lists** section.

:::image type="content" source="media/bidder-wide-settings.png" alt-text="Screenshot that explains the Bidder settings.":::

:::image type="content" source="media/app-bundle-list.png" alt-text="Screenshot that explains the Bidder settings.":::

Once you have located the **App Bundle Lists** section, you can use the navigation controls to edit, delete, view, or add a new app bundle list:

:::image type="content" source="media/test-bidder-bundle-list2.png" alt-text="Screenshot that explains the Bidder bundle list.":::!

To block or allow a specific app bundle list, go to the Profiles tab, select the bidder profile you want to edit, and scroll to the App bundle list dropdown. From the dropdown, select the bundle list you want to block or target.

:::image type="content" source="media/new-bidder-profile.png" alt-text="Screenshot that explains the Bidder profile.":::

### Bulk upload or edit bundle lists

Currently, bulk editing functionality is not available in the Bidder UI but can be done through the API. Below are sample API calls for creating a new list and updating an existing list.

### Create a new bundle list

To create a new bundle list, use the following `POST` request.  

> [!NOTE]
> You must specify the `bidder_id`.

```
POST -- https://api.adnxs.com/app-bundle-list?bidder_id=129 , 
{
    "app-bundle-list": {
        "bidder_id": 129,
        "name": "Mem List 2",
        "description": "Not another bundle list",
        "bundles": [
            "item1", "item2"
        ]
    }
}

```

### Edit an existing bundle list

To edit an existing bundle list, use the following PUT request.

```
{
PUT -- https://api.adnxs.com/app-bundle-list/22  (22 is the ID)
    "app-bundle-list": {
  "id": 22,
  "bidder_id": 129,
        "name": "Test Bidder Bundle List 2",
        "description": "Not another bundle list",
        "bundles": [
            "com.test.com", "memcache.8", "memcache.9"
        ]
    }
}

```

### FAQ

**Can I target a mobile app and a domain app at the same time?**

Yes, this is technically possible. However, mobile app bundle lists and domain lists have an AND relationship. If you are already targeting a domain list, create a separate profile to target the app list.

## Related topics

- [Bidder Platform User Interface](bidder-platform-user-interface.md)
- [Domain List](domain-list.md)
- [Profiles Screen](profiles-screen.md)
- [Creating a New Bidder Profile](creating-a-new-bidder-profile.md)
- [Editing a Bidder Profile](editing-a-bidder-profile.md)
- [Additional Functions](additional-functions.md)
- [Bidder Profile Targeting Options](bidder-profile-targeting-options.md)
- [Countries](countries.md)
- [Ad Types](ad-types.md)
- [Supply Types](supply-types.md)
- [Exchanges and Members](exchanges-and-members.md)
- [Unknown Users](unknown-users.md)
- [Sensitive Attributes](sensitive-attributes.md)
