# Revenue

## Overview

Time-series revenue data with component breakdown including usage, fees, and refunds

### Available Operations

* [get](#get) - Get revenue time series

## get

Returns time-bucketed revenue data including usage charges, fee charges, and refunds. Data is aggregated by subscription with an optional 'other' bucket for subscriptions outside the top N.

### Example Usage

<!-- UsageSnippet language="python" operationID="getRevenue" method="get" path="/v0/revenue" -->
```python
import os
from paygentic_sdk import Paygentic
from paygentic_sdk.utils import parse_datetime


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.revenue.get(start_time=parse_datetime("2024-07-23T16:05:39.311Z"), end_time=parse_datetime("2026-04-29T18:43:05.586Z"), bucket_width="hour", top_n=10)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                | Type                                                                                                     | Required                                                                                                 | Description                                                                                              |
| -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| `start_time`                                                                                             | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                     | :heavy_check_mark:                                                                                       | Start of the time range (ISO 8601 format)                                                                |
| `end_time`                                                                                               | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                     | :heavy_check_mark:                                                                                       | End of the time range (ISO 8601 format)                                                                  |
| `bucket_width`                                                                                           | [Optional[models.BucketWidth]](../../models/bucketwidth.md)                                              | :heavy_minus_sign:                                                                                       | Time bucket granularity                                                                                  |
| `merchant_id`                                                                                            | *Optional[str]*                                                                                          | :heavy_minus_sign:                                                                                       | Filter by merchant ID. At least one of merchantId, subscriptionIds, or customerId must be provided.      |
| `customer_id`                                                                                            | *Optional[str]*                                                                                          | :heavy_minus_sign:                                                                                       | Filter by customer ID. At least one of merchantId, subscriptionIds, or customerId must be provided.      |
| `subscription_ids`                                                                                       | List[*str*]                                                                                              | :heavy_minus_sign:                                                                                       | Filter by subscription IDs. At least one of merchantId, subscriptionIds, or customerId must be provided. |
| `top_n`                                                                                                  | *Optional[int]*                                                                                          | :heavy_minus_sign:                                                                                       | Limit to top N subscriptions by net revenue. Remaining subscriptions are aggregated into 'other'.        |
| `retries`                                                                                                | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                         | :heavy_minus_sign:                                                                                       | Configuration to override the default retry behavior of the client.                                      |

### Response

**[models.RevenueTimeSeriesResponse](../../models/revenuetimeseriesresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |