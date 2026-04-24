---
title: Business-Scoped User IDs API & Webhook Updates
deprecated: false
hidden: false
metadata:
  robots: index
---
Wh##atsApp will launch a Usernames feature later this year. When enabled by users, phone numbers might not be included in Message Webhooks.

In response to this adjustment, Omnichat will update the following Webhooks and Open API formats.

**Any changes described in this document are subject to change.** Please refer to the Change Log for the latest updates.

# Omnichat Webhooks

## customer/create, customer/update

<br />

## customer/channel_subscribe, customer/channel_unsubscribe

<br />

## customer/channel_omo_binding

<br />

## direct_msg/status

<br />

## whatsapp_flow/flow_create

<br />

## ticket/create, ticket/update

<br />

# Open API

## Contacts API

### Get contacts

<br />

### Upsert a Contact

### Delete Contact by User ID

## Customers API

### Get customer detail by member ID

## Tag API

https://open-api.omnichat.ai/v1/tagging-logs/records

### Get tagging log records

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

[https://open-api.omnichat.ai/v1/direct-messages](https://open-api.omnichat.ai/v1/direct-messages)

<br />

## Broadcast API

### Get broadcast recipient list

<br />

### Send broadcast 

[https://open-api.omnichat.ai/v1/broadcast](https://open-api.omnichat.ai/v1/broadcast)

<br />

## WhatsApp Headless API

<br />

# WhatsApp Message Webhook Forward

<br />

<br />

# Change Log

2026/05/06 Add bsuid in the Omnichat Webhook

<br />
