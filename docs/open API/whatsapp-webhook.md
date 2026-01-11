---
title: WhatsApp Message Webhook
deprecated: false
hidden: false
metadata:
  robots: index
---
# WhatsApp Message Webhook

Webhook events for WhatsApp messages. These are reference payloads for developers integrating with WhatsApp webhooks.

---

# Webhook Payload Structure

WhatsApp webhooks follow the Meta webhook format.

## Base Structure

```json
{
  "object": "whatsapp_business_account",
  "entry": [
    {
      "id": "{{WHATSAPP-BUSINESS-ACCOUNT-ID}}",
      "changes": [
        {
          "value": {
            "messaging_product": "whatsapp",
            "metadata": {
              "display_phone_number": "{{BUSINESS-PHONE-NUMBER}}",
              "phone_number_id": "{{BUSINESS-PHONE-NUMBER-ID}}"
            },
            ...
          },
          "field": "messages"
        }
      ]
    }
  ]
}
```

---

# Message Status Webhook

Webhook for message delivery status updates.

## Status Types

| Status | Description |
| :----- | :---------- |
| sent | Message is being sent |
| delivered | Message delivered to recipient's phone |
| read | Message read by recipient |
| failed | Message failed to send |

## Payload Example

### Message Sent

```json
{
  "object": "whatsapp_business_account",
  "entry": [
    {
      "id": "123456789",
      "changes": [
        {
          "value": {
            "messaging_product": "whatsapp",
            "metadata": {
              "display_phone_number": "85290000001",
              "phone_number_id": "123456789"
            },
            "statuses": [
              {
                "id": "wamid.HBgLODUyOTAzNTQ1MzM...",
                "status": "sent",
                "timestamp": "1604647464",
                "recipient_id": "85260000001"
              }
            ]
          },
          "field": "messages"
        }
      ]
    }
  ]
}
```

### Message Delivered

```json
{
  "object": "whatsapp_business_account",
  "entry": [
    {
      "id": "123456789",
      "changes": [
        {
          "value": {
            "messaging_product": "whatsapp",
            "metadata": {
              "display_phone_number": "85290000001",
              "phone_number_id": "123456789"
            },
            "statuses": [
              {
                "id": "wamid.HBgLODUyOTAzNTQ1MzM...",
                "status": "delivered",
                "timestamp": "1604647465",
                "recipient_id": "85260000001"
              }
            ]
          },
          "field": "messages"
        }
      ]
    }
  ]
}
```

### Message Read

```json
{
  "object": "whatsapp_business_account",
  "entry": [
    {
      "id": "123456789",
      "changes": [
        {
          "value": {
            "messaging_product": "whatsapp",
            "metadata": {
              "display_phone_number": "85290000001",
              "phone_number_id": "123456789"
            },
            "statuses": [
              {
                "id": "wamid.HBgLODUyOTAzNTQ1MzM...",
                "status": "read",
                "timestamp": "1604647470",
                "recipient_id": "85260000001"
              }
            ]
          },
          "field": "messages"
        }
      ]
    }
  ]
}
```

### Message Failed

```json
{
  "object": "whatsapp_business_account",
  "entry": [
    {
      "id": "123456789",
      "changes": [
        {
          "value": {
            "messaging_product": "whatsapp",
            "metadata": {
              "display_phone_number": "85290000001",
              "phone_number_id": "123456789"
            },
            "statuses": [
              {
                "id": "wamid.HBgLODUyOTAzNTQ1MzM...",
                "status": "failed",
                "timestamp": "1604647464",
                "recipient_id": "85260000001",
                "errors": [
                  {
                    "code": 131047,
                    "title": "Re-engagement message",
                    "message": "More than 24 hours have passed since the recipient last replied to the sender number."
                  }
                ]
              }
            ]
          },
          "field": "messages"
        }
      ]
    }
  ]
}
```

---

# Incoming Message Webhook

Webhook for incoming messages from customers.

## Payload Example

### Text Message

```json
{
  "object": "whatsapp_business_account",
  "entry": [
    {
      "id": "123456789",
      "changes": [
        {
          "value": {
            "messaging_product": "whatsapp",
            "metadata": {
              "display_phone_number": "85290000001",
              "phone_number_id": "123456789"
            },
            "contacts": [
              {
                "profile": {
                  "name": "Customer Name"
                },
                "wa_id": "85260000001"
              }
            ],
            "messages": [
              {
                "from": "85260000001",
                "id": "wamid.HBgLODUyOTAzNTQ1MzM...",
                "timestamp": "1604647464",
                "type": "text",
                "text": {
                  "body": "Hello, I need help!"
                }
              }
            ]
          },
          "field": "messages"
        }
      ]
    }
  ]
}
```

### Image Message

```json
{
  "object": "whatsapp_business_account",
  "entry": [
    {
      "id": "123456789",
      "changes": [
        {
          "value": {
            "messaging_product": "whatsapp",
            "metadata": {
              "display_phone_number": "85290000001",
              "phone_number_id": "123456789"
            },
            "messages": [
              {
                "from": "85260000001",
                "id": "wamid.HBgLODUyOTAzNTQ1MzM...",
                "timestamp": "1604647464",
                "type": "image",
                "image": {
                  "id": "123456789",
                  "mime_type": "image/jpeg",
                  "sha256": "abc123...",
                  "caption": "Product photo"
                }
              }
            ]
          },
          "field": "messages"
        }
      ]
    }
  ]
}
```

## See Also

- [WhatsApp Cloud API - Webhooks](https://developers.facebook.com/docs/whatsapp/cloud-api/webhooks)
