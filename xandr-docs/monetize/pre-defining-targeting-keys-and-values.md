---
title: Pre-Defining Targeting Keys and Values
description: In this article, find information about how to create and manage keys and values along with the key/value requirements.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Pre-defining targeting keys and values

One way to target an advertising campaign is by utilizing key/value sets based on information provided by publishers. There are many ways to target line items and campaigns based on various standard demographics. Publishers can also define custom sets of targeting criteria based on their own user information. By creating custom keys and corresponding values, publishers can enable advertisers to more narrowly target their users. In order for advertisers to target on these key/values sets, the publisher must first set up the keys and values that can be targeted.

## Key/Value overview

Keys are the categories that are used to create targets. Examples of keys are *city*, *sport*, or *car*. Values are the specific attributes within those categories that you want to target. Examples of values for *city* are *New York*, *London*, and *Tokyo*. Values for sport could include *football*, *rugby*, and *tennis*. Creating these key/value sets would allow advertisers to target, for example, all users in New York or London who play tennis.

## Key/Value management

Select **Key Values** from the **Network** menu to open the **Key/Value Management** window. From here you can view all the currently-defined keys, as well as activate and deactivate keys.

You can also create new keys, edit existing keys, and add and remove values to and from keys.

### Create a targeting key

To create a new key, click **+New**. This will open the **New Key/Value** window. Enter the following information:

- **Key Type** (required): This is the data type for the values associated with the key. All values for a key must be the same type. If you want to target using logical expressions such as greater than, less than, or between, use a **Numeric** key type. For example, if you create a key for age and use a Numeric key type, advertisers will be able to target on age > 21.
- **Key Name** (required): The name must be unique, including keys that have been deactivated. Keys cannot contain spaces and can be up to 20 character in length. See [Key/Value Requirements](#keyvalue-requirements) for other restrictions on key names.
- **Key Label** (optional): The label provides a descriptive name for the key. While the label is not required, it can be helpful for reporting and operations. It must be unique and can be a maximum of 190 characters. The label can contain spaces. You can edit the label at any time after the key has been created.

After you define your key, click **Save**. This will save the key and change the **New Key/Value** window to **Edit Key/Value**, which allows for editing of the key label and enables the **Values** section of the window.

### Update a targeting key

In the **Key/Value Management** window, hover over the key you want to update. Click on the pencil icon to open the **Edit Key/Value** window.

You can update both the key name and the label. You can also update all the key's associated values from the **Edit Key/Value** window.

If you update the key name, this update won't be reflected in any campaigns that are already using that key in their targeting. Any new targeting that is set up will show the new key name.

> [!NOTE]
> You cannot delete keys from the **Key/Value Management** window. If you have a key you no longer want advertisers to use for targeting, click the box next to the key and select **Deactivate** from the **Action** menu. You can re-activate the key at any time.

### Activate/Deactivate a key

When you create a new key, by default the key is active. A key that is active can be used in targeting and will appear in the **Key/Value Targeting** dialog when advertisers set their targeting options on line items or campaigns.

If you have a key that you do not want to be used in targeting, you must deactivate the key:

1. In the **Key/Value Management** window, click the check box next to the key you want to deactivate.
1. From the **Action** dropdown, select **Deactivate**.

When you deactivate a key, it will not be displayed for key/value targeting on a line item or campaign. However, if the key has already been used to target a line item or campaign, that targeting will remain in place. For example, let's say you create a key named *fruit*. An advertiser then targets their campaign on users who eat a *fruit* of *apple* or *orange*. If you then deactivate *fruit*, that campaign will continue to target *fruit = apple* or *orange*. If the advertiser removes that target from the campaign, they will not be able to re-add it until *fruit* is activated.

You can re-activate a key at any time by selecting the key and choosing **Activate** from the **Action** dropdown.

### Delete a key

We recommend that you deactivate keys rather than deleting them as deleting a key cannot be undone. If you deactivate a key, you can activate it again at any time.

If you do need to delete a key, follow these steps:

1. In the **Key/Value Management**  window, click the check box next to the key you want to delete.
1. From the **Action** dropdown, select **Delete**.

## Entering values

There are two ways to enter values: you can type them in or import them. Values can be up to 100 characters. See [Key/Value Requirements](#keyvalue-requirements) for more information on naming.

### Type individual values

You can enter individual values to target with the key. Simply type the values you want to target for that key in the **Values** text box, one value per line. If you want to include a label with the value, type the value name followed by a comma, followed by the label. For example:

```
Seattle, Space Needle 
```

When you've typed in your values, click **Add Values** to save them. The **Values** text box will clear and the values will move to the list of saved values at the bottom of the window.

### Import values

If you're targeting your key on a large number of values, you can bulk import them from a CSV (comma-separated values) file. Click **Import values from .csv** to open a file dialog you can use to navigate to and select your file. Your CSV file can **not** contain comma-separated values. The application will look for files with a `.csv` extension, but the file you import must be a plain-text file containing one value per line. For example, if your key is **city**, you might want to import a file that looks like this:

```
London
Paris
New York
San Francisco
Denver
```

You can include commas in your CSV file, but only to separate values from value labels. If you want to import labels with your values, your file will look something like this:

```
London, Big Ben
Paris, Eiffel Tower
New York, Big Apple
San Francisco, Golden Gate
Denver, Mile High
```

### Maximum values

You can add a maximum of 999 values to a single key. To add more values to a given key, you can combine keys with the same name with `or` expressions, as shown here:

:::image type="content" source="media/combine-key-values.png" alt-text="Screenshot that shows how to combine multiple values for a given key.":::

### Updating values

Values you type in or import (or that were added through the API) will appear at the bottom of the **Edit Key/Value** window. To edit a value, hover over the value name to reveal text boxes around the value and label. Click in the text box for the value or label you want to update and type in the new name. When you're done, click the **Save** button for that value.

> [!TIP]
> You can also use keyboard commands to edit values. Within a value, you can tab to go from one field to the next. To save a value you can either tab to the **Save** button and press the spacebar, or you can press **Enter** while your cursor is in the **Value Name** or **Value label** text box.

You can also delete values. Click the checkbox next to the value name to reveal a **Delete** button at the top of the values list. Click **Delete**.

> [!WARNING]
> Deleting a value cannot be undone. However, you can easily reenter values by typing them in the **Values** text box and adding them again.

If you delete a value that is currently being targeted in a campaign, the campaign will continue to target on that value. For any new targeting that is created, the value won't be displayed in the list of pre-defined values for this key.

## Key/Value requirements

The following restrictions are enforced when entering or importing values.

### Number of keys/values

- You can have up to 500 active keys at one time.
- You can have up to 100,000 pre-defined values per key.
- You can have up to 2,500,000 total pre-defined values at one time.

### Key/value naming

- Key and value names are not case-sensitive. All keys and values will be converted to lower-case.
- Key names cannot begin with `kw_`, because the tag URL query-strings must contain kw_key=value (with the kw_ prefix) for the key-value pair to be eligible/identified in auctions.
- Maximum key length is 50 characters.
- Maximum value name length is 100 characters.
- Key names cannot contain spaces.
- Value names may contain whitespace, so they can be more than one word.
- Key and value names cannot contain any of the following special characters:
  - `"` (double quotes)
  - `'` (apostrophe)
  - `=` (equal sign)
  - `!` (exclamation point)
  - `+` (plus sign)
  - `#` (hashtag)
  - `*` (asterisk)
  - `~` (tilde)
  - `;` (semicolon)
  - `^` (caret)
  - `()` (parentheses)
  - `< >` (angle brackets)
  - `[ ]` (square brackets)
  - `,` (comma)
  - `&` (ampersand)
  - `@` (at)
  - `:` (colon)
  - `?` (question mark)
  - `%` (percent)
  - `/` (forward slash)

<!--## Related topic

[Key/Value Targeting](key-value-targeting.md)-->
