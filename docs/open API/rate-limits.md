---
title: Rate Limits
deprecated: false
hidden: false
metadata:
  robots: index
---
A rate limit is the number of requests the API can receive in a given time period. Default API rate limit is 40 requests per second per Omnichat Team account.

The following updates will take effect starting July 29, 2026:

* Requests exceeding the rate limit will trigger a 429 Too Many Requests error.
* A `Retry-After` header will be provided in 429 responses to indicate the required wait time (in seconds) before the next retry.

<br />
