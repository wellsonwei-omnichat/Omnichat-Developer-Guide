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

| Field  | Type    | Required | Description                   |
| :----- | :------ | :------- | :---------------------------- |
| name   | String  | N        | Contact’s Name                |
| status | Boolean | N        | Contact’s subscription status |
