---
title: OMO Sales APIs
deprecated: false
hidden: false
metadata:
  robots: index
---
# OMO Sales APIs

APIs for OMO (Online-Merge-Offline) sales operations including reports and roster management.

## Subscription Required

- OMO Sales Cloud
- OMO Sales Open API Module

---

# Get Teammate's Messages Sent Report

Get the messages sent statistics of each teammate in a specific date range.

## Endpoint

**GET** `https://open-api.omnichat.ai/v1/reports/messages`

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
      <td>page</td>
      <td>Integer</td>
      <td>No</td>
      <td>Page number. Default: 1</td>
    </tr>
    <tr>
      <td>pageSize</td>
      <td>Integer</td>
      <td>No</td>
      <td>Number of results per page. Default: 20, Max: 100</td>
    </tr>
    <tr>
      <td>after</td>
      <td>Long</td>
      <td>Yes</td>
      <td>Start of date range in unix timestamp (milliseconds), inclusive. Max range: 7 days</td>
    </tr>
    <tr>
      <td>before</td>
      <td>Long</td>
      <td>Yes</td>
      <td>End of date range in unix timestamp (milliseconds), exclusive. Max range: 7 days</td>
    </tr>
  </tbody>
</Table>

## Response Body

| Field | Type | Description |
| :---- | :--- | :---------- |
| content | Array of `Message Sent Statistics` Object | Statistics per teammate |
| totalElements | Integer | Total number of records |

### `Message Sent Statistics` Object

| Field | Type | Description |
| :---- | :--- | :---------- |
| name | String | Teammate name |
| employeeCode | String | Employee code |
| shopLocations | Array of `Shop Location` Object | Shop locations |
| messageCount | Array of `Message Count` Object | Message counts by platform |

### `Shop Location` Object

| Field | Type | Description |
| :---- | :--- | :---------- |
| name | String | Shop location name |
| code | String | Shop location code |

### `Message Count` Object

| Field | Type | Description |
| :---- | :--- | :---------- |
| platform | String | Messaging platform: `line`, `facebook`, `whatsapp`, `instagram`, `wechat`, `website` |
| messages | Integer | Number of messages sent |
| productReferralLinks | Integer | Number of product referral link messages sent |

### Success Response - HTTP Status 200

```json
{
  "content": [
    {
      "name": "Sales Ken",
      "employeeCode": "S0001",
      "shopLocations": [
        { "name": "Shop A", "code": "S-001" },
        { "name": "Shop B", "code": "S-002" }
      ],
      "messageCount": [
        { "platform": "line", "messages": 131, "productReferralLinks": 5 },
        { "platform": "facebook", "messages": 4, "productReferralLinks": 0 },
        { "platform": "whatsapp", "messages": 0, "productReferralLinks": 0 }
      ]
    }
  ],
  "totalElements": 1
}
```

---

# Get Product Referral Link Order Report

Get all orders from product referral links in a specific date range.

## Endpoint

**GET** `https://open-api.omnichat.ai/v1/reports/product-referral-links/orders`

## Query Parameters

Same as "Get Teammate's Messages Sent Report".

## Response Body

| Field | Type | Description |
| :---- | :--- | :---------- |
| content | Array of `Order` Object | Orders from product referral links |
| totalElements | Integer | Total number of orders |

### `Order` Object

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
      <td>orderId</td>
      <td>String</td>
      <td>Order ID</td>
    </tr>
    <tr>
      <td>currency</td>
      <td>String</td>
      <td>Currency code</td>
    </tr>
    <tr>
      <td>total</td>
      <td>Double</td>
      <td>Order total amount</td>
    </tr>
    <tr>
      <td>date</td>
      <td>Long</td>
      <td>Order purchase time (unix timestamp)</td>
    </tr>
    <tr>
      <td>memberId</td>
      <td>String</td>
      <td>Member ID of customer</td>
    </tr>
    <tr>
      <td>linkSentTime</td>
      <td>Long</td>
      <td>Time agent sent the link (unix timestamp)</td>
    </tr>
    <tr>
      <td>linkClickedTime</td>
      <td>Long</td>
      <td>Time customer clicked the link (unix timestamp)</td>
    </tr>
    <tr>
      <td>considerationTime</td>
      <td>Double</td>
      <td>Time to purchase in minutes (rounded to 2 decimals)</td>
    </tr>
    <tr>
      <td>agentName</td>
      <td>String</td>
      <td>Sales agent name</td>
    </tr>
    <tr>
      <td>agentEmployeeCode</td>
      <td>String</td>
      <td>Sales agent employee code</td>
    </tr>
    <tr>
      <td>agentLocationName</td>
      <td>String</td>
      <td>Shop location name</td>
    </tr>
    <tr>
      <td>agentLocationCode</td>
      <td>String</td>
      <td>Shop location code</td>
    </tr>
    <tr>
      <td>91appOrderId</td>
      <td>Object</td>
      <td>91App order IDs (for 91App clients only)</td>
    </tr>
  </tbody>
</Table>

### Success Response - HTTP Status 200

```json
{
  "content": [
    {
      "orderId": "TX000001",
      "currency": "TWD",
      "total": 100,
      "date": 1604650656053,
      "memberId": "M001",
      "linkSentTime": 1604650656053,
      "linkClickedTime": 1604650656053,
      "considerationTime": 14.51,
      "agentName": "Sales Ken",
      "agentEmployeeCode": "S0001",
      "agentLocationName": "Shop A",
      "agentLocationCode": "S-001",
      "91appOrderId": {
        "tgCode": "TG00000000001",
        "tmCode": ["TM00000000001", "TM00000000002"],
        "tsCode": ["TS00000000001", "TS00000000002"]
      }
    }
  ],
  "totalElements": 1
}
```

---

# Check Product Referral Link Tracking Info

Get the tracking code information.

## Endpoint

**GET** `https://open-api.omnichat.ai/v1/product-referral-links/info`

## Query Parameters

| Parameter | Type | Required | Description |
| :-------- | :--- | :------- | :---------- |
| ocsaid | String | Yes | Sales tracking code from URL `ocsaid` query parameter or `__ocsaid` cookie |

## Response Body

### `Tracking Code Info` Object

| Field | Type | Description |
| :---- | :--- | :---------- |
| agentName | String | Sales agent name |
| agentEmployeeCode | String | Sales agent employee code |
| agentLocationName | String | Shop location name |
| agentLocationCode | String | Shop location code |
| linkSentTime | Long | Link sent time (unix timestamp) |
| linkClickedTime | Long | Link clicked time (unix timestamp) |
| linkTrackingMode | String | Tracking mode: `sent` or `clicked` |
| linkLifetime | Integer | Current link lifetime in days |

### Success Response - HTTP Status 200

```json
{
  "content": {
    "agentName": "Sales Ken",
    "agentEmployeeCode": "S0001",
    "agentLocationName": "Shop A",
    "agentLocationCode": "S-001",
    "linkSentTime": 1604650656053,
    "linkClickedTime": 1604650656053,
    "linkTrackingMode": "sent",
    "linkLifetime": 14
  }
}
```

---

# Upload Roster

Upload salesperson roster to Omnichat.

## Endpoint

**PUT** `https://open-api.omnichat.ai/v1/rosters`

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
      <td>month</td>
      <td>String</td>
      <td>Yes</td>
      <td>Month of roster. Format: YYYY-MM</td>
    </tr>
    <tr>
      <td>idField</td>
      <td>String</td>
      <td>Yes</td>
      <td>Staff identify key: `email`, `phone`, or `employeeCode`</td>
    </tr>
    <tr>
      <td>records</td>
      <td>Array</td>
      <td>Yes</td>
      <td>Roster records</td>
    </tr>
  </tbody>
</Table>

### `Staff Roster Record` Object

| Field | Type | Required | Description |
| :---- | :--- | :------- | :---------- |
| id | String | Yes | Staff identifier (must match Omnichat user settings) |
| locationCode | String | Yes | Shop location code (must match Omnichat settings) |
| time | Array of `Roster Time` Object | Yes | Roster details |

### `Roster Time` Object

| Field | Type | Required | Description |
| :---- | :--- | :------- | :---------- |
| day | Integer | Yes | Day of month |
| in | String | Yes | Clock-in time (hh:mm). Empty for day off |
| out | String | Yes | Clock-out time (hh:mm). Empty for day off |

## Response

**Success** - HTTP Status 200

```json
{
  "content": {
    "invalidRecords": []
  }
}
```

**With Invalid Records** - HTTP Status 200

```json
{
  "content": {
    "invalidRecords": [
      {
        "id": "A001",
        "locationCode": "locationCode-001",
        "time": [...],
        "error": "Duplicate 'id': 'A001', 'locationCode': 'locationCode-001'"
      }
    ]
  }
}
```

## Example Request

```json
{
  "month": "2023-04",
  "idField": "email",
  "records": [
    {
      "id": "john.doe@example.com",
      "locationCode": "locationCode-001",
      "time": [
        { "day": 1, "in": "09:30", "out": "18:30" },
        { "day": 2, "in": "09:30", "out": "18:30" },
        { "day": 3, "in": "", "out": "" }
      ]
    }
  ]
}
```
