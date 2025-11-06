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

<br />

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

      </td>
    </tr>
  </tbody>
</Table>
