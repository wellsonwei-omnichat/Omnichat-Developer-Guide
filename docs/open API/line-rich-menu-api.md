---
title: Line Rich Menu API
deprecated: false
hidden: true
metadata:
  robots: index
---
# Get Rich Menu List

## Endpoint

**GET** `https://open-api.omnichat.ai/v1/rich-menus`

## Response body

| Field   | Type  | Description               |
| :------ | :---- | :------------------------ |
| content | Array | List of team's rich menus |

### Rich menu object

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
        id
      </td>

      <td>
        String
      </td>

      <td>
        Unique identifier of the rich menu
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
        Display name of the rich menu
      </td>
    </tr>

    <tr>
      <td>
        status
      </td>

      <td>
        String
      </td>

      <td>
        Current status of the rich menu
        `DRAFT`: Menu is being edited and not yet scheduled
        `SCHEDULED`: Menu is scheduled for future publishing
        `PUBLISHED`: Menu is currently active
        `HALT`: Publishing is paused
        `FINISHED`: Menu publishing has ended
      </td>
    </tr>
  </tbody>
</Table>

# Get A Rich Menu Details

## Endpoint

**GET** `https://open-api.omnichat.ai/v1/rich-menus/{menu_id}`

## Response body

| Field   | Type   | Description                                     |
| :------ | :----- | :---------------------------------------------- |
| content | Object | Wrapper object containing the rich menu details |

### Rich menu object

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
        area
      </td>

      <td>
        String
      </td>

      <td>
        Area name of the rich menu
      </td>
    </tr>

    <tr>
      <td>
        actionType
      </td>

      <td>
        String
      </td>

      <td>
        Type of action triggered when this area is clicked
        `message`, `postback`, `url`, `menu_switch`, `certified_provider`
      </td>
    </tr>

    <tr>
      <td>
        actionContent
      </td>

      <td>
        String
      </td>

      <td>
        Content associated with the action
        `message`: the text content that will be sent when the area is clicked
        `postback`: the name of the chatbot and message block to be triggered, in the format: (chatbot name) > (message block name)
        `url`: the target URL that the user will be redirected to
        `menu_switch`: the name of the rich menu to switch to
        `certified_provider`: no associated content
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
        Total number of times this area has been clicked
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
        Percentage of total clicks represented by this area
      </td>
    </tr>
  </tbody>
</Table>