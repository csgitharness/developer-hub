---
title: Use REST resource delegate-group-tags
description: Describes the use of the delegate-group-tags REST resource.
# sidebar_position: 2
---


# Use REST resource delegate-group-tags
`/ng/api/delegate-group-tags`
`/ng/api/delegate-group-tags/delegate-groups`


Use the operations of the **Delegate Group Tags Resource** to add, list or delete tags from the specified delegate, to replace a set of tags with another for the specified delegate, or to list the delegates that have the specified tags.

To use this resource, you must have a Harness account and an API key. For information on configuring your Harness account with an API key, see [Harness API Quickstart](/docs/platform/apis/api-quickstart/).

Several operations of this resource additionally require the specification of a `groupIdentifier` value. This is the delegate identifier. 

To find the delegate identifier, navigate to **Account Settings > Account Resources**. Then click the delegate name. The identifier of the delegate is displayed on the **Overview** page. 

![](static/use-rest-resource-delegate-group-tags-01.png)

For detailed information on constructing requests, see [Delegate Group Tags Resource]().

## Use case

This resource is useful in integrations that automate the delegate lifecycle.

## Operations

The **Delegate Group Tags Resource** provides the following operations.

| **Operation** | **HTTP method** | **Description** |
| :-- | :-- | :-- |
| [Add tags](https://apidocs.harness.io/tag/Delegate-Group-Tags-Resource/#operation/addTagsToDelegateGroup) | `POST` | Add the specified list of tags to the delegate. |
| [Replace tags](https://apidocs.harness.io/tag/Delegate-Group-Tags-Resource#operation/updateTagsOfDelegateGroup) | `PUT` | Remove the existing tags from a delegate and replace them with the specified tags. |
| [Delete tags](https://apidocs.harness.io/tag/Delegate-Group-Tags-Resource#operation/deleteTagsFromDelegateGroup) | `DEL` | Remove the tags from the specified delegate. |
| [List delegate groups](https://apidocs.harness.io/tag/Delegate-Group-Tags-Resource#operation/listDelegateGroupsUsingTags) | `POST` | List the delegates that have the specified tags. |
| [Retrieve tags](https://apidocs.harness.io/tag/Delegate-Group-Tags-Resource#operation/listTagsForDelegateGroup) | `GET` | Retrieve a list of the tags associated with the specified delegate. |

## Add tags to a delegate

`operation/addTagsToDelegateGroup`

Use this operation to add a comma-separated list of one or more descriptive tags to a delegate.

### HTTP request

The following example URL includes the required and optional parameters in italics:

https://app.harness.io/gateway/ng/api/delegate-group-tags/docimmut?accountIdentifier=XXXXXXXXXXXxxxxxxxxxxx&orgIdentifier=myOrg&projectIdentifier=myProject

### Request body

The request body must include a JSON-formatted array of one or more descriptive tags specified as comma-separated strings. The following entity provides an example of the request body schema. 

```
{
  "tags": [
    "cd-del-prod-nginx", "cd-del-prod-smb"
  ]
}
```

In this case, the `tags` array contains strings for the tags `cd-del-prod-nginx` and `cd-del-prod-smb`:

For the API specification, see [Add given list of tags to the Delegate Group](https://apidocs.harness.io/tag/Delegate-Group-Tags-Resource#operation/addTagsToDelegateGroup) in [Harness NextGen Platform API Reference](https://apidocs.harness.io/).

### Response body

The response includes an entity that contains the specified array of tags, in this case `cd-del-prod-smb` and `cd-del-prod-nginx`.

```
{
    "metaData": { },
    "resource":
    {
        "accountIdentifier": "XXXXXXXXXXXxxxxxxxxxxx",
        "orgIdentifier": null,
        "projectIdentifier": null,
        "name": "doc-immut",
        "identifier": "docimmut",
        "tags":
        [
            "cd-del-prod-smb",
            "cd-del-prod-nginx"
        ]
    },
    "responseMessages": [ ]
}
```
 
## List delegates by tag
`operation/listDelegateGroupsUsingTags`

Use this operation to list the delegates that have the specified tags.  

### HTTP request

The following example URL includes the required and optional parameters in italics:

```
https://app.harness.io/gateway/ng/api/delegate-group-tags/docimmut?accountIdentifier=XXXXXXXXXXXxxxxxxxxxxx&orgIdentifier=myOrg&projectIdentifier=myProject
```

### Request body

The request body must include an entity formatted as follows. The entity must contain an array of the tags to search for. Specify one or more valid tags.

```
{
    "metaData": { },
    "resource":
    [
        {
            "accountIdentifier": "XXXXXXXXXXXxxxxxxxxxxx",
            "orgIdentifier": null,
            "projectIdentifier": null,
            "name": "doc-immut",
            "identifier": "docimmut",
            "tags":
            [
                "cd-del-prod-smb",
                "doc-immut",
                "cd-del-prod-nginx"
            ]
        }
    ],
"responseMessages": [ ]
}

```

In this example, the `tags` field specifies an array of the tags `cd-del-prod-smb`, `doc-immut`, and `cd-del-prod-nginx`.

For the API specification, see [List delegate groups by tag](https://apidocs.harness.io/tag/Delegate-Group-Tags-Resource#operation/listDelegateGroupsUsingTags) in [Harness NextGen Platform API Reference](https://apidocs.harness.io/).

### Response body

A successful response includes an entity containing an array of the delegates, if any, that are associated with the specified tags.

{
  "metaData": {
    "property1": {},
    "property2": {}
  },
  "resource": [
    {
      "accountIdentifier": "string",
      "orgIdentifier": "string",
      "projectIdentifier": "string",
      "name": "string",
      "identifier": "string",
      "tags": [
        "string"
      ]
    }
  ],
  "responseMessages": [
    {
      "code": "DEFAULT_ERROR_CODE",
      "level": "INFO",
      "message": "string",
      "exception": {
        "stackTrace": [
          {
            "classLoaderName": "string",
            "moduleName": "string",
            "moduleVersion": "string",
            "methodName": "string",
            "fileName": "string",
            "lineNumber": 0,
            "className": "string",
            "nativeMethod": true
          }
        ],
        "message": "string",
        "suppressed": [
          {
            "stackTrace": [
              {
                "classLoaderName": null,
                "moduleName": null,
                "moduleVersion": null,
                "methodName": null,
                "fileName": null,
                "lineNumber": null,
                "className": null,
                "nativeMethod": null
              }
            ],
            "message": "string",
            "localizedMessage": "string"
          }
        ],
        "localizedMessage": "string"
      },
      "failureTypes": [
        "EXPIRED"
      ]
    }
  ]
}

## List tags by delegate
`operation/listTagsForDelegateGroup``

Use this operation to obtain a list of the tags that are associated with the specified delegate. For the `groupIdentifier` path parameter, specify the delegate identifier.

### HTTP request

The following request URL includes the required and optional parameters in italics. 

```
https://app.harness.io/gateway/ng/api/delegate-group-tags/docimmut?accountIdentifier=XXXXXXXXXXXxxxxxxxxxxx
```

The only required query parameter is `groupIdentifier`, in this case, `docimmut`
.
### Request body

The request body must be empty.

### Response body

A successful request returns an entity of the following form. The entity contains an array of the tags that are associated with the specified delegate. In this example, the tags are associated with the delegate identified as `docimmut`. The delegate was assigned the tags `cd-del-prod-smb`, `doc-immut`, and `cd-del-prod-nginx`.

```
{
    "metaData": { },
    "resource":
    {
        "accountIdentifier": "XXXXXXXXXXXxxxxxxxxxxx",
        "orgIdentifier": null,
        "projectIdentifier": null,
        "name": "doc-immut",
        "identifier": "docimmut",
        "tags":
        [
            "cd-del-prod-smb",
            "doc-immut",
            "cd-del-prod-nginx"
        ]
    }
}

```

## Replace tags
`operation/updateTagsOfDelegateGroup`

Use this operation to remove the existing tags for a delegate, if any, and replace them with different tags. 

### HTTP request

The following query URL includes the required parameters in italics. For purposes of this example, the delegate identifier is `docdelegate` and the `accountIdentifier` is `XXXXXXXXXXXxxxxxxxxxxx`.

```
https://app.harness.io/gateway/ng/api/delegate-group-tags/docdelegate?accountIdentifier=XXXXXXXXXXXxxxxxxxxxxx
```

### Request body

Specify the replacement tags as comma-separated strings in the tags array, as shown in this JSON example:

```
{
  "tags": [
    "cd-tasks",  
    "ci-tasks-secondary"
  ]
}
```

### Response body

A successful response contains a delegate data transfer object (DTO) that identifies the delegate and includes a JSON array of the specified tags. 

```
{
  "metaData": {},
  "resource": {
    "accountIdentifier": "H5W8iol5TNWc4G9h5A2MXg",
    "orgIdentifier": null,
    "projectIdentifier": null,
    "name": "doc-delegate",
    "identifier": "docdelegate",
    "tags": [
      "ci-tasks-secondary",
      "cd-tasks"
    ]
  },
  "responseMessages": []
}
```

In this example, the delegate name is doc-delegate; the delegate is identified by the docdelegate identifier and is associated with the XXXXXXXXXXXxxxxxxxxxxx account. The tags array specifies the ci-tasks-secondary and cd-tasks tags for the docdelegate delegate.

## Remove tags from a delegate
`operation/deleteTagsFromDelegateGroup`

Use this operation to delete the tags from a delegate. 

### HTTP request

The following example URL includes the required parameters in italics. The `groupIdentifier` is the delegate identifier, in this case `docdelegate`. The `accountIdentifier` is `XXXXXXXXXXXxxxxxxxxxxx`.

https://app.harness.io/gateway/ng/api/delegate-group-tags/docdelegate?accountIdentifier=XXXXXXXXXXXxxxxxxxxxxx

### Request body

The request body must be empty. 

### Response body

The response contains a delegate data transfer object (DTO) that identifies the delegate and includes a JSON array that is empty. 

```
{
  "metaData": {},
  "resource": {
    "accountIdentifier": "XXXXXXXXXXXxxxxxxxxxxx",
    "orgIdentifier": null,
    "projectIdentifier": null,
    "name": "doc-delegate",
    "identifier": "docdelegate",
    "tags": []
  },
  "responseMessages": []
}
```

In this example, the delegate name is `doc-delegate`; the delegate is identified by the `docdelegate` identifier and is associated with the `XXXXXXXXXXXxxxxxxxxxxx` account. The delegate has no associated tags.

For the API specification, see [Deletes all tags from the delegate group](https://apidocs.harness.io/tag/Delegate-Group-Tags-Resource#operation/updateTagsOfDelegateGroup) in [Harness NextGen Platform API Reference](https://apidocs.harness.io/tag/Delegate-Group-Tags-Resource#operation/updateTagsOfDelegateGroup).

