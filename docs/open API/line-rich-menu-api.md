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

| Field   | Type   | Description                                              |
| :------ | :----- | :------------------------------------------------------- |
| content | Object | Wrapper object containing the rich menu details         |

### Content object

| Field  | Type   | Description                                                                 |
|--------|--------|------------------------------------------------------------------------------|
| id     | String | Unique identifier of the rich menu                                          |
| name   | String | Display name of the rich menu                                               |
| status | String | Current status of the rich menu. Possible values:                           |
|        |        | - `DRAFT`: Menu is being edited and not yet scheduled                       |
|        |        | - `SCHEDULED`: Menu is scheduled for future publishing                      |
|        |        | - `PUBLISHED`: Menu is currently active                                     |
|        |        | - `HALT`: Publishing is paused                                              |
|        |        | - `FINISHED`: Menu publishing has ended       

# Get A Rich Menu Details

## Endpoint

**GET** `https://open-api.omnichat.ai/v1/rich-menus/{menu_id}`