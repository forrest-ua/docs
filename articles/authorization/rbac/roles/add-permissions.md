---
title: Add Permissions to Roles
description: Learn how to add permissions to roles using either the Auth0 Dashboard or the Auth0 Management API.
topics:
  - authorization
  - mgmt-api
  - roles
  - permissions
contentType: 
    - how-to
useCase:
  - build-an-app
  - call-api
  - secure-api
---
# Add Permissions to Roles

In this guide, you'll learn how to add permissions to roles from the Auth0 Dashboard or with the Management API.

<%= include('../../_includes/_enable-authz-core') %>

## From the Dashboard

To add permissions to roles from the Dashboard:

1. Navigate to the [Users & Roles > Roles](${manage_url}/#/roles) page in the [Auth0 Dashboard](${manage_url}/), and click the name of the role to view.

![Click Create Role](/media/articles/authorization/role-list-added.png)

2. Click the **Permissions** tab, then click **Add Permissions**.

![Add Permissions](/media/articles/authorization/role-def-empty-permissions.png)

3. Select the API from which you want to assign permissions, then select the permissions to add to the role, and click **Add Permissions**.

![Add Permissions to Roles](/media/articles/authorization/role-select-add-permissions.png)

## Using the Management API

To add permissions to roles with the Management API, make a `POST` request to the [Add Role Permissions endpoint](/api/management/v2#!/roles/post_role_permissions). Be sure to replace `ROLE_ID`, `MGMT_API_ACCESS_TOKEN`, `API_IDENTIFIER`, and `PERMISSION_NAME` placeholder values with your role ID, Management API Access Token, API identifier (audience), and permission name(s), respectively.

```har
{
	"method": "POST",
	"url": "https://${account.namespace}/api/v2/roles/ROLE_ID/permissions",
  "headers": [
    { "name": "Content-Type", "value": "application/json" },
    { "name": "Authorization", "value": "Bearer MGMT_API_ACCESS_TOKEN" },
    { "name": "Cache-Control", "value": "no-cache" }
	],
	"postData": {
    "mimeType": "application/json",
    "text": "{ \"permissions\": [ { \"resource_server_identifier\": \"API_IDENTIFIER\", \"permission_name\": \"PERMISSION_NAME\" }, { \"resource_server_identifier\": \"API_IDENTIFIER\", \"permission_name\": \"PERMISSION_NAME\" } ] }"
  }
}
```

| **Value** | **Description** |
| - | - |
| `ROLE_ID` | Τhe ID of the role for which you want to add permissions. |
| `MGMT_API_ACCESS_TOKEN`  | [Access Token for the Management API](/api/management/v2/tokens) with the <dfn data-key="scope">scope</dfn> `update:roles`. |
| `API_IDENTIFIER` | This is the identifier of the API associated with the permission(s) you would like to add for the specified role, otherwise known as the audience. This is not the API ID. |
| `PERMISSION_NAME` | Name(s) of the permission(s) you would like to add for the specified role. |