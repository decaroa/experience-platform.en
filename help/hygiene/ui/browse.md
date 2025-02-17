---
title: Browse Data Hygiene Work Orders
description: Learn how to view and manage existing data hygiene work orders in the Adobe Experience Platform user interface.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
---
# Browse data hygiene work orders {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="Work order IDs"
>abstract="When a data hygiene request is sent to the system, a work order is created to execute the requested task. In other words, a work order represents a specific data hygiene process, which includes its current status and other related details. Each work order is automatically assigned its own unique ID upon creation."
>text="See the data hygiene UI guide to learn more."

>[!IMPORTANT]
>
>Data hygiene capabilities in Adobe Experience Platform are currently only available for organizations that have purchased Healthcare Shield.

When a data hygiene request is sent to the system, a work order is created to execute the requested task. A work order represents a specific data hygiene process, such as a scheduled dataset expiration, which includes its current status and other related details.

This guide covers how to view and manage existing work orders in the Adobe Experience Platform UI.

## List and filter existing work orders

When you first access the **[!UICONTROL Data Hygiene]** workspace in the UI, a list of existing work orders is shown along with their basic details.

![Image showing the [!UICONTROL Data Hygiene] workspace in the Platform UI](../images/ui/browse/work-order-list.png)

<!-- The list only shows work orders for one category at a time. Select **[!UICONTROL Consumer]** to view a list of consumer deletion tasks, and **[!UICONTROL Dataset]** to view a list of scheduled dataset expirations.

![Image showing the [!UICONTROL Dataset] tab](../images/ui/browse/dataset-tab.png) -->

Select the funnel icon (![Image of the funnel icon](../images/ui/browse/funnel-icon.png)) to view a list of filters for the displayed work orders.

![Image of the work order filters displayed](../images/ui/browse/filters.png)

| Filter | Description |
| --- | --- |
| [!UICONTROL Status] | Filter based on the current status of the work order:<ul><li>**[!UICONTROL Completed]**: The job has been completed.</li><li>**[!UICONTROL Pending]**: The job has been created but has not been executed yet. A [dataset expiration request](./dataset-expiration.md) assumes this status before the scheduled deletion date. Once the deletion date arrives, the status updates to [!UICONTROL Executing] unless the job is cancelled beforehand.</li><li>**[!UICONTROL Executing]**: The dataset expiration request has started and is currently processing.</li><li>**[!UICONTROL Cancelled]**: The job has been cancelled as part of a manual user request.</li></ul> |
| [!UICONTROL Date created] | Filter based on the when the work order was made. |
| [!UICONTROL Expiration date] | Filter dataset expiration requests based on the scheduled deletion date for the dataset in question. |
| [!UICONTROL Date updated] | Filter dataset expiration requests based on the when the work order was last updated. Creations and expirations are counted as updates. |

{style="table-layout:auto"}

## View the details of a work order

Select the ID of a listed work order to view its details.

![Image showing a work order ID being selected](../images/ui/browse/select-work-order.png)

<!-- Depending on the type of work order selected, different information and controls are provided. These are covered in the sections below.

### Consumer delete details

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Consumer delete response"
>abstract="When a consumer deletion process receives a response from the system, these messages are displayed under the **[!UICONTROL Result]** section. If a problem occurs while a work order is processing, any relevant error messages will appear in this section to help you troubleshoot the issue. To learn more, see the data hygiene UI guide."


The details of a consumer delete request are read-only, displaying its basic attributes such as its current status and the time elapsed since the request was made.

![Image showing the details page for a consumer delete work order](../images/ui/browse/consumer-delete-details.png)

### Dataset expiration details -->

The details page for a dataset expiration provides information on its basic attributes, including the scheduled expiration date on the days remaining before the deletion occurs. In the right rail, you can use controls to edit or cancel the expiration.

![Image showing the details page for a dataset expiration work order](../images/ui/browse/ttl-details.png)

## Next steps

This guide covered how to view and manage existing data hygiene work orders in the Platform UI. For information on creating your own work orders, see the guide on [scheduling a dataset expiration](./dataset-expiration.md).
