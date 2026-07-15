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

    res = paygentic.events.ingest(request={
        "type": "ai.inference",
        "source": "https://api.myapp.com",
        "subject": "cus_abc123",
        "data": {
            "tokens": 1500,
            "model": "gpt-4o",
        },
    })

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `request`                                                           | [models.IngestEventRequest](../../models/ingesteventrequest.md)     | :heavy_check_mark:                                                  | The request object to use for the request.                          |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

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