---
title: Broadcast APIs
deprecated: false
hidden: false
metadata:
  robots: index
---
# Get Click Statistics of Buttons in Broadcast

## Endpoint

GET `https://open-api.omnichat.ai/v1/broadcast/{broadcast_id}/buttons`

## Response body

| Field   | Type  | Description                                                            |
| :------ | :---- | :--------------------------------------------------------------------- |
| content | Array | List of the buttons of a specific broadcast and their click statistics |

### Click statistics object

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Field
      </th>

      <th>
        Type
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        messageIndex
      </td>

      <td>
        Integer
      </td>

      <td>
        Index of the message this button belongs to (starting from 0, based on the original broadcast message order)
      </td>
    </tr>

    <tr>
      <td>
        cardIndex
      </td>

      <td>
        Integer
      </td>

      <td>
        Indicates the index of the card the button belongs to if the message is a card-type message (e.g., carousel card); otherwise, it is 0.
      </td>
    </tr>

    <tr>
      <td>
        buttonIndex
      </td>

      <td>
        Integer
      </td>

      <td>
        Index of the button within its card or message (starting from 1 for visible buttons)<br />
        0 refers to the card’s default action, which is triggered by tapping on the image area. This only applies to card-type messages.
      </td>
    </tr>

    <tr>
      <td>
        clickedCount
      </td>

      <td>
        Integer
      </td>

      <td>
        Total number of times this button has been clicked
      </td>
    </tr>

    <tr>
      <td>
        clickedPercentage
      </td>

      <td>
        String
      </td>

      <td>
        Percentage of total clicks represented by this button (e.g., "23.45%")
      </td>
    </tr>
  </tbody>
</Table>