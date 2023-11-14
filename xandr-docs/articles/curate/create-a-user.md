---
title: Create a User
description: The article describes how You can create users and assign them to various roles. 
---

# Create a user

You can create users and assign them to various roles. Each role gives the user a different level of access to your account. For each user you can personalize the formats used for decimals and large numbers. This page walks you through the process.

## Create a network user

Network users have access to various areas and functionality of your Network based on the roles and permissions you specify. Only users with the **User Manager** role can create a Network User.

## User details

### Getting there

You add network users in the **Network** section of Invest DSP.. Click on your Member name in the top right of the navigation menu and select **Member Users**. This brings up the **Member Users** screen. Click the **+ New** button to open the **Create User** dialog.

### Enter contact information

From the **User Details** tab, enter the user's **Contact Information**.

> [!NOTE]
> The email ID enetered here will be the primary username for signing into the Xandr products via the Microsoft Identity Platform. Ensure the email is consistent across any accounts in the Xandr platform, and matches the user's email for authenticating to Microsoft products. For more details, visit [Microsoft Identity Platform Login](microsoft-identity-platform-login.md).
> [!NOTE]
> If the State is set to Inactive, the user will not be able to log in.

### Select numerical formatting

Within the **Contact Information** section you'll also find options for numeric formatting. From the **Reporting Decimal Format** and **Numerical Format** dropdowns, select the formats that are conventional in the user's geographical location. Numbers throughout Curate will be displayed in the format chosen here for this user.

- **Reporting Decimal Format** - Select whether a **Point** or Comma should be used for decimals when viewing numbers in reports.
  
> [!NOTE]
> When the Comma format is selected, users will not be able to export a report using CSV format.

- **Numerical Format** - Select the thousand separator and decimal mark for numbers everywhere in Curate except in reporting. This setting controls both how numbers appear to the user as well as how numbers can be entered by the user.

### Provide API username and app permissions

- **Login Credentials**: Enter a username. The username should not contain any special characters such as $, \#, and ". This will be the
  username the user can use to sign into the Xandr API. For accessing the Xandr Digital Platform UI products, the user's email will be used via the Microsoft Identity Platform to authenticate.
- **Permissions**: If this user needs to view billing information in Curate, select the **Admin User** check box.

## Roles & permissions

On the **Roles & Permission** tab, select the user role with the appropriate access rights for this particular
user.

> [!NOTE]
> Once the user has been created, you will not be able to change the user's role. To grant someone a different level of access to Curate, you will have to create a new user.

Check the **User must have peer approval to activate campaigns** checkbox if you want to require approval from another user on the network before this user's campaigns can be set to Active. This feature minimizes the risk of user-side errors in campaign activation and can help users identify and change settings to improve campaign performance.

> [!NOTE]
> The peer approval feature sets requirements for who must obtain approval, but not who has the ability to approve. Any other user who is able to create campaigns for your network can provide this approval. There is no way to designate a single approver of others' campaigns.

## Create an advertiser user

You can create users for advertisers that want to run reports for themselves. Only users with the **User Manager** and/or **Network Advertiser Manager** role can create an Advertiser User. Note that this is not the same as the Curate Advertiser Manager user: an advertiser user does not see data about any other advertisers and does not have editing capabilities. The following steps walk you
through the creation process.

1. Click on your member name in the top right of the navigation menu and select **Advertiser Users**.
1. On the **Advertiser Users** screen, click **Add User**. This opens the **Create New User** dialog.
1. In the **Contact Information** section, enter the user's information. Also, select whether a point or comma should be used for decimals in the reports received by this user. The user State defaults to **Active**. Setting the state to **Inactive** will prevent the user from logging in. 
1. In the **Login Credentials** section, enter the username that the user will use to log in to Curate. The username should not contain any special characters such as $, \#, and ". The username and password will be sent to the email address entered in the **Contact Information** section.
1. To finish creating the new advertiser user, click **Save**. The user is then added to the list of advertiser users.
