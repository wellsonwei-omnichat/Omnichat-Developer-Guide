---
title: Channels API
deprecated: false
hidden: false
metadata:
  robots: index
---
# Get Team Channels Info API

Get Channel Info

## Endpoint

**GET** [https://open-api.omnichat.ai/v1/channels](https://open-api.omnichat.ai/v1/channels)

## Response Body

### Success - HTTP Status 200

Array of `Channel` Objects

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

    <tr>
      <td>
        channelName
      </td>

      <td>
        String
      </td>

      <td>
        N
      </td>

      <td>
        Channel name / Team Name if `platform` is `web`
      </td>
    </tr>
  </tbody>
</Table>

<br />

<br />

<br />
