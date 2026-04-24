---
title: Business-Scoped User IDs API & Webhook Updates
deprecated: false
hidden: false
metadata:
  robots: index
---
WhatsApp will launch a [Usernames](https://developers.facebook.com/documentation/business-messaging/whatsapp/business-scoped-user-ids?) feature later this year. When enabled by users, phone numbers might not be included in Message Webhooks.

In response to this adjustment, Omnichat will update the following Webhooks and Open API formats.

**Any changes described in this document are subject to change.** Please refer to the Change Log for the latest updates.

# Omnichat Webhooks

## customer/create, customer/update

## customer/channel_subscribe, customer/channel_unsubscribe

## customer/channel_omo_binding

## direct_msg/status

## whatsapp_flow/flow_create

## ticket/create, ticket/update

<br />

# Open API

## Contacts API

### Get contacts

### Upsert a Contact

### Delete Contact by User ID

<br />

## Customers API

### Get customer detail by member ID

<br />

## Tag API

### Get tagging log records

<br />

## Rooms API

### Assign follow up agent

### Assign collaborator

### Unassign agent

### Unassign collaborator

<br />

## Messaging API

### Get chat history

### Get message details

### Send direct message

<br />

## Broadcast API

### Get broadcast recipient list

### Send broadcast

<br />

## WhatsApp Headless API

The format changes align with the official WhatsApp BSUID specifications. Please refer to this document for detailed information.

* [Send message requests](https://developers.facebook.com/documentation/business-messaging/whatsapp/business-scoped-user-ids/?locale=en_US#send-message-requests)
* [Send message response](https://developers.facebook.com/documentation/business-messaging/whatsapp/business-scoped-user-ids/?locale=en_US#send-message-response)
* [Send marketing message requests](https://developers.facebook.com/documentation/business-messaging/whatsapp/business-scoped-user-ids/?locale=en_US#send-marketing-message-requests)
* [Send marketing message response](https://developers.facebook.com/documentation/business-messaging/whatsapp/business-scoped-user-ids/?locale=en_US#send-marketing-message-response)

# WhatsApp Message Webhook Forward

The format changes align with the official WhatsApp BSUID specifications. Please refer to this document for detailed information.

* [Status messages webhooks](https://developers.facebook.com/documentation/business-messaging/whatsapp/business-scoped-user-ids/?locale=en_US#status-messages-webhooks)
* [Incoming messages webhooks](https://developers.facebook.com/documentation/business-messaging/whatsapp/business-scoped-user-ids/?locale=en_US#incoming-messages-webhooks-1)

# Change Log

2026/05/06 Add bsuid in the Omnichat Webhooks

<br />
