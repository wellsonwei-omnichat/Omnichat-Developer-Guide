---
title: Line Rich Menu API
deprecated: false
hidden: true
metadata:
  robots: index
---
# Get All Rich Menu List

## Endpoint

**GET** `https://open-api.omnichat.ai/v1/rich-menus`

## Response body

| Field   | Type   | Description                                     |
| :------ | :----- | :---------------------------------------------- |
| content | Object | Wrapper object containing the rich menu details |

### Content object

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