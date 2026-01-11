---
title: Identity APIs
deprecated: false
hidden: false
metadata:
  robots: index
---
# Identity APIs

APIs for checking member data using social identity.

## Subscription Required

- CS / Marketing / OMO Sales / Social CDP Cloud
- CRM Open API Module

---

# Check Member Data using Social ID

Get member data by social identity (e.g., LINE User ID).

## Endpoint

**POST** `https://open-api.omnichat.ai/v1/identities/member-data`

## Request Headers

| Header | Value | Description |
| :----- | :---- | :---------- |
| Authorization | Bearer \{API_TOKEN\} | API Token from Omnichat |
| Content-Type | application/json | - |

## Request Body

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>Field</th>
      <th>Type</th>
      <th>Required</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>platform</td>
      <td>String</td>
      <td>Yes</td>
      <td>
        Messaging Platform.

        Supported values:
        - `line`
        - `facebook` (Not supported yet)
        - `whatsapp` (Not supported yet)
      </td>
    </tr>
    <tr>
      <td>channelId</td>
      <td>String</td>
      <td>Yes</td>
      <td>
        Messaging Platform Channel ID.

        - For LINE: LINE Messaging Channel ID
        - For Facebook: Facebook Page ID
        - For WhatsApp: WhatsApp Business Phone Number
      </td>
    </tr>
    <tr>
      <td>ids</td>
      <td>Array of String</td>
      <td>Yes</td>
      <td>
        Contact's User IDs. Max: 100

        - For LINE: LINE User ID
        - For Facebook: Facebook PSID
        - For WhatsApp: WhatsApp Phone Number
      </td>
    </tr>
  </tbody>
</Table>

## Response Body

| Field | Type | Description |
| :---- | :--- | :---------- |
| content | Array of `Check Identity Result` Object | Result data |
| totalElements | Integer | Total number of elements |

### `Check Identity Result` Object

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
      <td>id</td>
      <td>String</td>
      <td>The value you sent in the ids field of the API call</td>
    </tr>
    <tr>
      <td>memberId</td>
      <td>String</td>
      <td>The corresponding member ID of the user id. Returns `null` if no linked member ID</td>
    </tr>
  </tbody>
</Table>

### Success Response - HTTP Status 200

```json
{
  "content": [
    { "id": "U66a669e12ff66601c06e1dcd06e8f63c", "memberId": "1234" },
    { "id": "U1535b48edaae6ea9bf7408e4d08b3d41", "memberId": null }
  ],
  "totalElements": 2
}
```

### Error Response - HTTP Status 4xx / 5xx

```json
{
  "errorCode": "INVALID_REQUEST_BODY",
  "message": "Invalid request body"
}
```

## Example Request

```json
{
  "platform": "line",
  "channelId": "123456789",
  "ids": [
    "U66a669e12ff66601c06e1dcd06e8f63c",
    "U1535b48edaae6ea9bf7408e4d08b3d41"
  ]
}
```
