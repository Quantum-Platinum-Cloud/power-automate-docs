---
title: Manage desktop flows
description: Learn how to manage desktop flows in the Power Automate portal.
author: georgiostrantzas
ms.subservice: desktop-flow
ms.topic: conceptual
ms.date: 01/17/2023
ms.author: marleon
ms.reviewer: gtrantzas
contributor:
search.audienceType: 
  - flowmaker
  - enduser
---

# Manage desktop flows

After creating desktop flows, you might need to view, edit, or check their status. To achieve all these tasks, go to **My flows** > **Desktop flows** in the Power Automate portal.

## See a list with desktop flows

1. Sign in to the [Power Automate portal](https://powerautomate.microsoft.com).

1. Go to **My flows** > **Desktop flows**.

   Using the available options in this tab, you can create new desktop flows and edit or delete existing desktop flows.

   :::image type="content" source="media/manage-desktop-flows/view-all.png" alt-text="Screenshot of the list with all desktop flows.":::

> [!NOTE]
> If you delete or rename a desktop flow, select the refresh button to reflect the changes in the desktop flows list.

## See details of desktop flows

For each of your desktop flows, you can see its details by selecting its name from the list of desktop flows. You can see various details including:

- The run history with details of each run.
- The applications or websites used in the desktop flow.

Follow these steps to see the details for a desktop flow:

1. Sign in to the [Power Automate portal](https://powerautomate.microsoft.com).
1. Go to **My flows** > **Desktop flows**.
1. Select any of your desktop flows.

:::image type="content" source="media/manage-desktop-flows/view-details.png" alt-text="Screenshot of the details of a desktop flow.":::

## Share desktop flows

You can share a desktop flow with other users in your organization, giving those users specific permissions to access your flows.

Follow these steps to share a desktop flow:

1. Sign in to the [Power Automate portal](https://powerautomate.microsoft.com).
1. Go to **My flows** > **Desktop flows**.
1. Select the desktop flow you want to share, and then **Share**.
1. Select **Add people**, and then enter the name of the person in your organization with whom you'd like to share the desktop flow.
1. Select the user and then select either **User** or **Co-owner** as the permission for the person with whom you share the flow.

    - **Co-owner**: This access level gives the co-owner full permissions to the desktop flow. They can edit, share, and delete the desktop flow.
    - **User**: This access level gives permission to only use that desktop flow in a cloud flow. No edit, rename, delete or share permissions are possible with this access. Alternatively, those users can create a copy of the desktop flow using the **Save as** option, and work independently.

1. Select **Save**.

   :::image type="content" source="media/manage-desktop-flows/sharing-ux.png" alt-text="Screenshot of the Share button.":::

> [!NOTE]
>
> Once a desktop flow has been shared, owners and co-owners can change the access of each user by selecting **Manage access** on the desktop flow details page.
> If someone shares a desktop flow with you, select the refresh button to see it in the **Shared with me** flows list.

## Reassign desktop flows

To reassign a desktop flow to another user:

1. Sign in to the [Power Automate portal](https://powerautomate.microsoft.com).
1. Go to **Data** > **Tables**.
1. Go to the **All** tab, and then search for the **Process** table.

    :::image type="content" source="media/manage-desktop-flows/manage-desktop-flows-process-table.png" alt-text="Screenshot of the Process table in the All tab":::

1. Select **Edit**.
1. Select your desktop flow in the list, and then select **Edit row using form**.

    :::image type="content" source="media/manage-desktop-flows/manage-desktop-flows-edit-row-using-form.png" alt-text="Screenshot of the Edit row using form button.":::

1. Select **Assign**, and then confirm the changes.

## Copy desktop flows

To duplicate an existing desktop flow:

1. Sign in to the [Power Automate portal](https://powerautomate.microsoft.com).
1. Go to **My flows** > **Desktop flows**.
1. Select the flow you want to copy.
1. Select **Save As**.

    :::image type="content" source="media/manage-desktop-flows/manage-desktop-flows-copy.png" alt-text="Screenshot of the Save As button.":::

1. Enter a name for the new desktop flow.
1. Select **Save**.

   :::image type="content" source="media/manage-desktop-flows/create-copy-of-this-flow.png" alt-text="Screenshot of the field to enter the name of the new desktop flow.":::

## Manage desktop flows access

For each of your desktop flows, you can manage its access by selecting **Manage access** in the desktop flows details page.

:::image type="content" source="media/manage-desktop-flows/manage-access.png" alt-text="Screenshot of the Manage access option.":::

In this page, you can:

- Share the desktop flow with another user.
- Edit users' permissions.
- Remove users' permissions for this desktop flow.

> [!NOTE]
>
> - Users of an environment with a Dataverse security role that provides them **Read** access to all the records of the **Process** Dataverse table are co-owners of all desktop flows created in this environment and can't be removed.
> - When a user isn't part of an environment anymore, you can continue to see it as a deactivated user. You'll be notified in the **Manage access** section of the desktop flow if this flow is shared with deactivated users. In this situation, remove access to them.

## Learn more

- [Create desktop flows](create-flow.md).
- [Trigger desktop flows from cloud flows](trigger-desktop-flows.md).
- [Monitor desktop flow runs](monitor-desktop-flow-runs.md).
- [Desktop flow activity](desktop-flow-activity.md).

[!INCLUDE[footer-include](../includes/footer-banner.md)]
