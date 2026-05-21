---
title: Microsoft Monetize - Peer Approval
description: In this article, find information about the peer approval feature and the workflow of line items that require peer approval.
ms.date: 10/21/2025
ms.service: publisher-monetization
ms.subservice: microsoft-monetize
ms.author: shsrinivasan
---

# Microsoft Monetize - Peer approval

Peer Approval provides a way for you to ensure that augmented line items are reviewed and approved by a second user before they can be set to active. This allows you to catch any possible setup errors before the line item starts spending.

> [!IMPORTANT]
> The Peer Approval feature is not activated for all clients. If you want to have your account enabled for the Peer Approval feature, contact your account representative.

## User settings

To designate that a user must receive approval for any line items they create before they can set them to Active, select the **User must have peer approval** checkbox on the user's account. This will cause an **Approval Status** field to appear on all line items they create.

## Line item creation workflow

For all line items created by a user who is required to request peer approval, the **Approval Status** field will initially be set to **Pending**. The line item's **State** field can not be set to **Active** until the **Approval Status** field is set to **Approved**.

Line items with **Approval Status** set to **Pending** must be reviewed by a user other than the creator of the line item. Once reviewed, the line item can either be **Rejected** (with comments explaining what corrections need to be made) or **Approved**.

- If the line item's **Approval Status** is set to **Rejected**, the changes suggested by the Approver must be made and saved. The line item's **Approval Status** will be reset to **Pending**.
- If the line item's **Approval Status** is set to **Approved**, the line item's **Status** field can be set to **Active**.

| Line Item status | Approval Status | Next action required | Who can perform the action |
|---|---|---|---|
| Inactive | Pending | Line item must be reviewed and marked as Rejected or Approved. | Any user (with line item edit permissions) who did not create the line item |
| Inactive | Approved | The line item **Status** field can be set to **Active**. | Any user (with line item edit permissions) |
| Inactive | Rejected | The line item must be corrected to address the reasons for rejection. Once these changes are made and saved, the **Approval Status** will be reset to **Pending**. | Any user (with line item edit permissions) |
| Inactive | Not Required | No review of the line item is needed because the user who created it does not have the **Approval Status** checkbox selected in their user profile. The line item **Status** field can be set to **Active** at any time. | N/A |
