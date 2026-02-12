---
title: Agent Message API
deprecated: false
hidden: false
metadata:
  robots: index
---
# Subscription Required

* Raccoon AI Add-on, or
* Open API - 3rd-party AI Agent Module

# Endpoint

**POST** [https://open-api.omnichat.ai/v1/agent-messages](https://open-api.omnichat.ai/v1/agent-messages)

# Request Body

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
        team
      </td>

      <td>
        String
      </td>

      <td>
        Y
      </td>

      <td>
        Team ID
        Use `team.id` retrieved from the webhook
      </td>
    </tr>

    <tr>
      <td>
        roomId
      </td>

      <td>
        String
      </td>

      <td>
        Y
      </td>

      <td>
        ID of the chat room to receive the message
      </td>
    </tr>

    <tr>
      <td>
        messages
      </td>

      <td>
        Array of `Message` objects
      </td>

      <td>
        Y
      </td>

      <td>
        Messages to send.  
        Max size for text and image: 5
      </td>
    </tr>

    <tr>
      <td>
        replyToken
      </td>

      <td>
        String
      </td>

      <td>
        Y*
      </td>

      <td>
        Reply token for LINE retrieved from the webhook  
        Required for LINE messaging
      </td>
    </tr>
  </tbody>
</Table>

### `Message` Object

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
        type
      </td>

      <td>
        String
      </td>

      <td>
        Y
      </td>

      <td>
        Message type.

        Available types:

        * `text`: Text message
        * `image`: Image message
        * `video`: Video message
        * `audio`: Audio message (not supported on Webchat)
        * `quick_reply`: Quick Reply message
        * `google_map` : Google Map message (webchat only)

        Max file size differs on different platforms.
      </td>
    </tr>

    <tr>
      <td>
        text
      </td>

      <td>
        String
      </td>

      <td>
        Y*
      </td>

      <td>
        Message content.

        Required if type is `text`
      </td>
    </tr>

    <tr>
      <td>
        url
      </td>

      <td>
        String
      </td>

      <td>
        Y*
      </td>

      <td>
        URL to media-related resources  
        Required if type is `image` or `audio`

        Find a supported extension for different message types in our [official manuals](https://docs.omnichat.ai/features/omnichannel-messenger/chuan-song-tu-pian-ying-pian-yin-xun-dang-an).
      </td>
    </tr>

    <tr>
      <td>
        video
      </td>

      <td>
        Video
      </td>

      <td>
        Y*
      </td>

      <td>
        video-related resources.  
        Required if type is video

        Find a supported extension for different message types in our [official manuals](https://docs.omnichat.ai/features/omnichannel-messenger/chuan-song-tu-pian-ying-pian-yin-xun-dang-an).
      </td>
    </tr>

    <tr>
      <td>
        quickReply
      </td>

      <td>
        QuickReply
      </td>

      <td>
        Y*
      </td>

      <td>
        `QuickReply` Object
        Required if type is `quick_reply`
      </td>
    </tr>

    <tr>
      <td>
        googleMap
      </td>

      <td>
        GoogleMap
      </td>

      <td>
        Y*
      </td>

      <td>
        GoogleMap Object  
        Required if type is `google_map`
      </td>
    </tr>
  </tbody>
</Table>

<br />

### `Video` Object

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
        url
      </td>

      <td>
        String
      </td>

      <td>
        Y
      </td>

      <td>
        URL to the video file.
      </td>
    </tr>

    <tr>
      <td>
        thumbnailUrl
      </td>

      <td>
        String
      </td>

      <td>
        Y*
      </td>

      <td>
        `previewImage` URL for `LINE` video message

        Only required in the LINE platform.
      </td>
    </tr>
  </tbody>
</Table>

<br />

### `QuickReply` Object

| Field   | Type               | Required | Description              |
| :------ | :----------------- | :------- | :----------------------- |
| text    | String             | Y        | Message with quick reply |
| replies | Reply Object Array | Y        | Reply options            |

<br />

#### `Reply` Object

| Field | Type   | Required | Description         |
| :---- | :----- | :------- | :------------------ |
| text  | String | Y        | Quick reply content |

<br />

### `GoogleMap` Object

| Field        | Type   | Required | Description                              |
| :----------- | :----- | :------- | :--------------------------------------- |
| staticUrl    | String | Y        | static map url                           |
| embeddingUrl | String | Y        | embedding map url                        |
| appUrl       | String | N        | open google map app if on mobile devices |

<br />

## Request Example

### Text

```json
{
    "team": "a122b64d-cbb4-4b32-aecb-c1cc48908e06",
    "roomId": "67ffde199a2d2ebc4714d41c",
    "messages": [
        {
            "type": "text",
            "text": "Example text"
        }
    ]
}
```

### Image

```json
{
    "team": "a122b64d-cbb4-4b32-aecb-c1cc48908e06",
    "roomId": "67ffde199a2d2ebc4714d41c",
    "messages": [
        {
            "type": "image",
            "url": "https:://exmaple-image.png"
        }
    ]
}
```

### Video

```json
{
    "team": "a122b64d-cbb4-4b32-aecb-c1cc48908e06",
    "roomId": "67ffde199a2d2ebc4714d41c",
    "messages": [
        {
            "type": "video",
            "video": {
                "url": "https://example/mock.mp4",
                "thumbnailUrl": "https://example/mock.jpg"
            }
        }
    ]
}
```

### Audio

```json
{
    "team": "a122b64d-cbb4-4b32-aecb-c1cc48908e06",
    "roomId": "67ffde199a2d2ebc4714d41c",
    "messages": [
        {
            "type": "audio",
            "url": "https:://exmaple-audio.m4a"
        }
    ]
}
```

### Quick Reply

```json
{
	  "team": "a122b64d-cbb4-4b32-aecb-c1cc48908e06",
    "roomId": "67ffde199a2d2ebc4714d41c",
    "messages": [
        {
            "type": "quick_reply",
            "quick_reply": {
                "text": "Message Content",
                "replies": [
                    {
                        "text": "echo text"
                    }
                ]
            }
        }
    ]
}
```

### Google Map

```json
 {
     "team": "Easychat-2",
     "roomId": "366e4390-7dc9-4858-bf77-ce329571e4d8",
     "messages": [{
         "type": "google_map",
         "googleMap": {
            "staticUrl": "https://maps.googleapis.com/maps/api/staticmap?center=25.033964,121.564468&zoom=15&size=600x400&scale=2&markers=color:red|label:T|25.033964,121.564468&key=AIzaSyCUz2ww6G5yRfo7u8Lt6rM4N0cUTDZIJ3M",
            "embeddingUrl": "https://www.google.com/maps/embed/v1/place?key=AIzaSyCUz2ww6G5yRfo7u8Lt6rM4N0cUTDZIJ3M&q=%E5%8F%B0%E5%8C%97101",
            "appUrl":"2222"
         }
     }]
 }
```

<br />

# Response Body

## Success - 200 OK

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
        messageIds
      </td>

      <td>
        Array of String
      </td>

      <td>
        Y
      </td>

      <td>
        Message IDs of sent messages.
        Response as null to the message that failed to send
      </td>
    </tr>
  </tbody>
</Table>

```json
{
    "messageIds": [
        "461230966842064897"
    ]
}
```

## Failed - 400 Bad Request

### No Feature Toggle

```json
{
    "errorCode": "INVALID_REQUEST_BODY",
    "message": "The team does not have access to the third-party AI agent feature."
}
```

### Invalid request body

```json
{
    "errorCode": "INVALID_REQUEST_BODY",
    "message": "roomId is required"
}
```

### Exceed max number of messages

```json
{
    "errorCode": "INVALID_REQUEST_BODY",
    "message": "Up to 5 messages are allowed at a time"
}
```

### Room not found / invalid `roomId`

```json
{
    "errorCode": "INVALID_REQUEST_BODY",
    "message": "roomId not found"
}
```

<br />

### Missing required text for `quick_reply`

```json
{
    "errorCode": "INVALID_REQUEST_BODY",
    "message": "quick_reply.text is required for quick_reply-type messages"
}
```

<br />

## Failed - 424 Failed Dependency

### Line API Failed

```json
{
    "errorCode": "LINE_API_EXCEPTION",
    "message": "Invalid reply token"
}
```
