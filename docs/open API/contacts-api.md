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

      </td>

      <td>

      </td>

      <td>

      </td>

      <td>

      </td>
    </tr>
  </tbody>
</Table>

<br />
