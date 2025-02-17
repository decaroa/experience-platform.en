---
title: Work order API Endpoint
description: The /workorder endpoint in the Data Hygiene API allows you to programmatically manage deletion tasks for consumer identities.
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
hide: true
hidefromtoc: true
---
# Work order endpoint

>[!IMPORTANT]
>
>Data hygiene capabilities in Adobe Experience Platform are currently only available for organizations that have purchased Healthcare Shield.

The `/workorder` endpoint in the Data Hygiene API allows you to programmatically manage deletion tasks for consumer identities in Adobe Experience Platform.

## Getting started

The endpoint used in this guide is part of the Data Hygiene API. Before continuing, please review the [overview](./overview.md) for links to related documentation, a guide to reading the sample API calls in this document, and important information regarding required headers that are needed to successfully make calls to any Experience Platform API.

## Delete identities {#delete-identities}

You can delete one or more consumer identities from a single dataset or all datasets by making a POST request to the `/workorder` endpoint.

**API format**

```http
POST /workorder
```

**Request**

Depending on the value of the `datasetId` provided in the request payload, the API call will delete consumer identities from all datasets or a single dataset that you specify. The following request deletes three consumer identities from a specific dataset.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "action": "delete_identity",
        "datasetId": "c48b51623ec641a2949d339bad69cb15",
        "identities": [
          {
            "namespace": {
              "code": "email"
            },
            "id": "poul.anderson@example.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cordwainer.smith@gmail.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cyril.kornbluth@yahoo.com"
          }
        ]
      }'
```

| Property | Description |
| --- | --- |
| `action` | The action to be performed. The value must be set to `delete_identity` when deleting identities. |
| `datasetId` | If you are deleting from a single dataset, this value must be the ID of the dataset in question. If you are deleting from all datasets, set the value to `ALL`.<br><br>If you are specifying a single dataset, the dataset's associated Experience Data Model (XDM) schema must have a primary identity defined. |
| `identities` | An array containing the identities of at least one user whose information you would like to delete. Each identity is comprised of an [identity namespace](../../identity-service/namespaces.md) and a value:<ul><li>`namespace`: Contains a single string property, `code`, which represents the identity namespace. </li><li>`id`: The identity value.</ul>If `datasetId` specifies a single dataset, each entity under `identities` must use the same identity namespace as the schema's primary identity.<br><br>If `datasetId` is set to `ALL`, the `identities` array is not constrained to any single namespace since each dataset might be different. However, your requests are still constrained the namespaces available to your organization, as reported by [Identity Service](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style="table-layout:auto"}

**Response**

A successful response returns the details of the identity deletion.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "batchId": "fc0cf8af-a176-4107-a31a-381d6af38cbe",
  "bundleOrdinal": 1,
  "payloadByteSize": 362,
  "operationCount": 3,
  "createdAt": 1652122493242,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| Property | Description |
| --- | --- |
| `workorderId` | The ID of the deletion order. This can be used to look up the status of the deletion later. |
| `orgId` | Your organization's ID. |
| `batchId` | The ID of the batch this deletion order is associated with, used for debugging purposes. Multiple deletion orders are bundled together into a batch to be processed by downstream services. |
| `bundleOrdinal` | The order in which this deletion order was received when it was bundled into a batch for downstream processing. Used for debugging purposes. |
| `payloadByteSize` | The size, in bytes, of the list of identities that were provided in the request payload that created this deletion order. |
| `operationCount` | The number of identities this deletion order applies to. |
| `createdAt` | A timestamp of when the deletion order was created. |
| `responseMessage` | The latest response returned by the system. If an error occurs during processing, this value will be a JSON string containing detailed error information to help you understand what might have gone wrong. |
| `status` | The current status of the deletion order. |
| `createdBy` | The user that created the deletion order. |

{style="table-layout:auto"}

## List the statuses of all identity deletions {#list}

You can list the statuses of all identity deletions by making a GET request.

**API format**

```http
GET /workorder?{QUERY_PARAMS}
```

| Parameter | Description |
| --- | --- |
| `{QUERY_PARAMS}` | A list of optional query parameters for the listing call, with multiple parameters separated by `&` characters. Accepted query params are as follows:<ul><li>`data` - A boolean value that, when set to `true`, includes all additional request and response data received for the deletion order. Defaults to `false`.</li><li>`start` - A timestamp for the beginning of the timeframe to search for deletion orders.</li><li>`end` - A timestamp for the end of the timeframe to search for deletion orders.</li><li>`page` - The specific response page to return.</li><li>`limit` - The number of records to be displayed per page.</li></ul>|

{style="table-layout:auto"}

**Request**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Response**

A successful response returns the details of all delete operations, including their current status. The example response below has been truncated for space.

```json
{
  "results": [
    {
      "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
      "orgId": "{ORG_ID}",
      "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650929265295,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    },
    {
      "workorderId": "e4a662e8-a5f3-497d-8d6a-d26970d8732b",
      "orgId": "{ORG_ID}",
      "batchId": "74fe4e38-ed42-4ca5-8bee-88bdc03ae786",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650931057899,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    }
  ],
  "total": 200,
  "count": 50,
  "_links": {
    "next": {
      "href": "https://platform.adobe.io/workorder?page=1&limit=50",
      "templated": false
    },
    "page": {
      "href": "https://platform.adobe.io/workorder?limit={limit}&page={page}",
      "templated": true
    }
  }
}
```

| Property | Description |
| --- | --- |
| `results` | Contains the list of deletion orders and their details. For more information on the properties of a deletion order, see the example response in the section on [looking up a deletion order](#lookup). |
| `total` | The total number of deletion orders found based on current filters. |
| `count` | The total number of deletion orders found on each page of the response. |
| `_links` | Contains pagination information to help you explore the rest of the response:<ul><li>`next`: Contains a URL for the next page in the response.</li><li>`page`: Contains a URL template to access another page in the response or adjust the number of items returned on each page.</li></ul> |

{style="table-layout:auto"}

## Retrieve the status of an identity deletion (#lookup)

After sending a request to [delete an identity](#delete-identities), you can check on its status using a GET request.

**API format**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parameter | Description |
| --- | --- |
| `{WORK_ORDER_ID}` | The `workorderId` of the identity deletion you are looking up. |

{style="table-layout:auto"}

**Request**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/ID6c28e2d2d2b54079aadf7be94568f6d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Response**

A successful response returns the details of the delete operation, including its current status.

```json
{
  "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
  "orgId": "{ORG_ID}",
  "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
  "bundleOrdinal": 1,
  "payloadByteSize": 164,
  "operationCount": 1,
  "createdAt": 1650929265295,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| Property | Description |
| --- | --- |
| `workorderId` | The ID of the deletion order. This can be used to look up the status of the deletion later. |
| `orgId` | Your organization's ID. |
| `batchId` | The ID of the batch this deletion order is associated with, used for debugging purposes. Multiple deletion orders are bundled together into a batch to be processed by downstream services. |
| `bundleOrdinal` | The order in which this deletion order was received when it was bundled into a batch for downstream processing. Used for debugging purposes. |
| `payloadByteSize` | The size, in bytes, of the list of identities that were provided in the request payload that created this deletion order. |
| `operationCount` | The number of identities this deletion order applies to. |
| `createdAt` | A timestamp of when the deletion order was created. |
| `responseMessage` | The latest response returned by the system. If an error occurs during processing, this value will be a JSON string containing detailed error information to help you understand what might have gone wrong. |
| `status` | The current status of the deletion order. |
| `createdBy` | The user that created the deletion order. |
