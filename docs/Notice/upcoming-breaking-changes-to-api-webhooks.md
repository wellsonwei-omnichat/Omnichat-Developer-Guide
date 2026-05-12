---
title: Upcoming Breaking Changes to API / Webhooks
deprecated: false
hidden: false
metadata:
  robots: index
---
**Starting July 29, 2026, the API will return a 429 error code if the Open API rate limit is exceeded**

* Requests exceeding the rate limit will trigger a 429 Too Many Requests error.
* A `Retry-After` header will be provided in 429 responses to indicate the required wait time (in seconds) before the next retry.
