---
title: WhatsApp
deprecated: false
hidden: false
metadata:
  robots: index
---
# WhatsApp

APIs for managing WhatsApp message templates.

## Subscription Required

- Marketing Cloud / Social CDP Cloud
- Marketing Open API Module

---

# Get WhatsApp Templates

Get WhatsApp message templates for a specific business phone number.

## Endpoint

**GET** `https://open-api.omnichat.ai/v1/whatsapp-message-templates`

## Request Headers

| Header | Value | Description |
| :----- | :---- | :---------- |
| Authorization | Bearer \{API_TOKEN\} | API Token from Omnichat |

## Query Parameters

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>Parameter</th>
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
      <td>page</td>
      <td>Integer</td>
      <td>No</td>
      <td>Page number. Default: 1</td>
    </tr>
    <tr>
      <td>pageSize</td>
      <td>Integer</td>
      <td>No</td>
      <td>Number of templates per page. Default: 10, Max: 100</td>
    </tr>
  </tbody>
</Table>

## Response Body

| Field | Type | Description |
| :---- | :--- | :---------- |
| content | Array of `WhatsAppMessageTemplate` Object | List of templates |
| totalElements | Integer | Total number of templates |

### `WhatsAppMessageTemplate` Object

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
      <td>Template ID</td>
    </tr>
    <tr>
      <td>name</td>
      <td>String</td>
      <td>Template name</td>
    </tr>
    <tr>
      <td>language</td>
      <td>String</td>
      <td>Template language code (e.g., `zh_HK`, `en_US`)</td>
    </tr>
    <tr>
      <td>category</td>
      <td>String</td>
      <td>Template category: `UTILITY`, `MARKETING`, `AUTHENTICATION`</td>
    </tr>
    <tr>
      <td>status</td>
      <td>String</td>
      <td>Template status: `APPROVED`, `PENDING`, `REJECTED`</td>
    </tr>
    <tr>
      <td>components</td>
      <td>Array</td>
      <td>Template components (HEADER, BODY, FOOTER, BUTTONS)</td>
    </tr>
  </tbody>
</Table>

### Success Response - HTTP Status 200

```json
{
  "content": [
    {
      "id": "1029152384366117",
      "category": "UTILITY",
      "status": "APPROVED",
      "name": "pre_order_message",
      "language": "zh_HK",
      "components": [
        {
          "type": "BODY",
          "text": "親愛的顧客：\n\n感謝您於網店的訂購！\n\n有關您的訂單（訂單編號：{{1}}）中訂購了 {{2}}件數預售產品",
          "example": {
            "body_text": [["ORDER0001", "3"]]
          }
        }
      ]
    },
    {
      "id": "3862205883993025",
      "category": "MARKETING",
      "status": "APPROVED",
      "name": "autopush_eu",
      "language": "zh_HK",
      "components": [
        {
          "type": "BODY",
          "text": "多謝您的支持，請持續關注我們最新動態與優惠資訊。"
        },
        {
          "type": "BUTTONS",
          "buttons": [
            { "type": "QUICK_REPLY", "text": "立即預約測試" },
            { "type": "QUICK_REPLY", "text": "主目錄" },
            { "type": "QUICK_REPLY", "text": "專人服務" }
          ]
        }
      ]
    }
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

## Template Component Types

| Type | Description |
| :--- | :---------- |
| HEADER | Header content (TEXT, IMAGE, VIDEO, DOCUMENT) |
| BODY | Main message content with parameters |
| FOOTER | Footer text |
| BUTTONS | Action buttons (QUICK_REPLY, URL, PHONE_NUMBER) |

## See Also

- [WhatsApp Cloud API - Template Object](https://developers.facebook.com/docs/whatsapp/cloud-api/reference/messages#template-object)
