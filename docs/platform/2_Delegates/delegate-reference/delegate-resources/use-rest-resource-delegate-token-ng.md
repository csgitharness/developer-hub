---
title: Use REST resource delegate-token-ng
description: Describes the use of the delegate-token-ng REST resource.
# sidebar_position: 2
---


# Use REST resource delegate-token-ng
`/ng/api/delegate-token-ng`
`/ng/api/delegate-token-ng/delegate-groups`


Use the **Delegate Token Resource** to create and delete delegate tokens. You can also use this resource to retrieve delegate tokens and delegates that are using specific delegate tokens. 

To use this resource, you must have a Harness account and an API key. For information on configuring your Harness account with an API key, see [Harness API Quickstart](https://docs.harness.io/article/f0aqiv3td7-api-quickstart).

For detailed information on constructing requests, see [Delegate Token Resource](https://apidocs.harness.io/tag/Delegate-Token-Resource).

## Use case

This resource is useful in integrations in which delegates are manipulated programmatically by delegate token.

## Operations

The **Delegate Token Resource** provides the following operations.

| **Operation** | **HTTP method** | **Description** |
| :-- | :-- | :-- |
| [Create delegate token](https://apidocs.harness.io/tag/Delegate-Token-Resource#operation/createDelegateToken) | `POST` | Creates and assigns a delegate token the specified name. |
| [List delegate groups by token](https://apidocs.harness.io/tag/Delegate-Token-Resource#operation/getDelegateGroupsUsingToken) | `GET` | Lists the delegate groups that are using the specified delegate token. |
| [Retrieve delegate tokens](https://apidocs.harness.io/tag/Delegate-Token-Resource#operation/getDelegateTokens) | `GET` | Retrieves delegate tokens by account, organization, project, and status. |
| [Revoke delegate token](https://apidocs.harness.io/tag/Delegate-Token-Resource#operation/revokeDelegateToken) | `PUT` | Revokes the delegate token of the specified token name. |


## Create a delegate token
`operation/createDelegateToken`

Use this request to create a delegate token and assign the token a name.

This request  requires an account identifier and the specification of a token name. For detailed information on required and optional parameters, see [Create Delegate Token](https://apidocs.harness.io/tag/Delegate-Token-Resource#operation/createDelegateToken).

### HTTP request

The following example URL includes the required and optional parameters in italics:

https://app.harness.io/gateway/ng/api/delegate-token-ng?accountIdentifier=XXXXXXXXXXXxxxxxxxxxxx&projectIdentifier=delegateAPIs&orgIdentifier=myOrg&tokenName=cdTasksToken

You can confirm the creation in **Account Settings > Account Resources**. If you specify a project for the token, you can find it in the project information. If you specify an organization and a project, the token is displayed only in the project information for the organization.

### Request body

The request body must be empty.

For the API specification, see [Create Delegate Token](https://apidocs.harness.io/tag/Delegate-Token-Resource#operation/createDelegateToken) in [Harness NextGen Platform API Reference](https://apidocs.harness.io/).

### Response body

The response body contains an object that describes the details of the token that was created, including the creator, the assigned UUID, and the associated account identifier.

**[Generate the response again -- Arpit says responseMessages should be empty]**

## List delegates by token
`operation/getDelegateGroupsUsingToken`

### HTTP request

The delegate token name is an optional query parameter. In the following example, the token name is `delegate-apis-token`:

```
/ng/api/delegate-token-ng/delegate-groups?accountIdentifier=H5W8iol5TNWc4G9h5A2MXg&delegateTokenName=delegate-apis-token
```

### Request body
The request body must be empty.

### Response body

The response contains the `delegateGroupDetails` array of objects, each of which describes one of the delegates that are using the specified token. 

`delegateTokenName` is an optional query parameter. If not specified, this operation returns a list that includes all the delegates associated with the account. 

**[Arpit says the responseMessages field should be empty for this one too]**

For the API specification, see [List delegate groups that are using the specified token](https://apidocs.harness.io/tag/Delegate-Token-Resource#operation/getDelegateGroupsUsingToken) in [Harness NextGen Platform API Reference]()https://apidocs.harness.io/.


## Retrieve tokens
`operation/getDelegateTokens`

Use this request to retrieve a list of delegate tokens associated with the specified account. You can optionally specify that the list be filtered by organization, project, or delegate token name.

### HTTP request

The following example URL includes the required and optional parameters in italics:

```
/ng/api/delegate-token-ng?accountIdentifier=XXXXXXXXXXXxxxxxxxxxxx&orgIdentifier=DocExample&projectIdentifier=delegateAPIs
```

### Request body

The request body must be empty.

For the API specification, see [Retrieve delegate tokens](https://apidocs.harness.io/tag/Delegate-Token-Resource#operation/getDelegateTokens) in [Harness NextGen Platform API Reference](https://apidocs.harness.io/).

### Response body

The response body includes an object that contains an array of `DelegateTokenDetails` objects. 

```
{
  "metaData": {},
  "resource": {
    "delegateGroupDetails": []
  },
  "responseMessages": []
}
```

Each `DelegateTokenDetails` object describes the details of one of the delegate tokens that were found. Each object is defined based on the following schema:

**[Regenerate the response body for this one too]**

 In this workflow, the **Delegate Token Resource** is used to list and then revoke a listed delegate token.

### Send the request

This request requires only one URL parameter &mdash; the identifier of the Harness account (`accountIdentifier`) for which you want to list the token names in use. You can narrow your results by using optional identifiers for Harness organization (`orgIdenifier`) and Harness project (`projectIdentifier`). You can optionally use the status parameter to include only those tokens that are active (“ACTIVE”) or revoked (“REVOKED"). 

### Example request

```
curl -i -X PUT \
  'https://app.harness.io/gateway/ng/api/delegate-token-ng?accountIdentifier=XXXXXXXXXXXxxxxxxxxxxx&orgIdentifier=string&projectIdentifier=string&tokenName=my-delegate' \
  -H 'x-api-key: pat.XXXXXXXXXXXxxxxxxxxxxx.63505f3c25597247dfb0c77a.suKA7bmXoEXdSa9vKOZa'
```

For the API specification, see [List tags](https://apidocs.harness.io/tag/Delegate-Group-Tags-Resource#operation/listTagsForDelegateGroup) in [Harness NextGen Platform API Reference](https://apidocs.harness.io/).

### Example response

The response includes a JSON object that contains information about the delegate/token name.

**[Regenerate response - responseMessages should be empty]**

### View the result

```

{
  "metaData": {},
  "resource": [
    {
      "uuid": null,
      "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
      "name": "default_token",
      "createdBy": null,
      "createdByNgUser": null,
      "createdAt": 1645515925370,
      "status": "ACTIVE",
      "value": null,
      "ownerIdentifier": null
    },
    {
      "uuid": null,
      "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
      "name": "example",
      "createdBy": null,
      "createdByNgUser": {
        "type": "USER",
        "name": "xxXxXxxxX3XxXXxXx16xXx",
        "email": "harness.user2@example.com",
        "username": "harness.user2@example.com",
        "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
        "jwtclaims": {
          "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
          "name": "xxXxXxxxX3XxXXxXx16xXx",
          "type": "USER",
          "email": "harness.user2@example.com",
          "username": "harness.user2@example.com"
        }
      },
      "createdAt": 1647384540182,
      "status": "ACTIVE",
      "value": null,
      "ownerIdentifier": null
    },
    {
      "uuid": null,
      "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
      "name": "qa",
      "createdBy": null,
      "createdByNgUser": {
        "type": "USER",
        "name": "xxXxXxxxX3XxXXxXx16xXx",
        "email": "harness.user2@example.com",
        "username": "harness.user2@example.com",
        "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
        "jwtclaims": {
          "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
          "name": "xxXxXxxxX3XxXXxXx16xXx",
          "type": "USER",
          "email": "harness.user2@example.com",
          "username": "harness.user2@example.com"
        }
      },
      "createdAt": 1647384899732,
      "status": "ACTIVE",
      "value": null,
      "ownerIdentifier": null
    },
    {
      "uuid": null,
      "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
      "name": "harness-user1",
      "createdBy": null,
      "createdByNgUser": {
        "type": "USER",
        "name": "YYYYYYYYYYYYzzzzzzzz",
        "email": "harness.user1@example.com",
        "username": "Harness User1",
        "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
        "jwtclaims": {
          "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
          "name": "YYYYYYYYYYYYzzzzzzzz",
          "type": "USER",
          "email": "harness.user1@example.com",
          "username": "Harness User1"
        }
      },
      "createdAt": 1656013873627,
      "status": "ACTIVE",
      "value": null,
      "ownerIdentifier": null
    },
    {
      "uuid": null,
      "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
      "name": "lavi",
      "createdBy": null,
      "createdByNgUser": {
        "type": "USER",
        "name": "YYYYYYYYYYYYzzzzzzzz",
        "email": "harness.user1@example.com",
        "username": "Harness User1",
        "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
        "jwtclaims": {
          "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
          "name": "YYYYYYYYYYYYzzzzzzzz",
          "type": "USER",
          "email": "harness.user1@example.com",
          "username": "Harness User1"
        }
      },
      "createdAt": 1656013897425,
      "status": "ACTIVE",
      "value": null,
      "ownerIdentifier": null
    },
    {
      "uuid": null,
      "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
      "name": "api example",
      "createdBy": null,
      "createdByNgUser": {
        "type": "USER",
        "name": "xxXxXxxxX3XxXXxXx16xXx",
        "email": "harness.user2@example.com",
        "username": "Harness User2",
        "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
        "jwtclaims": {
          "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
          "name": "xxXxXxxxX3XxXXxXx16xXx",
          "type": "USER",
          "email": "harness.user2@example.com",
          "username": "Harness User 2"
        }
      },
      "createdAt": 1666376232919,
      "status": "ACTIVE",
      "value": null,
      "ownerIdentifier": null
    },
    {
      "uuid": null,
      "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
      "name": "api example2",
      "createdBy": null,
      "createdByNgUser": {
        "type": "USER",
        "name": "xxXxXxxxX3XxXXxXx16xXx",
        "email": "harness.user2@example.com",
        "username": "Harness User2",
        "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
        "jwtclaims": {
          "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
          "name": "xxXxXxxxX3XxXXxXx16xXx",
          "type": "USER",
          "email": "harness.user2@example.com",
          "username": "Harness User2"
        }
      },
      "createdAt": 1666376263339,
      "status": "ACTIVE",
      "value": null,
      "ownerIdentifier": null
    },
    {
      "uuid": null,
      "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
      "name": "example3",
      "createdBy": null,
      "createdByNgUser": {
        "type": "USER",
        "name": "xxXxXxxxX3XxXXxXx16xXx",
        "email": "harness.user2@example.com",
        "username": "Harness User2",
        "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
        "jwtclaims": {
          "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
          "name": "xxXxXxxxX3XxXXxXx16xXx",
          "type": "USER",
          "email": "harness.user2@example.com",
          "username": "Harness User2"
        }
      },
      "createdAt": 1666376353456,
      "status": "ACTIVE",
      "value": null,
      "ownerIdentifier": null
    },
    {
      "uuid": null,
      "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
      "name": "delegateToken1",
      "createdBy": null,
      "createdByNgUser": {
        "type": "USER",
        "name": "C-xx01XXXXxXXx-xxXX6Xx",
        "email": "harness.user@example.com",
        "username": "Harness User",
        "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
        "jwtclaims": {
          "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
          "name": "C-xx01XXXXxXXx-xxXX6Xx",
          "type": "USER",
          "email": "harness.user@example.com",
          "username": "Harness User"
        }
      },
      "createdAt": 1666394445212,
      "status": "ACTIVE",
      "value": null,
      "ownerIdentifier": null
    }
  ],
  "responseMessages": []
}


```

## Revoke the delegate token
`operation/revokeToken`

Use this operation to revoke a delegate token. Harness Manager does not accept connections from delegates using revoked tokens.

### HTTP request

This request requires a Harness account ID (`accountIdentifier`) and the name of the token you want to revoke (`tokenName`). In this case, `tokenName` is `cdTasksToken`.

```
/ng/api/delegate-token-ng?accountIdentifier=XXXXXXXXXXXxxxxxxxxxxx&tokenName=cdTasksToken
```

You can optionally specify the associated Harness project ID (`projectIdentifier`) and the Harness organization ID (`orgIdentifier`). 

### Request body

The request body must be empty.

For the API specification, see [Revoke Delegate Token](https://apidocs.harness.io/tag/Delegate-Token-Resource#operation/revokeDelegateToken) in [Harness NextGen Platform API Reference](https://apidocs.harness.io/).

### Response body

A successful request returns with `HTTP status code 200 OK`. You can check the message body for the result of the `POST` action.

```
{
  "metaData": {},
  "resource": {
    "uuid": null,
    "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
    "name": "cdTasksToken",
    "createdBy": null,
    "createdByNgUser": {
      "type": "USER",
      "name": "C-xx01XXXXxXXx-xxXX6Xx",
      "email": "harness.user@harness.io",
      "username": "Harness User,
      "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
      "jwtclaims": {
        "accountId": "XXXXXXXXXXXxxxxxxxxxxx",
        "name": "C-xx01XXXXxXXx-xxXX6Xx",
        "type": "USER",
        "email": "harness.user@harness.io",
        "username": "Harness User"
      }
    },
    "createdAt": 1670454510813,
    "status": "REVOKED",
    "value": null,
    "ownerIdentifier": "myOrg/delegateAPIs"
  },
  "responseMessages": []
}
```
In this example, the `status` field indicates that the token is revoked.

Confirm the revocation of the delegate token by sending a second request to retrieve delegate tokens. For information on how to delete a delegate see [Delete a delegate](/docs/platrform/2_Delegates/manage-delegates/delete-a-delegate.md).
