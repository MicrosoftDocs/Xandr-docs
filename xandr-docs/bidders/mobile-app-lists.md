---
title: Mobile App Lists
description: Use the Bidder UI to manage mobile app bundle ID lists for targeting or blocking app traffic using unique app identifiers from app stores.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: bidder
ms.author: shsrinivasan
---

# Mobile app lists

## Mobile app instance bundle ID targeting

Mobile app instance bundle ID targeting is now available in the Bidder UI. Users can create, manage, and target these lists through the Bidder platform. This feature enables advertisers to include or exclude specific mobile app lists.

A bundle ID is a string of characters that advertisers and ad platforms use to identify specific mobile apps, based on the operating system of the device. This is generally the application’s unique identifier on their relevant app stores. The mobile app bundle ID targeting alpha allows third-party bidders to target or block app traffic using app store domains and bundle IDs. Users can now sign in to the Bidder UI or use the API to add, edit, or delete blocklists and allowlists using mobile app bundle IDs.

## Create, edit, and delete an app bundle list

To add, manage, or delete an app bundle list in the UI:

1. Navigate to the **[Bidder UI](https://bidder.xandr.com/)**.
1. Select the **Bidder Settings** tab.
1. Scroll down to the **app bundle lists** section.

:::image type="content" source="media/bidder-settings.png" alt-text="Screenshot explaining the Bidder Settings tab.":::

:::image type="content" source="media/app-bundle-lists.png" alt-text="Screenshot that explains the app bundle list.":::

Once you have located the **App bundle lists** section, you can use the navigation controls to edit, delete, view, or add a new app bundle list:

:::image type="content" source="media/test-bidder-bundle-lists.png" alt-text="Screenshot that explains the Bidder Bundle list.":::

To block or target an app bundle list:

1. Go to the **Profiles** tab.
1. Select the bidder profile to edit.
1. Scroll to the **App bundle list** dropdown.
1. From the dropdown, select the bundle list to block or target.

:::image type="content" source="media/new-bidder-profiles.png" alt-text="Screenshot that explains the Bidder profile.":::

### Bulk upload or edit bundle lists

Currently, bulk editing functionality is not available in the Bidder UI but can be done through the API.
Below are sample API calls for creating a new list and updating an existing list.

### Create a new bundle list

Use the `POST` method to create a new app bundle list. The `bidder_id` must be included as a query parameter in the URL.

> [!NOTE]
> You must specify the `bidder_id`.

```
POST -- https://api.adnxs.com/app-bundle-list?bidder_id=129 
{
    "app-bundle-list": {
        "bidder_id": 129,
        "name": "Mem List 2",
        "description": "Not another bundle list",
        "bundles": [
            "item1",
            "item2"
        ]
    }
}

```

### Edit an existing bundle list

Use the `PUT` method to update an existing app bundle list. The `id` in the URL corresponds to the app bundle list you want to modify.

```

PUT https://api.adnxs.com/app-bundle-list/22

{
    "app-bundle-list": {
        "id": 22,
        "bidder_id": 129,
        "name": "Test Bidder Bundle List 2",
        "description": "Not another bundle list",
        "bundles": [
            "com.test.com",
            "memcache.8",
            "memcache.9"
        ]
    }
}


```

### FAQ

**Can I target both a mobile app list and a domain list simultaneously in the same bidder profile?**

While this is technically possible, please note that mobile app bundle lists and domain lists have an **AND** relationship. For example, if an app list and a domain list are both positively targeted (action = include) in the same profile, **both conditions**  must be true for a request to pass.

However, because requests typically originate from either mobile or web (not both), a single request rarely satisfies **both conditions**. Therefore, if you are targeting a domain list, we recommend creating a separate profile to target the app list.

## Related topics

- [Bidder Platform User Interface](bidder-platform-user-interface.md)
- [Domain Lists](domain-lists.md)
- [Profiles Screen](profiles-screen.md)
- [Creating a New Bidder Profile](creating-a-new-bidder-profile.md)
- [Editing a Bidder Profile](editing-a-bidder-profile.md)
- [Additional Functions](additional-functions.md)
- [Bidder Profile Targeting Options](bidder-profile-targeting-options.md)
- [Countries](countries.md)
- [Ad Types](ad-types.md)
- [Exchanges and Members](exchanges-and-members.md)
- [Unknown Users](unknown-users.md)
- [Sensitive Attributes](sensitive-attributes.md)
