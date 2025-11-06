---
title: Contacts API
deprecated: false
hidden: false
metadata:
  robots: index
---
# Subscription Required

* CS / Marketing / OMO Sales / Social CDP Cloud
* CRM Open API Module
* Raccoon AI Add-on or 3rd-party AI Agent Open API Module

# Upsert a Contact

## Endpoint

**POST** [https://open-api.omnichat.ai/v1/contacts/\{platform}?channelId=\{channelId}&userId=\{userId}](https://open-api.omnichat.ai/v1/contacts/\{platform}?channelId=\{channelId}\&userId=\{userId})

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
        * webchat (only support update action, cannot upsert)
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

        * LINE → LINE Channel ID
        * Facebook → Facebook Page ID
        * WhatsApp → WhatsApp Business Phone Number
        * Instagram → Instagram Business Account ID
        * WeChat → WeChat ID
        * Webchat → Fixed value `webchat`
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

        * LINE → LINE User ID
        * Facebook → Facebook PSID
        * WhatsApp → WhatsApp Phone Number
        * Instagram → Instagram User ID
        * WeChat → WeChat User ID
        * Webchat → Webchat User ID
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
        Map\<String\, String\>
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

## `Custom Attribute` Objects

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field
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

## Responses

### Success - 204

HTTP Status 204 with empty response body

### Failed - Bad request - HTTP Status 4xx / 5xx

```json
{
    "errorCode": "MISSING_URL_PARAMETER",
    "message": "Missing URL parameters"
}
```
