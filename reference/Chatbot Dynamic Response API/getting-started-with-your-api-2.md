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

> **Authorization: Bearer `{API-TOKEN}`**

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

<HTMLBlock>{`
<table style="width: 100%; border-collapse: collapse;">
<thead>
<tr>
  <th style="border: 1px solid #ddd; padding: 8px;">Field Name</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Data Type</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Required</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Description</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Example</th>
</tr>
</thead>
<tbody>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>type</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Response message type.  </p>
<p>Supported values:  </p>
<ul>
<li><strong>text</strong>: Text message  </li>
<li><strong>image</strong>: Image message  </li>
<li><strong>carousel</strong>: Carousel messages  </li>
<li><strong>optionList</strong>: For WhatsApp only</li>
</ul>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>text</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>text</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y if type=text</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>For WhatsApp:<br>You can pass in “text” field as caption for type=image  </p>
<p>Max length: 4096 characters</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Your shipment tracking code is TS000001</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>image</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y if type=image</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Image URL of the response message</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p><code>https://www.example.com/image.png</code></p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>carousel</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Array of Carousel Object</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y if type=carousel</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Carousel message content<br>(Noted: For WhatsApp, it will be sent as image &amp; text message separately)</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>optionList</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Option List Object</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y if type=optionList</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>For WhatsApp only</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
</tr>
</tbody>
</table>
`}</HTMLBlock>
***

#### Carousel Object

<HTMLBlock>{`
<table style="width: 100%; border-collapse: collapse;">
<thead>
<tr>
  <th style="border: 1px solid #ddd; padding: 8px;">Field Name</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Data Type</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Required</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Description</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Example</th>
</tr>
</thead>
<tbody>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>image</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Carousel message image</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p><code>https://www.example.com/image.png</code></p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>title</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>For WhatsApp, max length is 4096 characters (combined with “title” field) and it will be bold</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Moisturizing Mask</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>text</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>For WhatsApp, max length is 4096 characters (combined with “title” field)</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>On sales 20% off</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>buttons</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Array of Button Object</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>For WhatsApp, you can have up to 3 buttons.</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>url</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Link of clicking message image.<br>Not supported in WhatsApp.</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p><code>https://www.example.com</code></p>
</td>
</tr>
</tbody>
</table>
`}</HTMLBlock>
***

#### LINE Image Carousel Object

| Field Name | Data Type              | Required | Description                             | Example                             |
| :--------- | :--------------------- | :------- | :-------------------------------------- | :---------------------------------- |
| image      | String                 | Y        | Carousel image                          | `https://www.example.com/image.png` |
| action     | Action Object          | Y        | Action when clicking the carousel image |                                     |
| buttons    | Array of Button Object | Y        | Buttons                                 |                                     |

***

#### Button Object

 <HTMLBlock>{`
<table style="width: 100%; border-collapse: collapse;">
<thead>
<tr>
  <th style="border: 1px solid #ddd; padding: 8px;">Field Name</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Data Type</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Required</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Description</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Example</th>
</tr>
</thead>
<tbody>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>type</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Button type:<br>Supported values:  </p>
<ul>
<li><strong>postback</strong>: trigger chatbot message  </li>
<li><strong>url</strong>: website link  </li>
<li><strong>message</strong>: send a text message</li>
</ul>
<p>For WhatsApp, if use type=url, the url will append to the message body</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>postback</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>title</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Message title  </p>
<p>For WhatsApp, max length: 20 characters</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>More Info</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>blockId</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y if type=postback</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Bot Block ID in Omnichat system</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>8d1f060f-3e0d-4f52-9837-4920e9b4406d</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>tags</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Array of String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>N</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Tags to be added when user clicks the button</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>[“Mask”]</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>attribute</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Attribute Object</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>N</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Attributes to be added when user clicks the button</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>url</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y if type=url</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Message sent to the user when clicking the button</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>message</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y if type=message</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>style</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y for LINE carousel image</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Button style  </p>
<p>Supported values:  </p>
<ul>
<li><strong>primary</strong>  </li>
<li><strong>secondary</strong></li>
</ul>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>color</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y for LINE carousel image</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Button color hex code</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
</tr>
</tbody>
</table>
`}</HTMLBlock>
***

#### Action Object

<HTMLBlock>{`
<table style="width: 100%; border-collapse: collapse;">
<thead>
<tr>
  <th style="border: 1px solid #ddd; padding: 8px;">Field Name</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Data Type</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Required</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Description</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Example</th>
</tr>
</thead>
<tbody>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>type</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Button type  </p>
<p>Supported values:  </p>
<ul>
<li><strong>postback</strong>: trigger chatbot message  </li>
<li><strong>url</strong>: website link  </li>
<li><strong>message</strong>: send a text message</li>
</ul>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>postback</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>blockId</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y if type=postback</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Bot Block ID in Omnichat system</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>tags</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Array of String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>N</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Tags to be added when user clicks the button</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>attribute</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Attribute Object</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>N</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Attributes to be added when user clicks the button</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>url</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y if type=url</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>message</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y if type=message</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>The Message sent to users when clicking</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
</tr>
</tbody>
</table>
`}</HTMLBlock>
***

#### Attribute Object

| Field Name | Data Type | Required | Description     | Example  |
| :--------- | :-------- | :------- | :-------------- | :------- |
| key        | String    | Y        | Attribute key   | MaskType |
| value      | String    | Y        | Attribute value | Moisture |

***

#### Option List Object

<HTMLBlock>{`
<table style="width: 100%; border-collapse: collapse;">
<thead>
<tr>
  <th style="border: 1px solid #ddd; padding: 8px;">Field Name</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Data Type</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Required</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Description</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Example</th>
</tr>
</thead>
<tbody>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>text</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Message body<br>Max length: 1024 characters</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>buttonTitle</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Option list button title<br>Max length: 20 characters</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>options</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Array of Option Object</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Options</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
</tr>
</tbody>
</table>
`}</HTMLBlock>

***

#### Option Object

<HTMLBlock>{`
<table style="width: 100%; border-collapse: collapse;">
<thead>
<tr>
  <th style="border: 1px solid #ddd; padding: 8px;">Field Name</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Data Type</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Required</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Description</th>
  <th style="border: 1px solid #ddd; padding: 8px;">Example</th>
</tr>
</thead>
<tbody>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>type</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Button type  </p>
<p>Supported values:  </p>
<ul>
<li><strong>postback</strong>: trigger chatbot message</li>
</ul>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>postback</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>title</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Option title<br>Max length: 24 characters</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Option 1</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>description</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Option description<br>Max length: 72 characters</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Option 1 Description</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>botId</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Chatbot ID in Omnichat system</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>8d1f060f-3e0d-4f52-9837-4920e9b4406d</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>blockId</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Y</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Chatbot Block ID in Omnichat system</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>8d1f060f-3e0d-4f52-9837-4920e9b4406d</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>tags</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Array of String</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>N</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Tags to be added when user clicks the button</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>[“Mask”]</p>
</td>
</tr>
<tr>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>attribute</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Attribute Object</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>N</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"><p>Attributes to be added when user clicks the button</p>
</td>
  <td style="border: 1px solid #ddd; padding: 8px;"></td>
</tr>
</tbody>
</table>
`}</HTMLBlock>