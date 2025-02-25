---
title: Replace an existing derived element
sidebar_label: Replace an existing derived element
description: This workflow sample demonstrates how to replace an existing derived element object through the Modeling service.
---

<Available since="2021 Update 1" />

:::tip

You can try out this workflow at [REST API Playground](https://www.postman.com/microstrategysdk/workspace/microstrategy-rest-api/folder/16131298-d4a5b7c7-3dba-46fc-acce-0683a23bb1fe?ctx=documentation).

Learn more about MicroStrategy REST API Playground [here](/docs/getting-started/playground.md).

:::

This workflow sample demonstrates how to replace an existing derived element object through the Modeling service.

1. Create a changeset.
1. [Replace an existing derived element.](#replace-an-existing-derived-element)
1. Commit the changeset.
1. Delete the changeset.

You want to replace the existing `"Region DE"` derived element object in the MicroStrategy Tutorial project. The derived element object ID is `610B9CC14AD9DCB69F094C89D3B5480B`. The project ID is `B19DEDCC11D4E0EFC000EB9495D0F44F`.

:::info

Get the authorization token needed to execute the request with [POST /api/auth/login](https://demo.microstrategy.com/MicroStrategyLibrary/api-docs/index.html#/Authentication/postLogin).

Get the project ID from [GET /api/projects](https://demo.microstrategy.com/MicroStrategyLibrary/api-docs/index.html#/Projects/getProjects_1).

:::

:::tip

Changesets are used in this workflow. For information on how to create and use changesets, see [Changesets](/docs/common-workflows/modeling/changesets.md).

:::

## Replace an existing derived element

Use [PUT /api/model/derivedElements/{derivedElementId}](https://demo.microstrategy.com/MicroStrategyLibrary/api-docs/index.html#/Derived%20Elements/ms-putDerivedElement)

The embedded elements in a derived element can be `"list"`, `"filter"`, `"calculation"` or `"all_other"`. In this example, you are replacing the existing `"Region DE"` derived element with an embedded `"list"` element and an `"all_other"` element.

:::tip

Each derived element must have exactly one `"all_other"` element.

:::

Sample Request Header:

```http
"accept": "application/json"
"X-MSTR-AuthToken": "pisu5dkkutqfblaamdomgr00ch"
"X-MSTR-MS-Changeset": "0E9F01172ECF4BA2BB510F7B9FB4F6E8"
```

Sample Request Body:

:::tip

For more details on how to set format properties, please refer to [Format samples for derived elements](format-samples.md).

:::

```json
{
  "information": {
    "name": "Replaced Region DE"
  },
  "attribute": {
    "objectId": "8D679D4B11D3E4981000E787EC6DE8A4",
    "name": "Region"
  },
  "elements": [
    {
      "name": "offline",
      "type": "list",
      "format": {
        "header": [],
        "values": []
      },
      "options": {
        "display": "this_element",
        "subtotal": "this_element",
        "includeIndividual": false
      },
      "text": "Mid-Atlantic, Northeast, Southeast, Northwest, Southwest, Central, South",
      "elements": [
        {
          "display": "Mid-Atlantic",
          "elementId": "h2"
        },
        {
          "display": "Northeast",
          "elementId": "h1"
        },
        {
          "display": "Southeast",
          "elementId": "h3"
        },
        {
          "display": "Northwest",
          "elementId": "h4"
        },
        {
          "display": "Southwest",
          "elementId": "h5"
        },
        {
          "display": "Central",
          "elementId": "h6"
        },
        {
          "display": "South",
          "elementId": "h7"
        }
      ]
    },
    {
      "name": "Web",
      "type": "all_other",
      "format": {
        "header": [],
        "values": []
      },
      "options": {
        "display": "individual_items",
        "subtotal": "this_element"
      }
    }
  ]
}
```

Sample Curl:

```bash
curl -X PUT "http://10.23.9.111:8080/MicroStrategyLibrary/api/model/derivedElements" -H "accept: application/json" -H "X-MSTR-AuthToken: 9rlq0e1dgg3rp237hiddruqcd0" -H "X-MSTR-MS-Changeset: EE48CD8879C44A03B18660AE7AFC8F68" -H "Content-Type: application/json" -d "{\"elements\":[{\"name\":\"offline\",\"type\":\"list\",\"format\":{\"header\":[],\"values\":[]},\"options\":{\"display\":\"this_element\",\"subtotal\":\"this_element\",\"includeIndividual\":false},\"text\":\"Mid-Atlantic,Northeast,Southeast,Northwest,Southwest,Central,South\",\"elements\":[{\"display\":\"Mid-Atlantic\",\"elementId\":\"h2\"},{\"display\":\"Northeast\",\"elementId\":\"h1\"},{\"display\":\"Southeast\",\"elementId\":\"h3\"},{\"display\":\"Northwest\",\"elementId\":\"h4\"},{\"display\":\"Southwest\",\"elementId\":\"h5\"},{\"display\":\"Central\",\"elementId\":\"h6\"},{\"display\":\"South\",\"elementId\":\"h7\"}]},{\"name\":\"Web\",\"type\":\"all_other\",\"format\":{\"header\":[],\"values\":[]},\"options\":{\"display\":\"individual_items\",\"subtotal\":\"this_element\"}}]}"
```

Sample Response Body:

You can view he new derived element's definition in the body of the response.

```json
{
  "information": {
    "dateCreated": "2021-02-20T09:18:18.000Z",
    "dateModified": "2021-02-20T09:40:14.000Z",
    "versionId": "325929D9432F9D23C7CEDFA473E70D7F",
    "primaryLocale": "en-US",
    "objectId": "610B9CC14AD9DCB69F094C89D3B5480B",
    "subType": "consolidation_element",
    "name": "Replaced Region DE"
  },
  "attribute": {
    "objectId": "8D679D4B11D3E4981000E787EC6DE8A4",
    "subType": "attribute",
    "name": "Region"
  },
  "elements": [
    {
      "id": "26785E245237495E908D9F620F81E02F",
      "name": "offline",
      "type": "list",
      "format": {
        "header": [],
        "values": []
      },
      "options": {
        "display": "this_element",
        "subtotal": "this_element",
        "includeIndividual": false
      },
      "text": "Mid-Atlantic, Northeast, Southeast, Northwest, Southwest, Central, South",
      "elements": [
        {
          "display": "Mid-Atlantic",
          "elementId": "h2"
        },
        {
          "display": "Northeast",
          "elementId": "h1"
        },
        {
          "display": "Southeast",
          "elementId": "h3"
        },
        {
          "display": "Northwest",
          "elementId": "h4"
        },
        {
          "display": "Southwest",
          "elementId": "h5"
        },
        {
          "display": "Central",
          "elementId": "h6"
        },
        {
          "display": "South",
          "elementId": "h7"
        }
      ]
    },
    {
      "id": "33686BC5418B4CFDAEC01298E5201E53",
      "name": "Web",
      "type": "all_other",
      "format": {
        "header": [],
        "values": []
      },
      "options": {
        "display": "individual_items",
        "subtotal": "this_element"
      }
    }
  ]
}
```

Response Code: 201 (The "Region DE" derived element is replaced successfully in the changeset.)
