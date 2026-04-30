---
title: Business-Scoped User IDs API & Webhook Updates
deprecated: false
hidden: false
metadata:
  robots: index
---
WhatsApp will launch a [Usernames feature](https://developers.facebook.com/documentation/business-messaging/whatsapp/business-scoped-user-ids?) later this year. When enabled by users, phone numbers might not be included in Message Webhooks.

In response to this adjustment, Omnichat will update the following Webhooks and Open API formats.

**Any changes described in this document are subject to change.** Please refer to the [Change Log](https://developers.omnichat.ai/docs/business-scoped-user-ids-api-webhook-updates#change-log) for the latest updates.

# Omnichat Webhooks

BSUIDs will begin appearing in webhooks in early May 2026.

## customer/create and customer/update

`bsuid` is added inside each entry of the `socialContacts` array for WhatsApp contacts.

### Updated: Customer's social channel contact information

| Field     | Description                                                                                               | Type       | Nullable             |
| :-------- | :-------------------------------------------------------------------------------------------------------- | :--------- | :------------------- |
| platform  | Platform name. Possible values: line, facebook, instagram, or whatsapp                                    | String     |                      |
| channelId | Channel ID / WhatsApp Business Phone Number                                                               | String     |                      |
| userId    | Social Messenger Channel User ID (LINE User ID / Facebook PSID / Instagram IGSID / WhatsApp Phone Number) | String     | **Yes for WhatsApp** |
| **bsuid** | **WhatsApp Business-Scoped User ID**                                                                      | **String** | **Yes**              |

### Updated JSON example

```json
{
  "memberId": "bruce001",
  "omniCustomerId": "67c7f3a056c62166b9cdaab8",
  "email": "bruce.ni@omnichat.ai",
  "phone": "886987654321",
  "name": "Bruce Ni",
  "tags": [
    "FB keyword auto reply add tag"
  ],
  "customAttributes": [
    {
      "key": "membership_tier",
      "value": "Bronze"
    }
  ],
  "socialContacts": [
    {
      "platform": "whatsapp",
      "channelId": "85298765432",
      "userId": "8526543210",    // CHANGED: may be null when WhatsApp user enables Username feature 
      "bsuid": "US.13491208655302741918"    // ADDED
    }
  ],
  "createdAt": "2023-11-09T14:09:57.511+08:00",
  "updatedAt": "2023-11-09T17:53:08.734+08:00"
}
```

<br />

## customer/channel_subscribe and customer/channel_unsubscribe

`bsuid` is added as a top-level field for WhatsApp subscribe / unsubscribe events.

### Updated Data Change Object Structure

| Field     | Description                                                                                    | Type       | Nullable             |
| :-------- | :--------------------------------------------------------------------------------------------- | :--------- | :------------------- |
| memberId  | Customer's unique ID                                                                           | String     |                      |
| email     | Customer's email                                                                               | String     |                      |
| phone     | Customer's phone                                                                               | String     |                      |
| name      | Customer's name                                                                                | String     |                      |
| platform  | Contact platform name. Possible values: **line**, **facebook**, **instagram**, or **whatsapp** | String     |                      |
| channelId | Contact channel ID / WABA Phone Number (WhatsApp)                                              | String     |                      |
| userId    | Contact user ID / User Phone Number (WhatsApp)                                                 | String     | **Yes for WhatsApp** |
| **bsuid** | **WhatsApp Business-Scoped User ID**                                                           | **String** | **Yes**              |

### Updated JSON example

```json
{
  "memberId": "bruce001",
  "email": "bruce.ni@omnichat.ai",
  "phone": "886987654321",  
  "name": "Bruce Ni",
  "platform": "whatsapp",
  "channelId": "85298765432",
  "userId": "8526543210",    // CHANGED: may be null when WhatsApp user enables Username feature
  "bsuid": "US.13491208655302741918"    // ADDED
}
```

<br />

## customer/channel_omo_binding

`bsuid` is added as a top-level field for WhatsApp OMO binding events.

### Updated Data Change Object Structure

| Field             | Description                                                 | Type       | Nullable             |
| :---------------- | :---------------------------------------------------------- | :--------- | :------------------- |
| platform          | Messaging Platform. Supported values: `line`, `whatsapp`    | String     |                      |
| channelId         | Messaging Platform Channel ID                               | String     |                      |
| userId            | Customer's User ID (LINE User ID / WhatsApp Phone Number)   | String     | **Yes for WhatsApp** |
| **bsuid**         | **WhatsApp Business-Scoped User ID**                        | **String** | **Yes**              |
| memberId          | Customer's unique ID                                        | String     | Yes                  |
| email             | Customer's email                                            | String     | Yes                  |
| phone             | Customer's phone                                            | String     | Yes                  |
| agentId           | The agent's system ID                                       | String     | Yes                  |
| agentName         | The agent name of the agent bound to the customer           | String     | Yes                  |
| agentEmail        | The Omnichat login email of the agent bound to the customer | String     | Yes                  |
| agentPhone        | The Omnichat login phone of the agent bound to the customer | String     | Yes                  |
| agentEmployeeCode | The employee code of the agent bound to the customer        | String     | Yes                  |
| agentLocationName | The shop location name of the agent bound to the customer   | String     | Yes                  |
| agentLocationCode | The shop location code of the agent bound to the customer   | String     | Yes                  |
| agentPhotoUrl     | The agent's photo                                           | String     | Yes                  |

### Updated JSON example

```json
{
  "platform": "whatsapp",
  "channelId": "85298765432",
  "userId": "8526543210",    // CHANGED: may be null when WhatsApp user enables Username feature
  "bsuid": "US.13491208655302741918",    // ADDED
  "memberId": "bruce001",
  "email": "bruce.ni@omnichat.ai",
  "phone": "886987654321",
  "agentName": "John Doe",
  "agentEmail": "john.doe@example.com",
  "agentPhone": "85256785678",
  "agentEmployeeCode": "S0001",
  "agentLocationName": "Shop A",
  "agentLocationCode": "SHOP-A",
  "agentPhotoUrl": "https://media-cdn.omnichat.ai/your_image.png"
}
```

<br />

## direct_msg/status

`bsuid` is added as a top-level field for WhatsApp Direct Message status events.

### Updated Data Change Object Structure

| Field      | Description                                                                                    | Type       | Nullable             |
| :--------- | :--------------------------------------------------------------------------------------------- | :--------- | :------------------- |
| trackId    | Message track ID                                                                               | String     |                      |
| messageIds | Message IDs                                                                                    | Array      |                      |
| platform   | Contact platform name. Possible values: **line**, **facebook**, **instagram**, or **whatsapp** | String     |                      |
| channelId  | Contact channel ID / WABA Phone Number (WhatsApp)                                              | String     |                      |
| userId     | Contact user ID / User Phone Number (WhatsApp)                                                 | String     | **Yes for WhatsApp** |
| memberId   | Customer's unique ID                                                                           | String     |                      |
| email      | Customer's email                                                                               | String     |                      |
| phone      | Customer's phone                                                                               | String     |                      |
| status     | Message status                                                                                 | String     |                      |
| **bsuid**  | **WhatsApp Business-Scoped User ID. Only present for WhatsApp**                                | **String** | **Yes**              |

### Updated JSON example

```json
{
  "trackId": "testing-event",
  "messageIds": [
    "testing-message-id"
  ],
  "platform": "whatsapp",
  "channelId": "85298765432",
  "userId": "8526543210",		// CHANGED: may be null when WhatsApp user enables Username feature 
  "memberId": "bruce001",
  "email": "bruce.ni@omnichat.ai",
  "phone": "886987654321",
  "status": "delivered",
  "bsuid": "US.13491208655302741918"    // ADDED
}
```

<br />

## whatsapp_flow/flow_create

`bsuid` is added as a top-level field when customers complete a WhatsApp Flow form.

### Updated Data Change Object Structure

| Field        | Description                                                                                                                                                                            | Type       | Nullable |
| :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------- | :------- |
| name         | Customer's name                                                                                                                                                                        | String     | Yes      |
| phone        | Customer's phone                                                                                                                                                                       | String     | **Yes**  |
| **bsuid**    | **WhatsApp Business-Scoped User ID**                                                                                                                                                   | **String** | **Yes**  |
| flowId       | WhatsApp flow's ID                                                                                                                                                                     | String     |          |
| flowName     | WhatsApp flow's Name                                                                                                                                                                   | String     |          |
| responseTime | Customer response time                                                                                                                                                                 | String     |          |
| flowResponse | The original response from WhatsApp. See `interactive.nfm_reply.response_json` in the [Meta Official Doc](https://developers.facebook.com/docs/whatsapp/flows/reference/flowswebhooks) | Object     |          |

### Updated JSON example

```json
{
  "name": "Omnichat",
  "phone": "85261234567",		// CHANGED: may be null when WhatsApp user enables Username feature 
  "bsuid": "US.13491208655302741918",    // ADDED
  "flowId": "1234567890",
  "flowName": "Example Flow",
  "responseTime": "2024-07-01T17:42:24.333+08:00",
  "flowResponse": {
    "Example Column 1": ["0", "1", "2"],
    "Example Column 2": ["0"]
  }
}
```

<br />

## ticket/create, ticket/update

`bsuid` is added as a top-level field for WhatsApp ticket events.

### Updated Data Change Object Structure

| Field               | Description                                                                        | Type       | Nullable             |
| :------------------ | :--------------------------------------------------------------------------------- | :--------- | :------------------- |
| ticketId            | A sequence number                                                                  | Integer    |                      |
| subject             | The subject of this ticket                                                         | String     |                      |
| customerName        | Customer's name                                                                    | String     |                      |
| isGroupChat         | Flag used to determine if the ticket is related to a group chat                    | Boolean    |                      |
| isCollaborationChat | Flag used to determine if the ticket is related to a collaboration chat            | Boolean    |                      |
| platform            | Supported values: `webchat`, `line`, `whatsapp`, `wechat`, `instagram`, `facebook` | String     |                      |
| channelId           | Contact channel ID / WABA Phone Number (WhatsApp)                                  | String     |                      |
| userId              | Contact user ID / User Phone Number (WhatsApp)                                     | String     | **Yes for WhatsApp** |
| **bsuid**           | **WhatsApp Business-Scoped User ID. Only present for WhatsApp**                    | **String** | **Yes**              |
| status              | Supported values: `Open`, `InProgress`, `Closed`                                   | String     |                      |
| createdAt           | Creation time                                                                      | String     |                      |
| closedAt            | Closed time when the ticket status is `Closed`. Always `null` for `ticket/create`  | String     | Yes                  |
| firstFollowUpAt     | First follow-up time                                                               | String     |                      |
| firstResponseAt     | The first response time of this ticket                                             | String     |                      |
| agentLogs           | List of Agent Logs. Default is an empty array                                      | Array      |                      |

### Updated JSON example — create

```json
{
  "ticketId": 123,
  "subject": "2025-02-10 13:54:56",
  "customerName": "Omnichat",
  "isGroupChat": false,
  "isCollaborationChat": false,
  "platform": "whatsapp",
  "channelId": "85298765432",		
  "userId": "8526543210",		// CHANGED: may be null when WhatsApp user enables Username feature 
  "bsuid": "US.13491208655302741918",    // ADDED
  "status": "Open",
  "createdAt": "2025-02-13T13:54:56.848+08:00",
  "closedAt": null,
  "firstFollowUpAt": "2025-02-10T13:54:56.848+08:00",
  "firstResponseAt": "2025-02-10T13:55:23.184+08:00",
  "agentLogs": [
    {
      "agentId": "8fc7e9e3-f742-4772-b918-02180f4a4403",
      "agentName": "Chris Sales",
      "actionType": "FOLLOW_UP_FROM_OPEN",
      "occurredAt": "2025-02-10T13:54:56.869+08:00"
    }
  ]
}
```

<br />

# Open API

Send Direct Message, Send Broadcast, and WhatsApp Headless APIs will be supported by June. All other APIs will be supported by mid-to-late May.

**We will provide detailed information soon.**

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

**API doc:** [https://documenter.getpostman.com/view/2s9YsMBC4o#9ea26161-d084-48cc-9b6c-43a378562246](https://documenter.getpostman.com/view/2s9YsMBC4o#9ea26161-d084-48cc-9b6c-43a378562246)

`bsuid` is added as a request field for WhatsApp events.

### Updated Request Object Structure

| Field                 | Description                                                                                            | Type       | Nullable             |
| :-------------------- | :----------------------------------------------------------------------------------------------------- | :--------- | :------------------- |
| platform              | Messaging Platform identifier. Possible values: `line`, `facebook`, `instagram`, `whatsapp`, `webchat` | String     |                      |
| channelId             | Specific Messaging Platform Channel ID                                                                 | String     |                      |
| userId                | Specific Messaging Platform Channel User ID / User Phone Number (WhatsApp)                             | String     | **Yes for WhatsApp** |
| **bsuid**             | **WhatsApp Business-Scoped User ID. Only present for WhatsApp.**                                       | **String** | **Yes**              |
| agentEmail            | Agent login email in Omnichat                                                                          | String     | Yes                  |
| agentPhone            | Agent login phone in Omnichat                                                                          | String     | Yes                  |
| agentEmployeeCode     | Agent employee code (Only for salesperson / sales manager agent user)                                  | String     | Yes                  |
| agentShopLocationCode | Agent shop location code                                                                               | String     | Yes                  |

### Updated JSON example

```json
{
  "platform": "whatsapp",
  "channelId": "85298765432",
  "userId": "8526543210",    // CHANGED: may be null when a WhatsApp user enables Username feature
  "bsuid": "US.13491208655302741918",    // ADDED
  "agentEmail": "john.doe@example.com"
}
```

<br />

### Unassign collaborator

<br />

## Messaging API

### Get chat history

### Get message details

### Send direct message

<br />

## Broadcast API

### Get broadcast recipient list response

**API doc:** [https://documenter.getpostman.com/view/2s9YsMBC4o#22901cfb-0713-40a8-bad1-a8fa15423ad3](https://documenter.getpostman.com/view/2s9YsMBC4o#22901cfb-0713-40a8-bad1-a8fa15423ad3)

`bsuid` is added to each recipient item in the broadcast recipients response for WhatsApp contacts.

### Updated Response Object Structure

| Field       | Description                                                     | Type       | Nullable |
| :---------- | :-------------------------------------------------------------- | :--------- | :------- |
| name        | Recipient's name                                                | String     |          |
| phone       | Recipient's phone number                                        | String     | Yes      |
| **bsuid**   | **WhatsApp Business-Scoped User ID. Only present for WhatsApp** | **String** | **Yes**  |
| success     | Whether the message was sent successfully                       | Boolean    |          |
| sentAt      | Sent time                                                       | String     |          |
| read        | Whether the message has been read                               | Boolean    |          |
| readAt      | Read time                                                       | String     |          |
| clicked     | Whether the message has been clicked                            | Boolean    |          |
| clickedAt   | Clicked time                                                    | String     |          |
| responded   | Whether the recipient has responded                             | Boolean    |          |
| respondedAt | Responded time                                                  | String     |          |
| messageId   | Message ID                                                      | String     |          |
| error       | Error message                                                   | String     |          |

### Updated JSON example

```json
{
  "name": "Bruce Ni",
  "phone": "8526543210",	// CHANGED: may be null when a WhatsApp user enables Username feature 
  "bsuid": "US.13491208655302741918",    // ADDED
  "success": true,
  "sentAt": "2025-04-28T10:30:00.000+08:00",
  "read": true,
  "readAt": "2025-04-28T10:32:15.000+08:00",
  "clicked": false,
  "clickedAt": null,
  "responded": false,
  "respondedAt": null,
  "messageId": "wamid.ABGGFlCGg0cvAgo-sJQh43L5Pe4W",
  "error": null
}
```

<br />

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

| Date       | Change                                                                                                                                                                                                                                                         |
| :--------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2026/05/06 | Added `bsuid` field to `customer/create`, `customer/update`, `customer/channel_subscribe`, `customer/channel_unsubscribe`, `customer/channel_omo_binding`, `direct_msg/status`, `whatsapp_flow/flow_create`, `ticket/create`, `ticket/update` webhook payloads |

<br />
