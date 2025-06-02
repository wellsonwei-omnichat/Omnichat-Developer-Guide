---
title: Getting Started
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Overview

In order to provide dynamic responses in Omnichat chatbot flow, please provide the following API for Omnichat to call.

## Endpoint

Dynamic and can be defined by you.

## Authorization

Please provide your API access token (Long-lived without expiration) and Omnichat will put the API token in Authorization header using the Bearer schema.

> **Authorization: Bearer {API-TOKEN}**

## Request Method

POST

## Content Type

application/json

## Request Body

Request body is dynamic according to the information you need to generate the dynamic response from your side.

For example:  
If you wish to support order inquiry in your chatbot and your Server needs order ID to retrieve the order information, you can design your request body as below

```json
{
  "orderId": "A0000001"
}
```

## Response Body

- You need to response to Omnichat API request using below format to send dynamic message content to your customer.
- You can include at most 5 messages inside the “messages” field.
- If your API failed to process the Omnichat API request (e.g. the order id is invalid), you can response with HTTP status code 400, Omnichat will trigger the error message block set in Omnichat admin portal.

***

### Success sample

Response Status: HTTP 200

Response Body:

```json
{
  "messages": [
    {
      "type": "text",
      "text": "You order A00001 will be shipped on 3/1 10:00AM."
    },
    {
      "type": "text",
      "text": "Your shipment tracking code is TS000001."
    },
    {
      "type": "image",
      "image": "https://www.example.com/image.png",
      "text": "image caption"
    },
    {
      "type": "carousel",
      "carousel": [
        {
          "image": "https://www.example.com/image.png",
          "title": "This is a carousel",
          "text": "This is the text",
          "url": "https://google.com",
          "buttons": [
            {
              "type": "postback",
              "title": "Button 1",
              "botId": "4d6702e4-0a2e-4939-aec3-30f9ce619928",
              "blockId": "6e69bfc3-ce07-414c-9eee-23b667b3e034",
              "tags": [
                "tag1",
                "tag2"
              ],
              "attribute": {
                "key": "ATTR_KEY_1",
                "value": "VAL_1"
              }
            },
            {
              "type": "url",
              "title": "Button 2",
              "url": "https://example.com/example.html",
              "tags": [
                "tag3"
              ]
            }
          ]
        }
      ]
    },
    {
      "type": "lineImageCarousel",
      "lineImageCarousel": [
        {
          "image": "https://www.example.com/image.png",
          "overlapImage": {
            "image": "https://www.example.com/overlap_image.png",
            "width": "100px",
            "height": "100px",
            "offsetTop": "18px",
            "offsetStart": "18px",
            "cornerRadius": "20px",
          },
          "action": {
            "type": "url",
            "url": "https://example.com/example.html",
            "tags": [
              "tag3"
            ]
          },
          "buttons": [
            {
              "type": "postback",
              "title": "Button 1",
              "style": "primary",
              "color": "FFFFFF99",
              "botId": "4d6702e4-0a2e-4939-aec3-30f9ce619928",
              "blockId": "6e69bfc3-ce07-414c-9eee-23b667b3e034",
              "tags": [
                "tag1",
                "tag2"
              ],
              "attribute": {
                "key": "ATTR_KEY_1",
                "value": "VAL_1"
              }
            },
            {
              "type": "url",
              "title": "Button 2",
              "style": "secondary",
              "color": "FFFFFF99",
              "url": "https://example.com/example.html",
              "tags": [
                "tag3"
              ]
            }
          ]
        }
      ]
    },
    {
      "type": "optionList",
      "optionList": {
        "text": "Please select your options",
        "buttonTitle": "Options",
        "options": [
          {
            "type": "postback",
            "title": "option 1",
            "description": "option 1 description",
            "botId": "4d6702e4-0a2e-4939-aec3-30f9ce619928",
            "blockId": "6e69bfc3-ce07-414c-9eee-23b667b3e034",
            "tags": [
              "tag1",
              "tag2"
            ],
            "attribute": {
              "key": "ATTR_KEY_1",
              "value": "VAL_1"
            }
          }
        ]
      }
    }
  ]
}
```

***

### Failed sample:

Response status: HTTP 400 Bad Request

Response body: Empty

***

### Properties

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Data Type",
    "h-2": "Required",
    "h-3": "Description",
    "h-4": "Example",
    "0-0": "type",
    "0-1": "String",
    "0-2": "Y",
    "0-3": "Response message type.  \n  \nSupported values:  \n- **text**: Text message  \n- **image**: Image message  \n- **carousel**: Carousel messages  \n- **optionList**: For WhatsApp only",
    "0-4": "text",
    "1-0": "text",
    "1-1": "String",
    "1-2": "Y if type=text",
    "1-3": "For WhatsApp:  \nYou can pass in “text” field as caption for type=image  \n  \nMax length: 4096 characters",
    "1-4": "Your shipment tracking code is TS000001",
    "2-0": "image",
    "2-1": "String",
    "2-2": "Y if type=image",
    "2-3": "Image URL of the response message",
    "2-4": "`https://www.example.com/image.png`",
    "3-0": "carousel",
    "3-1": "Array of Carousel Object",
    "3-2": "Y if type=carousel",
    "3-3": "Carousel message content  \n(Noted: For WhatsApp, it will be sent as image & text message separately)",
    "3-4": "",
    "4-0": "optionList",
    "4-1": "Option List Object",
    "4-2": "Y if type=optionList",
    "4-3": "For WhatsApp only",
    "4-4": ""
  },
  "cols": 5,
  "rows": 5,
  "align": [
    "left",
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


***

#### Carousel Object

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Data Type",
    "h-2": "Required",
    "h-3": "Description",
    "h-4": "Example",
    "0-0": "image",
    "0-1": "String",
    "0-2": "Y",
    "0-3": "Carousel message image",
    "0-4": "`https://www.example.com/image.png`",
    "1-0": "title",
    "1-1": "String",
    "1-2": "Y",
    "1-3": "For WhatsApp, max length is 4096 characters (combined with “title” field) and it will be bold",
    "1-4": "Moisturizing Mask",
    "2-0": "text",
    "2-1": "String",
    "2-2": "Y",
    "2-3": "For WhatsApp, max length is 4096 characters (combined with “title” field)",
    "2-4": "On sales 20% off",
    "3-0": "buttons",
    "3-1": "Array of Button Object",
    "3-2": "Y",
    "3-3": "For WhatsApp, you can have up to 3 buttons.",
    "3-4": "",
    "4-0": "url",
    "4-1": "String",
    "4-2": "Y",
    "4-3": "Link of clicking message image.  \nNot supported in WhatsApp.",
    "4-4": "`https://www.example.com`"
  },
  "cols": 5,
  "rows": 5,
  "align": [
    "left",
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


***

#### LINE Image Carousel Object

| Field Name | Data Type              | Required | Description                             | Example                             |
| :--------- | :--------------------- | :------- | :-------------------------------------- | :---------------------------------- |
| image      | String                 | Y        | Carousel image                          | `https://www.example.com/image.png` |
| action     | Action Object          | Y        | Action when clicking the carousel image |                                     |
| buttons    | Array of Button Object | Y        | Buttons                                 |                                     |

***

#### Button Object

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Data Type",
    "h-2": "Required",
    "h-3": "Description",
    "h-4": "Example",
    "0-0": "type",
    "0-1": "String",
    "0-2": "Y",
    "0-3": "Button type:  \nSupported values:  \n- **postback**: trigger chatbot message  \n- **url**: website link  \n- **message**: send a text message  \n  \nFor WhatsApp, if use type=url, the url will append to the message body",
    "0-4": "postback",
    "1-0": "title",
    "1-1": "String",
    "1-2": "Y",
    "1-3": "Message title  \n  \nFor WhatsApp, max length: 20 characters",
    "1-4": "More Info",
    "2-0": "blockId",
    "2-1": "String",
    "2-2": "Y if type=postback",
    "2-3": "Bot Block ID in Omnichat system",
    "2-4": "8d1f060f-3e0d-4f52-9837-4920e9b4406d",
    "3-0": "tags",
    "3-1": "Array of String",
    "3-2": "N",
    "3-3": "Tags to be added when user clicks the button",
    "3-4": "[“Mask”]",
    "4-0": "attribute",
    "4-1": "Attribute Object",
    "4-2": "N",
    "4-3": "Attributes to be added when user clicks the button",
    "4-4": "",
    "5-0": "url",
    "5-1": "String",
    "5-2": "Y if type=url",
    "5-3": "Message sent to the user when clicking the button",
    "5-4": "",
    "6-0": "message",
    "6-1": "String",
    "6-2": "Y if type=message",
    "6-3": "",
    "6-4": "",
    "7-0": "style",
    "7-1": "String",
    "7-2": "Y for LINE carousel image",
    "7-3": "Button style  \n  \nSupported values:  \n- **primary**  \n- **secondary**",
    "7-4": "",
    "8-0": "color",
    "8-1": "String",
    "8-2": "Y for LINE carousel image",
    "8-3": "Button color hex code",
    "8-4": ""
  },
  "cols": 5,
  "rows": 9,
  "align": [
    "left",
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


***

#### Action Object

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Data Type",
    "h-2": "Required",
    "h-3": "Description",
    "h-4": "Example",
    "0-0": "type",
    "0-1": "String",
    "0-2": "Y",
    "0-3": "Button type  \n  \nSupported values:  \n- **postback**: trigger chatbot message  \n- **url**: website link  \n- **message**: send a text message",
    "0-4": "postback",
    "1-0": "blockId",
    "1-1": "String",
    "1-2": "Y if type=postback",
    "1-3": "Bot Block ID in Omnichat system",
    "1-4": "",
    "2-0": "tags",
    "2-1": "Array of String",
    "2-2": "N",
    "2-3": "Tags to be added when user clicks the button",
    "2-4": "",
    "3-0": "attribute",
    "3-1": "Attribute Object",
    "3-2": "N",
    "3-3": "Attributes to be added when user clicks the button",
    "3-4": "",
    "4-0": "url",
    "4-1": "String",
    "4-2": "Y if type=url",
    "4-3": "",
    "4-4": "",
    "5-0": "message",
    "5-1": "String",
    "5-2": "Y if type=message",
    "5-3": "The Message sent to users when clicking",
    "5-4": ""
  },
  "cols": 5,
  "rows": 6,
  "align": [
    "left",
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


***

#### Attribute Object

| Field Name | Data Type | Required | Description     | Example  |
| :--------- | :-------- | :------- | :-------------- | :------- |
| key        | String    | Y        | Attribute key   | MaskType |
| value      | String    | Y        | Attribute value | Moisture |

***

#### Option List Object

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Data Type",
    "h-2": "Required",
    "h-3": "Description",
    "h-4": "Example",
    "0-0": "text",
    "0-1": "String",
    "0-2": "Y",
    "0-3": "Message body  \nMax length: 1024 characters",
    "0-4": "",
    "1-0": "buttonTitle",
    "1-1": "String",
    "1-2": "Y",
    "1-3": "Option list button title  \nMax length: 20 characters",
    "1-4": "",
    "2-0": "options",
    "2-1": "Array of Option Object",
    "2-2": "Y",
    "2-3": "Options",
    "2-4": ""
  },
  "cols": 5,
  "rows": 3,
  "align": [
    "left",
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]


***

#### Option Object

[block:parameters]
{
  "data": {
    "h-0": "Field Name",
    "h-1": "Data Type",
    "h-2": "Required",
    "h-3": "Description",
    "h-4": "Example",
    "0-0": "type",
    "0-1": "String",
    "0-2": "Y",
    "0-3": "Button type  \n  \nSupported values:  \n- **postback**: trigger chatbot message",
    "0-4": "postback",
    "1-0": "title",
    "1-1": "String",
    "1-2": "Y",
    "1-3": "Option title  \nMax length: 24 characters",
    "1-4": "Option 1",
    "2-0": "description",
    "2-1": "String",
    "2-2": "Y",
    "2-3": "Option description  \nMax length: 72 characters",
    "2-4": "Option 1 Description",
    "3-0": "botId",
    "3-1": "String",
    "3-2": "Y",
    "3-3": "Chatbot ID in Omnichat system",
    "3-4": "8d1f060f-3e0d-4f52-9837-4920e9b4406d",
    "4-0": "blockId",
    "4-1": "String",
    "4-2": "Y",
    "4-3": "Chatbot Block ID in Omnichat system",
    "4-4": "8d1f060f-3e0d-4f52-9837-4920e9b4406d",
    "5-0": "tags",
    "5-1": "Array of String",
    "5-2": "N",
    "5-3": "Tags to be added when user clicks the button",
    "5-4": "[“Mask”]",
    "6-0": "attribute",
    "6-1": "Attribute Object",
    "6-2": "N",
    "6-3": "Attributes to be added when user clicks the button",
    "6-4": ""
  },
  "cols": 5,
  "rows": 7,
  "align": [
    "left",
    "left",
    "left",
    "left",
    "left"
  ]
}
[/block]