# UsageEvents

## Overview

### Available Operations

* [create](#create) - Create
* [list](#list) - List
* [get](#get) - Get
* [refund](#refund) - Refund
* [batch_create](#batch_create) - Batch Create

## create

Creates a usage event. The idempotencyKey is used to ensure the event is processed only once by downstream consumers, even if the same event is submitted multiple times. Duplicate submissions will be accepted and return the same response.

### Example Usage

<!-- UsageSnippet language="python" operationID="createUsageEvent" method="post" path="/v0/usage" -->
```python
import os
from paygentic_sdk import Paygentic
from paygentic_sdk.utils import parse_datetime


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.usage_events.create(customer_id="<id>", idempotency_key="<value>", merchant_id="<id>", properties=[], timestamp=parse_datetime("2026-05-14T00:54:35.100Z"))

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                                                                                                     | Type                                                                                                                                                                                                                                                                                                                                          | Required                                                                                                                                                                                                                                                                                                                                      | Description                                                                                                                                                                                                                                                                                                                                   |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `customer_id`                                                                                                                                                                                                                                                                                                                                 | *str*                                                                                                                                                                                                                                                                                                                                         | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                            | Customer identifier that generated this consumption event. Sample values: 'cus_abc123xyz', 'cus_789def456'                                                                                                                                                                                                                                    |
| `idempotency_key`                                                                                                                                                                                                                                                                                                                             | *str*                                                                                                                                                                                                                                                                                                                                         | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                            | Unique deduplication key preventing duplicate event processing. Sample values: 'usg_2024_01_15_abc123', 'event_wallet_xyz789', 'consumption_ref_456def'                                                                                                                                                                                       |
| `merchant_id`                                                                                                                                                                                                                                                                                                                                 | *str*                                                                                                                                                                                                                                                                                                                                         | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                            | Merchant organization identifier owning this consumption event. Sample values: 'org_abc123xyz', 'org_789def456'                                                                                                                                                                                                                               |
| `properties`                                                                                                                                                                                                                                                                                                                                  | List[[models.CreateUsageEventRequestProperty](../../models/createusageeventrequestproperty.md)]                                                                                                                                                                                                                                               | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                            | N/A                                                                                                                                                                                                                                                                                                                                           |
| `timestamp`                                                                                                                                                                                                                                                                                                                                   | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                            | Actual occurrence timestamp for the consumption event in ISO 8601 format. Sample values: '2024-01-15T10:30:00Z', '2024-02-01T14:45:30Z'. Represents when the event occurred, not when Paygentic received it.                                                                                                                                  |
| `entitlement_id`                                                                                                                                                                                                                                                                                                                              | *Optional[str]*                                                                                                                                                                                                                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                            | Commitment identifier for this consumption event. Sample values: 'com_abc123xyz', 'com_789def456'                                                                                                                                                                                                                                             |
| `metadata`                                                                                                                                                                                                                                                                                                                                    | Dict[str, *str*]                                                                                                                                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                            | Custom key-value attributes providing context about the consumption event. Sample values: {"model_name": "claude-3-opus", "input_tokens": "1500", "output_tokens": "800"} or {"storage_tier": "premium", "data_center": "eu-west-1", "encryption": "enabled"} or {"image_resolution": "1024x1024", "generation_model": "stable-diffusion-xl"} |
| `retries`                                                                                                                                                                                                                                                                                                                                     | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                            | Configuration to override the default retry behavior of the client.                                                                                                                                                                                                                                                                           |

### Response

**[models.UsageEvent](../../models/usageevent.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403                          | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## list

List

### Example Usage

<!-- UsageSnippet language="python" operationID="listUsageEvents" method="get" path="/v0/usage" -->
```python
import os
from paygentic_sdk import Paygentic
from paygentic_sdk.utils import parse_datetime


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.usage_events.list(end_time=parse_datetime("2026-03-29T00:23:32.822Z"), start_time=parse_datetime("2024-02-04T03:47:15.138Z"), limit=10, offset=0)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                    | Type                                                                                                                                         | Required                                                                                                                                     | Description                                                                                                                                  |
| -------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| `end_time`                                                                                                                                   | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                         | :heavy_check_mark:                                                                                                                           | ISO 8601 date-time string filtering events up to this timestamp. Sample values: '2024-01-31T23:59:59Z', '2024-02-28T12:00:00Z'               |
| `start_time`                                                                                                                                 | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                         | :heavy_check_mark:                                                                                                                           | ISO 8601 date-time string filtering events from this timestamp onward. Sample values: '2024-01-15T00:00:00Z', '2024-02-01T10:30:00Z'         |
| `consumer_id`                                                                                                                                | *Optional[str]*                                                                                                                              | :heavy_minus_sign:                                                                                                                           | Filter by consumer ID. This is only available if the caller is member of the consumer organization.                                          |
| `customer_id`                                                                                                                                | *Optional[str]*                                                                                                                              | :heavy_minus_sign:                                                                                                                           | Filter by customer ID. This is only available if the caller is member of the merchant organization owning this customer.                     |
| `limit`                                                                                                                                      | *Optional[int]*                                                                                                                              | :heavy_minus_sign:                                                                                                                           | Number of usage events to return                                                                                                             |
| `merchant_id`                                                                                                                                | *Optional[str]*                                                                                                                              | :heavy_minus_sign:                                                                                                                           | Filter by merchant ID. This is only available if the caller is member of the merchant organization.                                          |
| `offset`                                                                                                                                     | *Optional[int]*                                                                                                                              | :heavy_minus_sign:                                                                                                                           | Number of usage events to skip                                                                                                               |
| `subscription_id`                                                                                                                            | *Optional[str]*                                                                                                                              | :heavy_minus_sign:                                                                                                                           | Filter by subscription ID. This is only available if the caller is member of the consumer or merchant organization owning this subscription. |
| `retries`                                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                             | :heavy_minus_sign:                                                                                                                           | Configuration to override the default retry behavior of the client.                                                                          |

### Response

**[models.ListUsageEventsResponse](../../models/listusageeventsresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403                          | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get

Get

### Example Usage

<!-- UsageSnippet language="python" operationID="getUsageEvent" method="get" path="/v0/usage/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.usage_events.get(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.UsageEvent](../../models/usageevent.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## refund

Marks a usage event as refunded. This reverts the consumption recorded by the usage event and creates a corresponding refund billing event if the usage event was already billed.

### Example Usage

<!-- UsageSnippet language="python" operationID="refundUsageEvent" method="patch" path="/v0/usage/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.usage_events.refund(id="<id>", refunded=False)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                       | Type                                                                                                                            | Required                                                                                                                        | Description                                                                                                                     |
| ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                            | *str*                                                                                                                           | :heavy_check_mark:                                                                                                              | N/A                                                                                                                             |
| `refunded`                                                                                                                      | *bool*                                                                                                                          | :heavy_check_mark:                                                                                                              | Set to true to mark the usage event as refunded. Once refunded, the event cannot be un-refunded.                                |
| `reason`                                                                                                                        | *Optional[str]*                                                                                                                 | :heavy_minus_sign:                                                                                                              | Optional reason for the refund. Sample values: 'Customer request', 'Billing error', 'Service credit', 'System error correction' |
| `retries`                                                                                                                       | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                | :heavy_minus_sign:                                                                                                              | Configuration to override the default retry behavior of the client.                                                             |

### Response

**[models.UsageEvent](../../models/usageevent.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404, 422                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## batch_create

Creates multiple usage events in a single request. The idempotencyKey for each event is used to ensure the event is processed only once by downstream consumers, even if the same event is submitted multiple times. Duplicate submissions will be accepted and return the same response.

### Example Usage

<!-- UsageSnippet language="python" operationID="batchCreateUsageEvents" method="post" path="/v0/usage/batch" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.usage_events.batch_create(events=[])

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                       | Type                                                                            | Required                                                                        | Description                                                                     |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| `events`                                                                        | List[[models.CreateUsageEventRequest](../../models/createusageeventrequest.md)] | :heavy_check_mark:                                                              | N/A                                                                             |
| `retries`                                                                       | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                | :heavy_minus_sign:                                                              | Configuration to override the default retry behavior of the client.             |

### Response

**[models.BatchUsageEventResponse](../../models/batchusageeventresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403                          | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |