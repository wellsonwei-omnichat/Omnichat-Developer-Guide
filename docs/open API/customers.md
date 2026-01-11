---
title: Customers
deprecated: false
hidden: false
metadata:
  robots: index
---
# Customers

APIs for managing customer profiles (identified by memberId or omniCustomerId).

## Subscription Required

| Feature Toggle | Description |
|----------------|-------------|
| `open_api_crm` | CRM Open API Module - Required for all Customer endpoints |

---

# Get Customer Detail by Member ID

Get customer details by Member ID.

## Endpoint

**GET** `https://open-api.omnichat.ai/v1/customers`

## Request Headers

| Header | Value | Description |
| :----- | :---- | :---------- |
| Authorization | Bearer \{API_TOKEN\} | API Token from Omnichat |

## Query Parameters

| Parameter | Type | Required | Description |
| :-------- | :--- | :------- | :---------- |
| memberId | String | Yes | Customer's Member ID |

## Response Body

| Field | Type | Description |
| :---- | :--- | :---------- |
| content | `Customer` Object | Customer details |

### `Customer` Object

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
      <td>username</td>
      <td>String</td>
      <td>Customer username (internal)</td>
    </tr>
    <tr>
      <td>name</td>
      <td>String</td>
      <td>Customer's name</td>
    </tr>
    <tr>
      <td>profilePicture</td>
      <td>String</td>
      <td>Profile picture URL</td>
    </tr>
    <tr>
      <td>memberId</td>
      <td>String</td>
      <td>Member ID</td>
    </tr>
    <tr>
      <td>phone</td>
      <td>String</td>
      <td>Phone number</td>
    </tr>
    <tr>
      <td>email</td>
      <td>String</td>
      <td>Email address</td>
    </tr>
    <tr>
      <td>socialChannelSubscribed</td>
      <td>Boolean</td>
      <td>Whether customer has linked social messaging profile</td>
    </tr>
    <tr>
      <td>tags</td>
      <td>Array of String</td>
      <td>Customer tags</td>
    </tr>
    <tr>
      <td>reachable</td>
      <td>Boolean</td>
      <td>Whether customer is reachable via marketing message</td>
    </tr>
    <tr>
      <td>customAttributes</td>
      <td>Array of Object</td>
      <td>Custom attributes</td>
    </tr>
    <tr>
      <td>linkedUsers</td>
      <td>Array of Object</td>
      <td>Linked social messaging profiles</td>
    </tr>
    <tr>
      <td>pointBalance</td>
      <td>String</td>
      <td>Current loyalty point balance</td>
    </tr>
    <tr>
      <td>accumulatedPoints</td>
      <td>String</td>
      <td>Accumulated loyalty points</td>
    </tr>
    <tr>
      <td>lastMessageReceivedAt</td>
      <td>Long</td>
      <td>Last message received timestamp</td>
    </tr>
    <tr>
      <td>lastCsMessageSentAt</td>
      <td>Long</td>
      <td>Last CS message sent timestamp</td>
    </tr>
    <tr>
      <td>lastMarketingMessageSentAt</td>
      <td>Long</td>
      <td>Last marketing message sent timestamp</td>
    </tr>
    <tr>
      <td>createdAt</td>
      <td>Long</td>
      <td>Creation timestamp</td>
    </tr>
    <tr>
      <td>updatedAt</td>
      <td>Long</td>
      <td>Last update timestamp</td>
    </tr>
  </tbody>
</Table>

### `Custom Attribute` Object

| Field | Type | Description |
| :---- | :--- | :---------- |
| key | String | Attribute key |
| type | Integer | Data type: `1`=text, `2`=number, `3`=date, `4`=datetime, `5`=boolean |
| value | Mixed | Attribute value |
| displayName | String | Display name |
| status | Boolean | Whether active |

### `Linked User` Object

| Field | Type | Description |
| :---- | :--- | :---------- |
| platform | String | Platform: `line`, `whatsapp`, etc. |
| channelId | String | Channel ID |
| channelUserId | String | User ID on the channel |
| channelUsername | String | Username on the channel |
| channelName | String | Channel name |
| roomId | String | Chat room ID |
| subscribed | Boolean | Subscription status |

### Success Response - HTTP Status 200

```json
{
  "content": {
    "username": "6694e599b4dadc211e33f9da",
    "name": "Peter Chan",
    "profilePicture": "https://example.com/profile.png",
    "memberId": "OC-TEST-0001",
    "phone": "85222222222",
    "email": "example@omnichat.ai",
    "socialChannelSubscribed": true,
    "tags": ["VVIP", "Sporty"],
    "reachable": true,
    "customAttributes": [
      {
        "key": "gender",
        "type": 1,
        "value": "male",
        "displayName": "Gender",
        "status": true
      }
    ],
    "linkedUsers": [
      {
        "platform": "line",
        "channelId": "1111111111111",
        "channelUserId": "U0000000000000000000000",
        "channelUsername": "liu0000000000000000000000",
        "channelName": "LINE channel name",
        "roomId": "li1111111111111-u0000000000000000000000",
        "subscribed": true
      }
    ],
    "pointBalance": "100",
    "accumulatedPoints": "500",
    "lastMessageReceivedAt": 1742196237835,
    "lastCsMessageSentAt": 1729564624123,
    "lastMarketingMessageSentAt": 1736236655000,
    "createdAt": 1679037836356,
    "updatedAt": 1743387002575
  }
}
```

---

# Upsert a Customer by Member ID

Create or update a customer by Member ID.

## Endpoint

**PUT** `https://open-api.omnichat.ai/v1/customers?memberId={memberId}`

## Query Parameters

| Parameter | Type | Required | Description |
| :-------- | :--- | :------- | :---------- |
| memberId | String | Yes | Customer's Member ID |

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
      <td>name</td>
      <td>String</td>
      <td>No</td>
      <td>Customer's name</td>
    </tr>
    <tr>
      <td>email</td>
      <td>String</td>
      <td>No</td>
      <td>Customer's email</td>
    </tr>
    <tr>
      <td>phone</td>
      <td>String</td>
      <td>No</td>
      <td>Customer's phone</td>
    </tr>
    <tr>
      <td>tags</td>
      <td>Array of String</td>
      <td>No</td>
      <td>Tags to replace. Cannot use with tagsToAdd/tagsToRemove</td>
    </tr>
    <tr>
      <td>tagsToAdd</td>
      <td>Array of String</td>
      <td>No</td>
      <td>Tags to add. Cannot use with tags</td>
    </tr>
    <tr>
      <td>tagsToRemove</td>
      <td>Array of String</td>
      <td>No</td>
      <td>Tags to remove. Cannot use with tags</td>
    </tr>
    <tr>
      <td>customAttributes</td>
      <td>Array of Object</td>
      <td>No</td>
      <td>Custom attributes to set</td>
    </tr>
  </tbody>
</Table>

### `Custom Attribute` Object (Request)

| Field | Type | Description |
| :---- | :--- | :---------- |
| key | String | Attribute key. Max 100 characters |
| value | Mixed | Attribute value. Format depends on type. Max 1000 characters |

**Value Format:**
- **number**: Use number format (not string)
- **boolean**: Use `true` / `false`
- **datetime**: Use ISO8601 format, e.g., `2022-11-01T14:16:00`
- **date**: Use `YYYY-MM-DD` format

**To remove value:**
- **string/date/datetime**: Pass empty string
- **boolean**: Pass `false`
- **number**: Pass `0`

## Response

**Success** - HTTP Status 204 with empty response body

### Example Request

```json
{
  "name": "Peter Chan",
  "email": "example@example.com",
  "phone": "85298765432",
  "tagsToAdd": ["VVIP", "Sporty"],
  "tagsToRemove": ["VIP"],
  "customAttributes": [
    { "key": "MemberTier", "value": "GOLD" },
    { "key": "Points", "value": 2031 },
    { "key": "TotalSpending", "value": 900.00 },
    { "key": "AcceptedMarketingPromotion", "value": true },
    { "key": "LastPurchaseDate", "value": "2022-11-01" },
    { "key": "RegisterDatetime", "value": "2022-11-01T14:16:00" }
  ]
}
```

---

# Upsert a Customer by OmniCustomer ID

Create or update a customer by OmniCustomer ID.

## Endpoint

**PUT** `https://open-api.omnichat.ai/v1/customers?omniCustomerId={omniCustomerId}`

## Query Parameters

| Parameter | Type | Required | Description |
| :-------- | :--- | :------- | :---------- |
| omniCustomerId | String | Yes | OmniCustomer ID |

## Request Body

Same as "Upsert a Customer by Member ID".

## Response

**Success** - HTTP Status 204 with empty response body

---

# Delete Customer by Member ID

Delete a customer (including member profile and chat history) by Member ID.

## Endpoint

**DELETE** `https://open-api.omnichat.ai/v1/customers?memberId={memberId}`

## Query Parameters

| Parameter | Type | Required | Description |
| :-------- | :--- | :------- | :---------- |
| memberId | String | Yes | Customer's Member ID |

## Response

**Success** - HTTP Status 204 with empty response body

**Error** - HTTP Status 4xx / 5xx

```json
{
  "errorCode": "MISSING_URL_PARAMETER",
  "message": "Missing URL parameters"
}
```
