---
title: Contacts APIs
deprecated: false
hidden: false
metadata:
  robots: index
---
# Subscription Required

* CS / Marketing / OMO Sales / Social CDP Cloud
* CRM Open API Module
* Raccoon AI Add-on or 3rd-party AI Agent Open API Module

# Get Contacts

Get updated contacts by specific date range

## Endpoint

**GET** [https://open-api.omnichat.ai/v1/contacts](https://open-api.omnichat.ai/v1/contacts)

## Query Parameters

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Required
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        platform
      </td>

      <td>
        String
      </td>

      <td>
        Y
      </td>

      <td>
        Messaging Platform.

        Supported values:

        * line
        * facebook
        * whatsapp
        * instagram
        * wechat
        * webchat
      </td>
    </tr>

    <tr>
      <td>
        channelId
      </td>

      <td>
        String
      </td>

      <td>
        Y
      </td>

      <td>
        Contact's channel ID to manipulate.

        Specific Messaging Platform Channel ID.

        For LINE → LINE Channel ID  
        For Facebook → Facebook Page ID  
        For WhatsApp → WhatsApp Business Phone Number  
        For Instagram → Instagram Business Account ID  
        For WeChat → WeChat ID  
        For Webchat → Fixed value `webchat`
      </td>
    </tr>

    <tr>
      <td>
        userId
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Contact's ID to manipulate.

        For LINE → LINE User ID  
        For Facebook → Facebook PSID For WhatsApp → WhatsApp Phone Number For Instagram → Instagram User ID For WeChat → WeChat User ID For Webchat → Webchat User ID
      </td>
    </tr>

    <tr>
      <td>
        memberId
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Contact's member ID
      </td>
    </tr>

    <tr>
      <td>
        phone
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Contact's phone number
      </td>
    </tr>

    <tr>
      <td>
        email
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Contact's email address
      </td>
    </tr>

    <tr>
      <td>
        updatedAfter
      </td>

      <td>
        Long
      </td>

      <td>
        Y* (if no specific `userId`,`memberId`,`phone`,`email`)
      </td>

      <td>
        The start of the specific date range in unix timestamp (milliseconds) (inclusive)
      </td>
    </tr>

    <tr>
      <td>
        updatedBefore
      </td>

      <td>
        Long
      </td>

      <td>
        Y* (if no specific `userId`,`memberId`,`phone`,`email`)
      </td>

      <td>
        The end of the specific date range in unix timestamp (milliseconds) (exclusive)
      </td>
    </tr>

    <tr>
      <td>
        page
      </td>

      <td>
        Integer
      </td>

      <td>
        Y* (if no specific `userId`,`memberId`,`phone`,`email`)
      </td>

      <td>
        Page number. Default: 1
      </td>
    </tr>

    <tr>
      <td>
        pageSize
      </td>

      <td>
        Integer
      </td>

      <td>
        Y* (if no specific `userId`,`memberId`,`phone`,`email`)
      </td>

      <td>
        Number of contacts per page

        Default: 20 (Max: 100)
      </td>
    </tr>
  </tbody>
</Table>

## Request example

```powershell Example1
curl --location 'https://open-api.omnichat.ai/v1/contacts?platform=line&page=1&pageSize=20&updatedAfter=1652371200000&updatedBefore=1653580800000'
```

<br />

```powershell Example2
curl --location 'https://open-api.omnichat.ai/v1/contacts?platform=whatsapp&userId=886989777777'
```

<br />

```powershell Example3
curl --location 'https://open-api.omnichat.ai/v1/contacts?platform=line&memberId=example_member_id_123'
```

## Response Body

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Nullable
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        id
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Contact's user ID
      </td>
    </tr>

    <tr>
      <td>
        channel
      </td>

      <td>
        `Channel` Object
      </td>

      <td>
        N
      </td>

      <td>
        Messaging channel object
      </td>
    </tr>

    <tr>
      <td>
        name
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Contact’s name
      </td>
    </tr>

    <tr>
      <td>
        lastMessageTime
      </td>

      <td>
        Long
      </td>

      <td>
        Y
      </td>

      <td>
        Contact's last message received time
      </td>
    </tr>

    <tr>
      <td>
        subscribedAt
      </td>

      <td>
        Long
      </td>

      <td>
        Y
      </td>

      <td>
        Contact's subscription time
      </td>
    </tr>

    <tr>
      <td>
        unsubscribedAt
      </td>

      <td>
        Long
      </td>

      <td>
        Y
      </td>

      <td>
        Contact's un-subscription time
      </td>
    </tr>

    <tr>
      <td>
        updatedAt
      </td>

      <td>
        Long
      </td>

      <td>
        N
      </td>

      <td>
        Contact's information last updated time
      </td>
    </tr>

    <tr>
      <td>
        status
      </td>

      <td>
        Boolean
      </td>

      <td>
        N
      </td>

      <td>
        Contact’s subscription status
      </td>
    </tr>

    <tr>
      <td>
        email
      </td>

      <td>
        String
      </td>

      <td>
        Y
      </td>

      <td>
        Contact’s email
      </td>
    </tr>

    <tr>
      <td>
        phone
      </td>

      <td>
        String
      </td>

      <td>
        Y
      </td>

      <td>
        Contact’s phone number
      </td>
    </tr>

    <tr>
      <td>
        memberId
      </td>

      <td>
        String
      </td>

      <td>
        Y
      </td>

      <td>
        Contact’s website member ID
      </td>
    </tr>

    <tr>
      <td>
        note
      </td>

      <td>
        String
      </td>

      <td>
        Y
      </td>

      <td>
        Contact’s note
      </td>
    </tr>

    <tr>
      <td>
        agentName
      </td>

      <td>
        String
      </td>

      <td>
        Y
      </td>

      <td>
        Name of the agent bound to the contact
      </td>
    </tr>

    <tr>
      <td>
        agentEmployeeCode
      </td>

      <td>
        String
      </td>

      <td>
        Y
      </td>

      <td>
        The employee code of the agent bound to the contact  
        (Only for OMO Sales Cloud)
      </td>
    </tr>

    <tr>
      <td>
        agentLocationName
      </td>

      <td>
        String
      </td>

      <td>
        Y
      </td>

      <td>
        Shop location name of the agent bound to the contact
      </td>
    </tr>

    <tr>
      <td>
        agentLocationCode
      </td>

      <td>
        String
      </td>

      <td>
        Y
      </td>

      <td>
        The shop location code of the agent bound to the contact  
        (Only for OMO Sales Cloud)
      </td>
    </tr>

    <tr>
      <td>
        agentBindTime
      </td>

      <td>
        String
      </td>

      <td>
        Y
      </td>

      <td>
        The time when the agent bound to the contact (ISO 8601 format)
      </td>
    </tr>

    <tr>
      <td>
        tags
      </td>

      <td>
        Array of String
      </td>

      <td>
        Y
      </td>

      <td>
        Contact’s tags to be replaced

        **[Noted: This field cannot be used together with t`agsToAdd` or `tagsToRemove` fields]**
      </td>
    </tr>

    <tr>
      <td>
        customAttributes
      </td>

      <td>
        `CustomAttribute` Object
      </td>

      <td>
        N
      </td>

      <td>
        Contact's custom attributes
      </td>
    </tr>
  </tbody>
</Table>

### `Custom Attributes` Object

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Nullable
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        key
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Attribute key  
        Max. length: 100 characters
      </td>
    </tr>

    <tr>
      <td>
        value
      </td>

      <td>
        Object  
        (according to the data type of the custom attribute configured in Omnichat portal)
      </td>

      <td>
        N
      </td>

      <td>
        Attribute value  
        Max. length: 1000 characters

        Format:  
        For `number` value, use number (integer / float) format (NOT string)  
        For `boolean` value, use true / false  
        For `datetime` value, use ISO8601 format datetime string, e.g. `2022-11-01T14:16:00`  
        For `date` value, use `YYYY-MM-DD` format string

        Remove custom attribute values:  
        You can pass in empty string for `string`/`date`/`datetime` type custom attribute to remove the value  
        For `date`/`datetime`, it will convert to `1970-01-01` in system

        For `boolean`, you should pass in false  
        For `number`, you should pass in 0
      </td>
    </tr>

    <tr>
      <td>
        displayName
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Display/readable name of the custom attribute
      </td>
    </tr>

    <tr>
      <td>
        type
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        type of the custom attribute

        Possible values: `text`: Text `number`: Number `date`: Date `datetime`: Date time `boolean`: Boolean
      </td>
    </tr>
  </tbody>
</Table>

### `Channel` Object

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Nullable
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        platform
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Channel platform

        Supported values:

        * line
        * facebook
        * whatsapp
        * instagram
        * wechat
        * web

        For 3rd-party AI Agent Open API modules:  
        only `line` and `web` are supported.
      </td>
    </tr>

    <tr>
      <td>
        channelId
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Channel ID / Fixed value `webchat` if `platform` is `web`
      </td>
    </tr>
  </tbody>
</Table>

### Success - 200

```json
{
  "content": [
    {
      "channel": {
        "platform": "line",
        "channelId": "165000000"
      },
      "id": "U2bd582c37356d37cb6d46a823de3a908",
      "name": "Alan",
      "lastMessageTime": 1604650656053,
      "subscribedAt": 1604650656053,
      "unsubscribedAt": 1604650656053,
      "updatedAt": 1604650656053,
      "tags": [
        "VIP",
        "Sports"
      ],
      "customAttributes": [
        {
          "key": "MEMBER_TIER",
          "value": "GOLD",
          "type": "text",
          "displayName": "Member Tier"
        },
        {
          "key": "GENDER",
          "value": "M",
          "type": "text",
          "displayName": "Gender"
        }
      ],
      "status": true,
      "note": "new customer",
      "email": "test@email.com",
      "phone": "886966633355",
      "memberId": "9431",
      "agentName": null,
      "agentEmployeeCode": null,
      "agentBindTime": null,
      "agentLocationName": null,
      "agentLocationCode": null
    },
    {
      "channel": {
        "platform": "line",
        "channelId": "165000000"
      },
      "id": "U2bd582c37356d37cb6d46a823de3a413",
      "name": "Mary",
      "lastMessageTime": 1604650656053,
      "tags": [],
      "status": true,
      "note": "",
      "email": "mary@email.com",
      "phone": "88690000000",
      "memberId": "",
      "agentName": "Sales Ken",
      "agentEmployeeCode": "S0001",
      "agentBindTime": 1604650656053,
      "agentLocationName": "Shop A",
      "agentLocationCode": "S-001"
    },
    {
      "channel": {
        "platform": "line",
        "channelId": "165000002"
      },
      "id": "U2bd582c37356d37cb6d46a823de3a444",
      "name": "Peter",
      "lastMessageTime": 1604650656053,
      "tags": [],
      "status": true,
      "note": "refund on 6/7",
      "email": "peter@email.com",
      "phone": "",
      "memberId": "",
      "agentName": null,
      "agentEmployeeCode": null,
      "agentBindTime": null,
      "agentLocationName": null,
      "agentLocationCode": null
    }
  ],
  "totalElements": 3
}
```

### Failed - Bad request / Internal Server Error - HTTP Status 4xx / 5xx

```json
{
    "errorCode": "",
    "message": ""
}
```

### Error Codes

* `INVALID_REQUEST_PARAMETERS`: Missing required query params (channelId+userId for specific query, or updatedAfter+updatedBefore for list query)
* `INVALID_REQUEST_PARAMETER`: Request parameter constraint violation (e.g., platform is null)
* `INVALID_REQUEST_BODY`: Request body validation failed
* `INVALID_FORMAT`: Invalid property format (e.g., invalid enum value)
* `MISMATCH_TYPE`: Query parameter type mismatch (e.g., invalid platform enum, non-integer page)
* `MISSING_URL_PARAMETER`: Required parameter is missing
* `USER_ID_NOT_FOUND`: Specific user query returned no results
* `UNEXPECTED_ERROR`: Unhandled runtime exception

# Upsert a Contact

## Endpoint

**PUT** [https://open-api.omnichat.ai/v1/contacts/\{platform}?channelId=\{channelId}&userId=\{userId}](https://open-api.omnichat.ai/v1/contacts/\{platform}?channelId=\{channelId}\&userId=\{userId})

## Parameters

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Location
      </th>

      <th>
        Required
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        platform
      </td>

      <td>
        Path
      </td>

      <td>
        Y
      </td>

      <td>
        Messaging Platform.

        Supported values:

        * line
        * facebook
        * whatsapp
        * instagram
        * wechat
        * webchat
      </td>
    </tr>

    <tr>
      <td>
        channelId
      </td>

      <td>
        Query
      </td>

      <td>
        Y
      </td>

      <td>
        Contact's channel ID to manipulate.

        Specific Messaging Platform Channel ID.

        For LINE → LINE Channel ID  
        For Facebook → Facebook Page ID  
        For WhatsApp → WhatsApp Business Phone Number  
        For Instagram → Instagram Business Account ID  
        For WeChat → WeChat ID  
        For Webchat → Fixed value `webchat`
      </td>
    </tr>

    <tr>
      <td>
        userId
      </td>

      <td>
        Query
      </td>

      <td>
        Y
      </td>

      <td>
        Contact's ID to manipulate.

        For LINE → LINE User ID  
        For Facebook → Facebook PSID For WhatsApp → WhatsApp Phone Number For Instagram → Instagram User ID For WeChat → WeChat User ID For Webchat → Webchat User ID
      </td>
    </tr>
  </tbody>
</Table>

## Request Body

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Required
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        name
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Contact’s Name
      </td>
    </tr>

    <tr>
      <td>
        status
      </td>

      <td>
        Boolean
      </td>

      <td>
        N
      </td>

      <td>
        Contact’s subscription status
      </td>
    </tr>

    <tr>
      <td>
        email
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Contact’s email
      </td>
    </tr>

    <tr>
      <td>
        phone
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Contact’s phone number
      </td>
    </tr>

    <tr>
      <td>
        memberId
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Contact’s member ID
      </td>
    </tr>

    <tr>
      <td>
        note
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Contact’s note
      </td>
    </tr>

    <tr>
      <td>
        agentEmployeeCode
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        The employee code of the agent bound to the contact  
        (Only for OMO Sales Cloud)
      </td>
    </tr>

    <tr>
      <td>
        agentLocationCode
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        The shop location code of the agent bound to the contact  
        (Only for OMO Sales Cloud)
      </td>
    </tr>

    <tr>
      <td>
        tags
      </td>

      <td>
        Array of String
      </td>

      <td>
        N
      </td>

      <td>
        Contact’s tags to be replaced

        **[Noted: This field cannot be used together with t`agsToAdd` or `tagsToRemove` fields]**
      </td>
    </tr>

    <tr>
      <td>
        tagsToAdd
      </td>

      <td>
        Array of String
      </td>

      <td>
        N
      </td>

      <td>
        Tags to be added to the contact

        **[Noted: This field cannot be used together with `tags` field]**
      </td>
    </tr>

    <tr>
      <td>
        tagsToRemove
      </td>

      <td>
        Array of String
      </td>

      <td>
        N
      </td>

      <td>
        Tags to be removed to the contact

        **[Noted: This field cannot be used together with `tags` field]**
      </td>
    </tr>

    <tr>
      <td>
        customAttributes
      </td>

      <td>
        `CustomAttribute` Object
      </td>

      <td>
        N
      </td>

      <td>
        Contact's custom attributes
      </td>
    </tr>

    <tr>
      <td>
        extraAttributes
      </td>

      <td>
        Map\<String, String>
      </td>

      <td>
        N
      </td>

      <td>
        Extra attributes
      </td>
    </tr>
  </tbody>
</Table>

### `Custom Attribute` Objects

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Nullable
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        key
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Attribute key  
        Max. length: 100 characters
      </td>
    </tr>

    <tr>
      <td>
        value
      </td>

      <td>
        Object  
        (according to the data type of the custom attribute configured in Omnichat portal)
      </td>

      <td>
        N
      </td>

      <td>
        Attribute value  
        Max. length: 1000 characters

        Format:  
        For `number` value, use number (integer / float) format (NOT string)  
        For `boolean` value, use true / false  
        For `datetime` value, use ISO8601 format datetime string, e.g. `2022-11-01T14:16:00`  
        For `date` value, use `YYYY-MM-DD` format string

        Remove custom attribute values:  
        You can pass in empty string for `string`/`date`/`datetime` type custom attribute to remove the value  
        For `date`/`datetime`, it will convert to `1970-01-01` in system

        For `boolean`, you should pass in false  
        For `number`, you should pass in 0
      </td>
    </tr>
  </tbody>
</Table>

## Request Example

```json
{
	"name": "Peter Chan",
	"status": false,
	"email": "example@example.com",
	"phone": "85298765432",
	"memberId": "M00001",
	"agentEmployeeCode": "EMP-001",
	"agentLocationCode": "SHOP-A",
  "tagsToAdd": [ "VVIP", "Sporty" ],
  "tagsToRemove": [ "VIP" ],
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

## Respons Body

### Success - 204

HTTP Status 204 with empty response body

### Failed - Bad request - HTTP Status 4xx / 5xx

```json
{
    "errorCode": "MISSING_URL_PARAMETER",
    "message": "Missing URL parameters"
}
```
