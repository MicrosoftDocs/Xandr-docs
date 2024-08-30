---
title: Create a Placement Group
description: In this article, find information on how to create and set up a placement group.
ms.date: 10/28/2023
---

# Create a placement group

Publishers create placement groups to organize and maintain placements. Values and settings assigned to a placement group apply to all placements in that group. Each placement must be associated with a placement group, but no placement can be associated to multiple groups.

## Step 1. Start a new placement group

- **From the Publishers tab**:

    Select **Inventory Manager**, then select the publisher you want to work with from the **Select Publisher** dialog. Select **Create New** > **Placement Group** from the dropdown menu. The **Create New Placement Group** dialog will appear.

- **From the Inventory tab**:

    Select **Placements**, then select the publisher you want to work with from the **Select a Publisher** dialog. You can also select **Inventory** from the main navigation window, find the publisher you want to work with, then click the button under **Placements** for that publisher. Both of these actions will open the **Inventory Manager**. Select **Create New** > **Placement Group** from the dropdown menu. The **Create New Placement Group** dialog will appear.

## Step 2. Define the placement group details

In the **Create New Placement Group** dialog on the **Placement Group Details** tab, complete the following fields:

- **Name**: Enter the name you want to use for the placement group.
- **Code**: Enter a code that you can use for organizational or reference information. This is not shared with buyers. This option is available only if you select the **Code (Advanced)** setting in this section.
- **Domain**: Enter the top level domain name. This is not shared with buyers. This setting is optional.

You must also select the appropriate **Supply Type** from the dropdown:

- **Standard Website**: Select this option if the available inventory is part of a display website.
- **Mobile Optimized Website**: Select this option if the available inventory is part of a website that has been created specifically for viewing on a mobile device.
- **Mobile Application**: Select this option if the available inventory is part of a mobile app.

> [!NOTE]
> Only traffic matching the placement group's supply type can serve within that placement group.
>
> For example, if a seller labels their placement group as **Standard Website** but the traffic coming through that placement group is both standard website as well as mobile optimized, any campaign targeting **Mobile Application** placement groups will not be able to serve on this inventory.

## Step 3. Select your marketplace settings

You can designate the Microsoft Advertising Marketplaces in which you want the inventory associated with this placement group to be available.

### RTB marketplace

- To designate that all inventory associated with this placement group's placements is to be resold within the RTB Marketplace, select **Participate** under the **RTB Marketplace** section. This inventory will then be available to third-party buyers (as well as direct buyers). This is the default setting for all newly created placement groups.
- To designate that all inventory associated with this placement group's placements is only available to direct demand, select **Do not participate** under the **RTB Marketplace** section. No inventory associated with this placement group's placements will be resold.
- If you select **Do not participate** and also **Allow Deal demand for this placement group**, this will only allow buyers to access the placement group via deals.

## Step 4. Apply universal categories to the placement group

On the **Content Categories** tab, you can apply Microsoft Advertising universal categories for a specific placement group, making it attractive to buyers who have targeted these categories in their campaigns. You must choose one of the following options:

- **Categorize as mixed/unknown**: Select this option to leave all category settings unselected. Buyers will not be able to specifically target this placement group.

- **Include selected universal categories**: Select this option to select the categories that you want to assign to the placement group. Numerous choices appear in the **Available Universal Categories** field when this option is chosen.

  You can choose any category in the **Available Universal Categories** field and select the associated **Add** option to move it to the **Selected Universal Categories** field. Categories in this field are applied to the placement group (and subsequently to all placements within the placement groups). You can also enter a term in the search field to limit the number of available choices.

> [!NOTE]
> The targeting categories you see when these tabs are first exposed are the top-level categories. The number of sub-categories associated to each is shown in parentheses (e.g., **Finance (8)**). You can click on the **Add** link to apply the entire top-level category, or you can click on the category name to see all of the sub-categories to which it is associated. From there, you can apply the individual sub-categories.

## Step 5. Apply custom categories to the placement group

On the **Content Categories** tab, you can apply custom categories (i.e., ones that you have defined yourself) to a placement groups. Buyers who have a managed relationship with you can target these categories through their campaigns. You must choose one of the following options:

- **Don't apply custom categories**: Select this option to leave all category settings unselected. Buyers will not be able to specifically target this placement group.

- **Include selected custom categories**: Select this option to select the categories that you want to assign to the placement group.

  You can choose any category in the **Available Custom Categories** field and select the associated **Add** option to move it to the **Selected Custom Categories** field. Categories in this field are applied to the placement group. You can also enter a term in the search field to limit the number of available choices.

> [!NOTE]
> Buyers with whom you have a managed relationship can view this inventory. You can expose this inventory to buyers with whom you do not have a managed relationship can find this inventory in **Network**, on **Third-Party Inventory**, under **Network Resold**.

You can add new custom categories from here as well. In the **New custom category** field, enter the name of the new category and click **Create**. The new category is listed in the **Available Custom Categories** field.

## Step 6. Self-audit the placement group

On the **Self-Auditing Criteria** tab, determine where and how placement group auditing will occur.

> [!TIP]
> We recommend that all publishers self-audit their inventory to make it available to more buyers.

You must select one of the two options:

- **Do not self-audit this placement group**: Select this option to allow auditing at the placement level. This enables you to use different auditing criteria for each placement.
- **Self-audit this placement group**: Select this option to perform auditing at the placement group level, meaning that all placements under this placement group will use the same auditing criteria. When you select this option, the **Sensitivity Audit** and **Self-Audit Confirmation** sections appear.

The **Sensitivity Audit** section allows you to notate any attributes of the placement group that may exist and to determine the intended audience for the placement group. This allows buyers to make more educated decisions about whether they want to purchase inventory in this placement group. There are three categories in this section:

### Sensitive attributes

If this placement group has sensitive attributes, you must select **This placement group has the following sensitive attributes** at the top of the list. If there are no sensitive attributes to apply, you must check **No Sensitive Attributes apply** at the bottom of the list.

If you indicate that there are sensitive attributes, you must choose at least one of the options in the list. Conversely, you cannot specify that there are no sensitive attributes and then click the checkbox for an attribute.

### Intended audience

You must select one of the following audience types:

- General audience
- Children
- Young adults
- Ages 16 and up

> [!NOTE]
> The exact age ranges of these audience types can be defined through the [Profile Service](../digital-platform-api/profile-service.md).

### Always banned

You cannot select these options (they are for informational purposes only). Placements that contain any of these topics are banned on this placement group.

## Step 7. Confirm your self-audit

You must check the **checkbox** in this section to confirm that you have done the following:

- Self-audited this placement group to comply with the Microsoft Advertising content standards
- Set the appropriate sensitive attributes
- Noted the intended audience

> [!NOTE]
> The **View the Microsoft Advertising content standards** link provides detailed information about the standards that platform content must meet. You can click the link from the **Self-audit Criteria** tab.

## Step 8. Save the placement group

To finish adding the placement group to the Microsoft Advertising platform, click the **Save** button. Alternately, if you want to save the placement group and immediately create a new placement under it, click the **Save and Add New Placement** button.
