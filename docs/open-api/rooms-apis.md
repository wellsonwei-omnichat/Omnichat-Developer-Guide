---
title: Rooms APIs
excerpt: >-
  APIs for assigning and unassigning follow-up agents and collaborators to
  contacts.
---
# Assign Follow Up Agent

Assign a follow-up agent to a contact.

<Callout icon="⚠️" theme="warning">
If the target room is a collaboration room and the target agent role is not a CS role, the target agent must be assigned as a collaborator first. Call the [Assign Collaborator](#assign-collaborator) API before calling this endpoint.
</Callout>

**Subscription Required:**
- Customer Service Cloud / Social CDP Cloud
- CRM Open API Module

## Endpoint

**POST** [https://open-api.omnichat.ai/v1/rooms/assign-agent](https://open-api.omnichat.ai/v1/rooms/assign-agent)

## Headers

| Header        | Value                  |
| :------------ | :--------------------- |
| Authorization | Bearer `{{API-TOKEN}}` |

## Request Body

| Field                  | Type   | Required | Description                                                                                                                      |
| :--------------------- | :----- | :------- | :------------------------------------------------------------------------------------------------------------------------------- |
| platform               | String | Y        | Messaging platform. Supported values: `line`, `whatsapp`                                                                         |
| channelId              | String | Y        | Messaging platform Channel ID. For LINE → LINE Messaging Channel ID. For WhatsApp → WhatsApp Business Phone Number               |
| userId                 | String | Y        | Contact's User ID. For LINE → LINE User ID. For WhatsApp → WhatsApp Phone Number                                                 |
| agentEmail             | String | N        | Agent login email in Omnichat. *One of `agentEmail`, `agentPhone`, or `agentEmployeeCode` is required*                            |
| agentPhone             | String | N        | Agent login phone in Omnichat. *One of `agentEmail`, `agentPhone`, or `agentEmployeeCode` is required*                            |
| agentEmployeeCode      | String | N        | Agent employee code (salesperson / sales manager only). *One of `agentEmail`, `agentPhone`, or `agentEmployeeCode` is required*   |
| agentShopLocationCode  | String | N        | Agent shop location code. *Required if assigning to a salesperson / sales manager agent*                                          |

## Request Example

```json
{
    "platform": "whatsapp",
    "channelId": "85250000001",
    "userId": "85215022101325",
    "agentEmail": "agent001@example.com",
    "agentPhone": null,
    "agentEmployeeCode": "EM0001",
    "agentShopLocationCode": "SHOP02"
}
```

## Response Body

### Success - 204

Agent assigned successfully. Empty response body.

### Failed - 4xx / 5xx

```json
{
    "message": "OCE::<category>::<message>"
}
```

<br />

# Assign Collaborator

Assign a collaborator to a contact.

**Subscription Required:**
- Customer Service Cloud / Social CDP Cloud
- CRM Open API Module

## Endpoint

**POST** [https://open-api.omnichat.ai/v1/rooms/assign-collaborator](https://open-api.omnichat.ai/v1/rooms/assign-collaborator)

## Headers

| Header        | Value                  |
| :------------ | :--------------------- |
| Authorization | Bearer `{{API-TOKEN}}` |

## Request Body

| Field                  | Type   | Required | Description                                                                                                                      |
| :--------------------- | :----- | :------- | :------------------------------------------------------------------------------------------------------------------------------- |
| platform               | String | Y        | Messaging platform. Supported values: `line`, `whatsapp`                                                                         |
| channelId              | String | Y        | Messaging platform Channel ID. For LINE → LINE Messaging Channel ID. For WhatsApp → WhatsApp Business Phone Number               |
| userId                 | String | Y        | Contact's User ID. For LINE → LINE User ID. For WhatsApp → WhatsApp Phone Number                                                 |
| agentEmail             | String | N        | Agent login email in Omnichat. *One of `agentEmail`, `agentPhone`, or `agentEmployeeCode` is required*                            |
| agentPhone             | String | N        | Agent login phone in Omnichat. *One of `agentEmail`, `agentPhone`, or `agentEmployeeCode` is required*                            |
| agentEmployeeCode      | String | N        | Agent employee code. *One of `agentEmail`, `agentPhone`, or `agentEmployeeCode` is required*                                      |
| agentShopLocationCode  | String | N        | Agent shop location code. *Required if assigning to a salesperson / sales manager agent*                                          |

## Request Example

```json
{
    "platform": "whatsapp",
    "channelId": "85250000001",
    "userId": "85215022101325",
    "agentEmail": "agent001@example.com",
    "agentPhone": null,
    "agentEmployeeCode": "EM0001",
    "agentShopLocationCode": "SHOP02"
}
```

## Response Body

### Success - 204

Collaborator assigned successfully. Empty response body.

### Failed - 400 Bad Request

| Error Message                                                                        | Description                                                              |
| :----------------------------------------------------------------------------------- | :----------------------------------------------------------------------- |
| `OCE::BAD_REQUEST::userId is required`                                               | `userId` field is blank or missing                                       |
| `OCE::BAD_REQUEST::channelId is required`                                            | `channelId` field is blank or missing                                    |
| `OCE::BAD_REQUEST::platform is required`                                             | `platform` field is blank or missing                                     |
| `OCE::BAD_REQUEST::platform (xxx) is not supported yet`                              | The provided platform is not `line` or `whatsapp`                        |
| `OCE::BAD_REQUEST::team (xxx) is not supported to use Open API Customer Service`     | The team does not have `OPEN_API` or `OPEN_API_CUSTOMER_SERVICE` enabled |
| `OCE::BAD_REQUEST::At least one of agentEmail, agentPhone, or agentEmployeeCode must be provided` | All three agent identifier fields are blank               |
| `OCE::BAD_REQUEST::agentShopLocationCode is required when agentEmployeeCode is provided` | `agentEmployeeCode` was provided but `agentShopLocationCode` is missing |
| `OCE::BAD_REQUEST::Platform not found: xxx`                                          | Platform name does not match any known platform enum                     |
| `OCE::BAD_REQUEST::Channel not found: xxx`                                           | WhatsApp account not found for the given team and channel                |
| `OCE::BAD_REQUEST::WhatsappAccUserDoc not found: xxx`                                | WhatsApp user not found for the given team, channel, and telephone       |
| `OCE::BAD_REQUEST::No valid agent identifier provided`                               | No agent resolver could handle the provided agent identifiers            |
| `OCE::BAD_REQUEST::Unauthenticated access token`                                    | The provided token does not match the system API key                     |
| `OCE::BAD_REQUEST::Missing arkhamApiToken in systemSetting`                          | System setting `arkhamApiToken` is not configured                        |

### Failed - 500 Internal Server Error

| Error Message                              | Description               |
| :----------------------------------------- | :------------------------ |
| `OCE::INTERNAL_SERVER_ERROR::<message>`    | Unexpected server error   |

<br />

# Unassign Agent

Unassign a single sales role agent from a contact.

**Subscription Required:**
- Available for OMO teams only

## Endpoint

**POST** [https://open-api.omnichat.ai/v1/rooms/unassign-agent](https://open-api.omnichat.ai/v1/rooms/unassign-agent)

## Headers

| Header        | Value                  |
| :------------ | :--------------------- |
| Authorization | Bearer `{{API-TOKEN}}` |

## Request Body

| Field     | Type   | Required | Description                                                                                          |
| :-------- | :----- | :------- | :--------------------------------------------------------------------------------------------------- |
| platform  | String | Y        | Messaging platform. Supported values: `line`, `whatsapp`                                             |
| channelId | String | Y        | Messaging platform Channel ID. For LINE → LINE Messaging Channel ID. For WhatsApp → WhatsApp Business Phone Number |
| userId    | String | Y        | Contact's User ID. For LINE → LINE User ID. For WhatsApp → WhatsApp Phone Number                     |

## Request Example

```json
{
    "platform": "whatsapp",
    "channelId": "85250000001",
    "userId": "85215022101325"
}
```

## Response Body

### Success - 204

Agent unassigned successfully. Empty response body.

### Failed - 4xx / 5xx

```json
{
    "message": "OCE::<category>::<message>"
}
```

<br />

# Unassign Collaborator

Unassign a collaborator from a contact.

**Subscription Required:**
- Customer Service Cloud / Social CDP Cloud
- CRM Open API Module

## Endpoint

**POST** [https://open-api.omnichat.ai/v1/rooms/unassign-collaborator](https://open-api.omnichat.ai/v1/rooms/unassign-collaborator)

## Headers

| Header        | Value                  |
| :------------ | :--------------------- |
| Authorization | Bearer `{{API-TOKEN}}` |

## Request Body

| Field             | Type   | Required | Description                                                                                                        |
| :---------------- | :----- | :------- | :----------------------------------------------------------------------------------------------------------------- |
| platform          | String | Y        | Messaging platform. Supported values: `line`, `whatsapp`                                                           |
| channelId         | String | Y        | Messaging platform Channel ID. For LINE → LINE Messaging Channel ID. For WhatsApp → WhatsApp Business Phone Number |
| userId            | String | Y        | Contact's User ID. For LINE → LINE User ID. For WhatsApp → WhatsApp Phone Number                                   |
| agentEmail        | String | N        | Agent login email in Omnichat. *One of `agentEmail`, `agentPhone`, or `agentEmployeeCode` is required*              |
| agentPhone        | String | N        | Agent login phone in Omnichat. *One of `agentEmail`, `agentPhone`, or `agentEmployeeCode` is required*              |
| agentEmployeeCode | String | N        | Agent employee code. *One of `agentEmail`, `agentPhone`, or `agentEmployeeCode` is required*                        |

## Request Example

```json
{
    "platform": "whatsapp",
    "channelId": "85250000001",
    "userId": "85215022101325",
    "agentEmail": "agent001@example.com"
}
```

## Response Body

### Success - 204

Collaborator unassigned successfully. Empty response body.

### Failed - 400 Bad Request

| Error Message                                                                    | Description                                                              |
| :------------------------------------------------------------------------------- | :----------------------------------------------------------------------- |
| `OCE::BAD_REQUEST::userId is required`                                           | `userId` field is blank or missing                                       |
| `OCE::BAD_REQUEST::channelId is required`                                        | `channelId` field is blank or missing                                    |
| `OCE::BAD_REQUEST::platform is required`                                         | `platform` field is blank or missing                                     |
| `OCE::BAD_REQUEST::platform (xxx) is not supported yet`                          | The provided platform is not `line` or `whatsapp`                        |
| `OCE::BAD_REQUEST::team (xxx) is not supported to use Open API Customer Service` | The team does not have `OPEN_API` or `OPEN_API_CUSTOMER_SERVICE` enabled |
| `OCE::BAD_REQUEST::Platform not found: xxx`                                      | Platform name does not match any known platform enum                     |
| `OCE::BAD_REQUEST::Channel not found: xxx`                                       | WhatsApp account not found for the given team and channel                |
| `OCE::BAD_REQUEST::WhatsappAccUserDoc not found: xxx`                            | WhatsApp user not found for the given team, channel, and telephone       |
| `OCE::BAD_REQUEST::No valid agent identifier provided`                           | No agent resolver could handle the provided agent identifiers            |
| `OCE::BAD_REQUEST::Unauthenticated access token`                                 | The provided token does not match the system API key                     |
| `OCE::BAD_REQUEST::Missing arkhamApiToken in systemSetting`                      | System setting `arkhamApiToken` is not configured                        |

### Failed - 500 Internal Server Error

| Error Message                              | Description               |
| :----------------------------------------- | :------------------------ |
| `OCE::INTERNAL_SERVER_ERROR::<message>`    | Unexpected server error   |# Assign Follow Up Agent

Assign a follow-up agent to a contact.

<Callout icon="⚠️" theme="warning">
If the target room is a collaboration room and the target agent role is not a CS role, the target agent must be assigned as a collaborator first. Call the [Assign Collaborator](#assign-collaborator) API before calling this endpoint.
</Callout>

**Subscription Required:**
- Customer Service Cloud / Social CDP Cloud
- CRM Open API Module

## Endpoint

**POST** [https://open-api.omnichat.ai/v1/rooms/assign-agent](https://open-api.omnichat.ai/v1/rooms/assign-agent)

## Headers

| Header        | Value                  |
| :------------ | :--------------------- |
| Authorization | Bearer `{{API-TOKEN}}` |

## Request Body

| Field                  | Type   | Required | Description                                                                                                                      |
| :--------------------- | :----- | :------- | :------------------------------------------------------------------------------------------------------------------------------- |
| platform               | String | Y        | Messaging platform. Supported values: `line`, `whatsapp`                                                                         |
| channelId              | String | Y        | Messaging platform Channel ID. For LINE → LINE Messaging Channel ID. For WhatsApp → WhatsApp Business Phone Number               |
| userId                 | String | Y        | Contact's User ID. For LINE → LINE User ID. For WhatsApp → WhatsApp Phone Number                                                 |
| agentEmail             | String | N        | Agent login email in Omnichat. *One of `agentEmail`, `agentPhone`, or `agentEmployeeCode` is required*                            |
| agentPhone             | String | N        | Agent login phone in Omnichat. *One of `agentEmail`, `agentPhone`, or `agentEmployeeCode` is required*                            |
| agentEmployeeCode      | String | N        | Agent employee code (salesperson / sales manager only). *One of `agentEmail`, `agentPhone`, or `agentEmployeeCode` is required*   |
| agentShopLocationCode  | String | N        | Agent shop location code. *Required if assigning to a salesperson / sales manager agent*                                          |

## Request Example

```json
{
    "platform": "whatsapp",
    "channelId": "85250000001",
    "userId": "85215022101325",
    "agentEmail": "agent001@example.com",
    "agentPhone": null,
    "agentEmployeeCode": "EM0001",
    "agentShopLocationCode": "SHOP02"
}
```

## Response Body

### Success - 204

Agent assigned successfully. Empty response body.

### Failed - 4xx / 5xx

```json
{
    "message": "OCE::<category>::<message>"
}
```

<br />

# Assign Collaborator

Assign a collaborator to a contact.

**Subscription Required:**
- Customer Service Cloud / Social CDP Cloud
- CRM Open API Module

## Endpoint

**POST** [https://open-api.omnichat.ai/v1/rooms/assign-collaborator](https://open-api.omnichat.ai/v1/rooms/assign-collaborator)

## Headers

| Header        | Value                  |
| :------------ | :--------------------- |
| Authorization | Bearer `{{API-TOKEN}}` |

## Request Body

| Field                  | Type   | Required | Description                                                                                                                      |
| :--------------------- | :----- | :------- | :------------------------------------------------------------------------------------------------------------------------------- |
| platform               | String | Y        | Messaging platform. Supported values: `line`, `whatsapp`                                                                         |
| channelId              | String | Y        | Messaging platform Channel ID. For LINE → LINE Messaging Channel ID. For WhatsApp → WhatsApp Business Phone Number               |
| userId                 | String | Y        | Contact's User ID. For LINE → LINE User ID. For WhatsApp → WhatsApp Phone Number                                                 |
| agentEmail             | String | N        | Agent login email in Omnichat. *One of `agentEmail`, `agentPhone`, or `agentEmployeeCode` is required*                            |
| agentPhone             | String | N        | Agent login phone in Omnichat. *One of `agentEmail`, `agentPhone`, or `agentEmployeeCode` is required*                            |
| agentEmployeeCode      | String | N        | Agent employee code. *One of `agentEmail`, `agentPhone`, or `agentEmployeeCode` is required*                                      |
| agentShopLocationCode  | String | N        | Agent shop location code. *Required if assigning to a salesperson / sales manager agent*                                          |

## Request Example

```json
{
    "platform": "whatsapp",
    "channelId": "85250000001",
    "userId": "85215022101325",
    "agentEmail": "agent001@example.com",
    "agentPhone": null,
    "agentEmployeeCode": "EM0001",
    "agentShopLocationCode": "SHOP02"
}
```

## Response Body

### Success - 204

Collaborator assigned successfully. Empty response body.

### Failed - 400 Bad Request

| Error Message                                                                        | Description                                                              |
| :----------------------------------------------------------------------------------- | :----------------------------------------------------------------------- |
| `OCE::BAD_REQUEST::userId is required`                                               | `userId` field is blank or missing                                       |
| `OCE::BAD_REQUEST::channelId is required`                                            | `channelId` field is blank or missing                                    |
| `OCE::BAD_REQUEST::platform is required`                                             | `platform` field is blank or missing                                     |
| `OCE::BAD_REQUEST::platform (xxx) is not supported yet`                              | The provided platform is not `line` or `whatsapp`                        |
| `OCE::BAD_REQUEST::team (xxx) is not supported to use Open API Customer Service`     | The team does not have `OPEN_API` or `OPEN_API_CUSTOMER_SERVICE` enabled |
| `OCE::BAD_REQUEST::At least one of agentEmail, agentPhone, or agentEmployeeCode must be provided` | All three agent identifier fields are blank               |
| `OCE::BAD_REQUEST::agentShopLocationCode is required when agentEmployeeCode is provided` | `agentEmployeeCode` was provided but `agentShopLocationCode` is missing |
| `OCE::BAD_REQUEST::Platform not found: xxx`                                          | Platform name does not match any known platform enum                     |
| `OCE::BAD_REQUEST::Channel not found: xxx`                                           | WhatsApp account not found for the given team and channel                |
| `OCE::BAD_REQUEST::WhatsappAccUserDoc not found: xxx`                                | WhatsApp user not found for the given team, channel, and telephone       |
| `OCE::BAD_REQUEST::No valid agent identifier provided`                               | No agent resolver could handle the provided agent identifiers            |
| `OCE::BAD_REQUEST::Unauthenticated access token`                                    | The provided token does not match the system API key                     |
| `OCE::BAD_REQUEST::Missing arkhamApiToken in systemSetting`                          | System setting `arkhamApiToken` is not configured                        |

### Failed - 500 Internal Server Error

| Error Message                              | Description               |
| :----------------------------------------- | :------------------------ |
| `OCE::INTERNAL_SERVER_ERROR::<message>`    | Unexpected server error   |

<br />

# Unassign Agent

Unassign a single sales role agent from a contact.

**Subscription Required:**
- Available for OMO teams only

## Endpoint

**POST** [https://open-api.omnichat.ai/v1/rooms/unassign-agent](https://open-api.omnichat.ai/v1/rooms/unassign-agent)

## Headers

| Header        | Value                  |
| :------------ | :--------------------- |
| Authorization | Bearer `{{API-TOKEN}}` |

## Request Body

| Field     | Type   | Required | Description                                                                                          |
| :-------- | :----- | :------- | :--------------------------------------------------------------------------------------------------- |
| platform  | String | Y        | Messaging platform. Supported values: `line`, `whatsapp`                                             |
| channelId | String | Y        | Messaging platform Channel ID. For LINE → LINE Messaging Channel ID. For WhatsApp → WhatsApp Business Phone Number |
| userId    | String | Y        | Contact's User ID. For LINE → LINE User ID. For WhatsApp → WhatsApp Phone Number                     |

## Request Example

```json
{
    "platform": "whatsapp",
    "channelId": "85250000001",
    "userId": "85215022101325"
}
```

## Response Body

### Success - 204

Agent unassigned successfully. Empty response body.

### Failed - 4xx / 5xx

```json
{
    "message": "OCE::<category>::<message>"
}
```

<br />

# Unassign Collaborator

Unassign a collaborator from a contact.

**Subscription Required:**
- Customer Service Cloud / Social CDP Cloud
- CRM Open API Module

## Endpoint

**POST** [https://open-api.omnichat.ai/v1/rooms/unassign-collaborator](https://open-api.omnichat.ai/v1/rooms/unassign-collaborator)

## Headers

| Header        | Value                  |
| :------------ | :--------------------- |
| Authorization | Bearer `{{API-TOKEN}}` |

## Request Body

| Field             | Type   | Required | Description                                                                                                        |
| :---------------- | :----- | :------- | :----------------------------------------------------------------------------------------------------------------- |
| platform          | String | Y        | Messaging platform. Supported values: `line`, `whatsapp`                                                           |
| channelId         | String | Y        | Messaging platform Channel ID. For LINE → LINE Messaging Channel ID. For WhatsApp → WhatsApp Business Phone Number |
| userId            | String | Y        | Contact's User ID. For LINE → LINE User ID. For WhatsApp → WhatsApp Phone Number                                   |
| agentEmail        | String | N        | Agent login email in Omnichat. *One of `agentEmail`, `agentPhone`, or `agentEmployeeCode` is required*              |
| agentPhone        | String | N        | Agent login phone in Omnichat. *One of `agentEmail`, `agentPhone`, or `agentEmployeeCode` is required*              |
| agentEmployeeCode | String | N        | Agent employee code. *One of `agentEmail`, `agentPhone`, or `agentEmployeeCode` is required*                        |

## Request Example

```json
{
    "platform": "whatsapp",
    "channelId": "85250000001",
    "userId": "85215022101325",
    "agentEmail": "agent001@example.com"
}
```

## Response Body

### Success - 204

Collaborator unassigned successfully. Empty response body.

### Failed - 400 Bad Request

| Error Message                                                                    | Description                                                              |
| :------------------------------------------------------------------------------- | :----------------------------------------------------------------------- |
| `OCE::BAD_REQUEST::userId is required`                                           | `userId` field is blank or missing                                       |
| `OCE::BAD_REQUEST::channelId is required`                                        | `channelId` field is blank or missing                                    |
| `OCE::BAD_REQUEST::platform is required`                                         | `platform` field is blank or missing                                     |
| `OCE::BAD_REQUEST::platform (xxx) is not supported yet`                          | The provided platform is not `line` or `whatsapp`                        |
| `OCE::BAD_REQUEST::team (xxx) is not supported to use Open API Customer Service` | The team does not have `OPEN_API` or `OPEN_API_CUSTOMER_SERVICE` enabled |
| `OCE::BAD_REQUEST::Platform not found: xxx`                                      | Platform name does not match any known platform enum                     |
| `OCE::BAD_REQUEST::Channel not found: xxx`                                       | WhatsApp account not found for the given team and channel                |
| `OCE::BAD_REQUEST::WhatsappAccUserDoc not found: xxx`                            | WhatsApp user not found for the given team, channel, and telephone       |
| `OCE::BAD_REQUEST::No valid agent identifier provided`                           | No agent resolver could handle the provided agent identifiers            |
| `OCE::BAD_REQUEST::Unauthenticated access token`                                 | The provided token does not match the system API key                     |
| `OCE::BAD_REQUEST::Missing arkhamApiToken in systemSetting`                      | System setting `arkhamApiToken` is not configured                        |

### Failed - 500 Internal Server Error

| Error Message                              | Description               |
| :----------------------------------------- | :------------------------ |
| `OCE::INTERNAL_SERVER_ERROR::<message>`    | Unexpected server error   |