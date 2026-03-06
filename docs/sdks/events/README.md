# Events

## Overview

Ingest raw metering events that are processed by the meters service.

### Available Operations

* [ingest](#ingest) - Ingest Event

## ingest

Ingest a raw metering event. The event is published to the meter-events PubSub topic for processing by the meters service.

### Example Usage

<!-- UsageSnippet language="python" operationID="ingestEvent" method="post" path="/v0/events" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.events.ingest(type_="<value>", source="<value>", subject="<value>", data={
        "key": "<value>",
        "key1": "<value>",
    })

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                         | Type                                                                                                                              | Required                                                                                                                          | Description                                                                                                                       |
| --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `type`                                                                                                                            | *str*                                                                                                                             | :heavy_check_mark:                                                                                                                | CloudEvents type. Must match an eventType configured on a BillableMetric.                                                         |
| `source`                                                                                                                          | *str*                                                                                                                             | :heavy_check_mark:                                                                                                                | Event source URI identifying the application.                                                                                     |
| `subject`                                                                                                                         | *str*                                                                                                                             | :heavy_check_mark:                                                                                                                | Customer or entity ID this event relates to.                                                                                      |
| `data`                                                                                                                            | Dict[str, *Any*]                                                                                                                  | :heavy_check_mark:                                                                                                                | Event payload containing the metering data.                                                                                       |
| `namespace`                                                                                                                       | *Optional[str]*                                                                                                                   | :heavy_minus_sign:                                                                                                                | Organization/merchant ID. Defaults to the authenticated user's organization. Platform users can specify a different organization. |
| `timestamp`                                                                                                                       | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                              | :heavy_minus_sign:                                                                                                                | Event timestamp. Defaults to server time if not provided.                                                                         |
| `idempotency_key`                                                                                                                 | *Optional[str]*                                                                                                                   | :heavy_minus_sign:                                                                                                                | User-provided deduplication key. If not provided, a unique key is generated.                                                      |
| `retries`                                                                                                                         | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                  | :heavy_minus_sign:                                                                                                                | Configuration to override the default retry behavior of the client.                                                               |

### Response

**[models.EventResponse](../../models/eventresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 422                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |