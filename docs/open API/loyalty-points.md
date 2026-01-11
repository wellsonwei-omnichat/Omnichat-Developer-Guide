---
title: Loyalty APIs
deprecated: false
hidden: false
metadata:
  robots: index
---
# Loyalty APIs

APIs for managing customer loyalty points.

## Subscription Required

| Feature Toggle | Description |
|----------------|-------------|
| `open_api_loyalty_point` | Loyalty Points Open API Module - Required for adjusting loyalty points |
| `open_api` | Open API Module - Base requirement |

---

# Adjust Loyalty Points

Adjust (add/deduct) a contact's loyalty points using phone number, email, or member ID.

## Endpoint

**PUT** `https://open-api.omnichat.ai/v1/loyalty-points/action/adjust`

## Request Headers

| Header | Value | Description |
| :----- | :---- | :---------- |
| Authorization | Bearer \{API_TOKEN\} | API Token from Omnichat |
| Content-Type | application/json | - |

## Request Body

<Table align={["left","left","left","left"]}>
  <thead>
    <tr>
      <th>Field</th>
      <th>Type</th>
      <th>Required</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>phone</td>
      <td>String</td>
      <td>Conditional</td>
      <td>Phone number. One of phone, email, or memberId is required. Must be numeric.</td>
    </tr>
    <tr>
      <td>email</td>
      <td>String</td>
      <td>Conditional</td>
      <td>Email address. One of phone, email, or memberId is required.</td>
    </tr>
    <tr>
      <td>memberId</td>
      <td>String</td>
      <td>Conditional</td>
      <td>Member ID. One of phone, email, or memberId is required.</td>
    </tr>
    <tr>
      <td>points</td>
      <td>Integer</td>
      <td>Yes</td>
      <td>Amount of loyalty points to adjust. Use negative value for deduction.</td>
    </tr>
  </tbody>
</Table>

> 📘 Note
> You can only use the field configured as the identifier for loyalty points in your Omnichat portal.

## Response

**Success** - HTTP Status 200 with empty response body

**Error** - HTTP Status 4xx / 5xx

```json
{
  "errorCode": "INVALID_REQUEST_BODY",
  "message": "phone number must be numeric"
}
```

## Examples

### Adjust using Phone Number

```json
{
  "phone": "852912345678",
  "points": 10
}
```

### Adjust using Email

```json
{
  "email": "john.doe@omnichat.ai",
  "points": 10
}
```

### Adjust using Member ID

```json
{
  "memberId": "123456",
  "points": 10
}
```

### Deduct Points

```json
{
  "phone": "852912345678",
  "points": -50
}
```
