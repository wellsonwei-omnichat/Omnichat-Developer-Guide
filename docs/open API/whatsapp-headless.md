---
title: WhatsApp Headless
deprecated: false
hidden: false
metadata:
  robots: index
---
# WhatsApp Headless

APIs for sending WhatsApp messages directly without tracking. This is a passthrough API to WhatsApp Cloud API.

## Subscription Required

- WhatsApp Headless API Module

---

# Send Message

Send a WhatsApp message directly to a recipient.

## Endpoint

**POST** `https://open-api.omnichat.ai/v1/whatsapp/headless-api/{business-phone-number}/messages`

## Request Headers

| Header | Value | Description |
| :----- | :---- | :---------- |
| Authorization | Bearer \{API_TOKEN\} | API Token from Omnichat |
| Content-Type | application/json | - |

## Path Parameters

| Parameter | Type | Required | Description |
| :-------- | :--- | :------- | :---------- |
| business-phone-number | String | Yes | WhatsApp Business phone number |

## Request Body

The request body follows the [WhatsApp Cloud API message format](https://developers.facebook.com/docs/whatsapp/cloud-api/reference/messages).

## Supported Message Types

| Type | Description |
| :--- | :---------- |
| text | Plain text message |
| image | Image message by URL |
| audio | Audio message by URL |
| video | Video message by URL |
| document | Document message by URL |
| sticker | Sticker message by URL |
| location | Location message |
| template | Template message (text, media, interactive) |
| interactive | Interactive message (list, buttons) |

## Examples

### Send Text Message

```json
{
  "messaging_product": "whatsapp",
  "recipient_type": "individual",
  "to": "85260000001",
  "type": "text",
  "text": {
    "preview_url": false,
    "body": "Hello, this is a test message!"
  }
}
```

### Send Text Message with Preview URL

```json
{
  "messaging_product": "whatsapp",
  "recipient_type": "individual",
  "to": "85260000001",
  "type": "text",
  "text": {
    "preview_url": true,
    "body": "Check out this link: https://example.com"
  }
}
```

### Send Image Message

```json
{
  "messaging_product": "whatsapp",
  "recipient_type": "individual",
  "to": "85260000001",
  "type": "image",
  "image": {
    "link": "https://example.com/image.png",
    "caption": "Image caption"
  }
}
```

### Send Video Message

```json
{
  "messaging_product": "whatsapp",
  "recipient_type": "individual",
  "to": "85260000001",
  "type": "video",
  "video": {
    "link": "https://example.com/video.mp4",
    "caption": "Video caption"
  }
}
```

### Send Document Message

```json
{
  "messaging_product": "whatsapp",
  "recipient_type": "individual",
  "to": "85260000001",
  "type": "document",
  "document": {
    "link": "https://example.com/document.pdf",
    "filename": "document.pdf",
    "caption": "Document caption"
  }
}
```

### Send Location Message

```json
{
  "messaging_product": "whatsapp",
  "recipient_type": "individual",
  "to": "85260000001",
  "type": "location",
  "location": {
    "latitude": 22.3193,
    "longitude": 114.1694,
    "name": "Hong Kong",
    "address": "Hong Kong, China"
  }
}
```

### Send Reply Button

```json
{
  "messaging_product": "whatsapp",
  "recipient_type": "individual",
  "to": "85260000001",
  "type": "interactive",
  "interactive": {
    "type": "button",
    "body": {
      "text": "Please select an option:"
    },
    "action": {
      "buttons": [
        { "type": "reply", "reply": { "id": "option1", "title": "Option 1" } },
        { "type": "reply", "reply": { "id": "option2", "title": "Option 2" } }
      ]
    }
  }
}
```

### Send List Message

```json
{
  "messaging_product": "whatsapp",
  "recipient_type": "individual",
  "to": "85260000001",
  "type": "interactive",
  "interactive": {
    "type": "list",
    "header": {
      "type": "text",
      "text": "Select an item"
    },
    "body": {
      "text": "Please choose from the list below:"
    },
    "action": {
      "button": "View Options",
      "sections": [
        {
          "title": "Section 1",
          "rows": [
            { "id": "item1", "title": "Item 1", "description": "Description 1" },
            { "id": "item2", "title": "Item 2", "description": "Description 2" }
          ]
        }
      ]
    }
  }
}
```

### Send Template Message (Text)

```json
{
  "messaging_product": "whatsapp",
  "recipient_type": "individual",
  "to": "85260000001",
  "type": "template",
  "template": {
    "name": "hello_world",
    "language": {
      "code": "en_US"
    }
  }
}
```

### Send Template Message with Media Header

```json
{
  "messaging_product": "whatsapp",
  "recipient_type": "individual",
  "to": "85260000001",
  "type": "template",
  "template": {
    "name": "marketing_template",
    "language": {
      "code": "en_US"
    },
    "components": [
      {
        "type": "header",
        "parameters": [
          {
            "type": "image",
            "image": {
              "link": "https://example.com/header-image.png"
            }
          }
        ]
      },
      {
        "type": "body",
        "parameters": [
          { "type": "text", "text": "John Doe" },
          { "type": "text", "text": "50%" }
        ]
      }
    ]
  }
}
```

## Response

The response follows the WhatsApp Cloud API response format.

### Success Response

```json
{
  "messaging_product": "whatsapp",
  "contacts": [
    {
      "input": "85260000001",
      "wa_id": "85260000001"
    }
  ],
  "messages": [
    {
      "id": "wamid.HBgLODUyOTAzNTQ1MzMVAgARGBI..."
    }
  ]
}
```

## See Also

- [WhatsApp Cloud API - Messages](https://developers.facebook.com/docs/whatsapp/cloud-api/reference/messages)
