---
title: System Users
deprecated: false
hidden: false
metadata:
  robots: index
---
# System Users

APIs for retrieving system user information.

## Subscription Required

| Feature Toggle | Description |
|----------------|-------------|
| `open_api` | Open API Module - Required for retrieving system users |

---

# Get System Users List

Get the list of system users (agents/teammates) in your team.

## Endpoint

**GET** `https://open-api.omnichat.ai/v1/system-users`

## Request Headers

| Header | Value | Description |
| :----- | :---- | :---------- |
| Authorization | Bearer \{API_TOKEN\} | API Token from Omnichat |

## Response Body

| Field | Type | Description |
| :---- | :--- | :---------- |
| content | Array of `System User` Object | List of system users |

### `System User` Object

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>Field</th>
      <th>Type</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>team</td>
      <td>String</td>
      <td>Team name</td>
    </tr>
    <tr>
      <td>username</td>
      <td>String</td>
      <td>Internal username (UUID)</td>
    </tr>
    <tr>
      <td>name</td>
      <td>String</td>
      <td>Display name</td>
    </tr>
    <tr>
      <td>email</td>
      <td>String</td>
      <td>Email address</td>
    </tr>
    <tr>
      <td>phone</td>
      <td>String</td>
      <td>Phone number (nullable)</td>
    </tr>
    <tr>
      <td>profilePicture</td>
      <td>String</td>
      <td>Profile picture URL (nullable)</td>
    </tr>
    <tr>
      <td>available</td>
      <td>Boolean</td>
      <td>Whether user is available</td>
    </tr>
    <tr>
      <td>status</td>
      <td>Integer</td>
      <td>User status code</td>
    </tr>
    <tr>
      <td>role</td>
      <td>Integer</td>
      <td>User role code</td>
    </tr>
    <tr>
      <td>employeeCode</td>
      <td>String</td>
      <td>Employee code (nullable)</td>
    </tr>
    <tr>
      <td>shops</td>
      <td>Array</td>
      <td>Assigned shops (nullable)</td>
    </tr>
  </tbody>
</Table>

### `Shop` Object

| Field | Type | Description |
| :---- | :--- | :---------- |
| id | String | Shop ID |
| code | String | Shop code |
| name | String | Shop name |
| categories | Array | Shop categories |

### Success Response - HTTP Status 200

```json
{
  "content": [
    {
      "team": "Omnichat",
      "username": "1d9e3925-f08c-4236-92ef-b4c5394c9a14",
      "email": "john.doe@omnichat.ai",
      "phone": "+85212345678",
      "profilePicture": "https://media-cdn.omnichat.ai/upload/photos/user-upload-photo/1d9e3925-f08c-4236-92ef-b4c5394c9a14.png",
      "available": true,
      "status": 1,
      "role": 7,
      "name": "John Doe",
      "employeeCode": "E0001",
      "shops": [
        {
          "id": "60fd8409892243037e17f1d2",
          "code": "A01",
          "name": "Shop A01",
          "categories": []
        }
      ]
    },
    {
      "team": "Omnichat",
      "username": "e5255710-1701-4876-ac22-1d0da7f9291c",
      "email": "peter.pan@omnichat.ai",
      "phone": null,
      "profilePicture": null,
      "available": true,
      "status": 1,
      "role": 7,
      "name": "Peter Pan",
      "employeeCode": null,
      "shops": null
    }
  ]
}
```
