---
title: Meta Business APIs
deprecated: false
hidden: false
metadata:
  robots: index
---
# Meta Business APIs

APIs for Meta (Facebook/WhatsApp) business operations.

---

# Upload Public Key

Upload a public key for WhatsApp Business encryption.

## Endpoint

**POST** `https://open-api.omnichat.ai/v1/whatsapp-business/public-key`

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
      <td>phone</td>
      <td>String</td>
      <td>Yes</td>
      <td>WhatsApp Business phone number</td>
    </tr>
    <tr>
      <td>businessPublicKey</td>
      <td>String</td>
      <td>Yes</td>
      <td>Public key for encryption</td>
    </tr>
  </tbody>
</Table>

## Response

**Success** - HTTP Status 200 with empty response body

**Error** - HTTP Status 4xx / 5xx

```json
{
  "errorCode": "INVALID_REQUEST_BODY",
  "message": "Invalid request body"
}
```

## Example Request

```json
{
  "phone": "85298765432",
  "businessPublicKey": "-----BEGIN PUBLIC KEY-----\nMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA...\n-----END PUBLIC KEY-----"
}
```
