# Revenue

## Overview

Revenue data from invoices and payments

### Available Operations

* [get](#get) - Get revenue summary

## get

Returns revenue summary with invoice and payment breakdowns (outstanding/paid/writtenOff), plus a time-series trend. Revenue is sourced from all issued invoices (v0 + v1) and completed payments.

### Example Usage

<!-- UsageSnippet language="python" operationID="getRevenue" method="get" path="/v0/revenue" -->
```python
import os
from paygentic_sdk import Paygentic
from paygentic_sdk.utils import parse_datetime


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.revenue.get(start_time=parse_datetime("2024-07-23T16:05:39.311Z"), end_time=parse_datetime("2026-04-29T18:43:05.586Z"), bucket_width="day", merchant_id="org_YS8jkP59V71TdUvj")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                | Type                                                                                                     | Required                                                                                                 | Description                                                                                              |
| -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| `start_time`                                                                                             | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                     | :heavy_check_mark:                                                                                       | Start of the time range (ISO 8601 format)                                                                |
| `end_time`                                                                                               | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                     | :heavy_check_mark:                                                                                       | End of the time range (ISO 8601 format)                                                                  |
| `bucket_width`                                                                                           | [Optional[models.BucketWidth]](../../models/bucketwidth.md)                                              | :heavy_minus_sign:                                                                                       | Time bucket granularity for trend data                                                                   |
| `merchant_id`                                                                                            | *Optional[str]*                                                                                          | :heavy_minus_sign:                                                                                       | Filter by merchant ID. At least one of merchantId, subscriptionIds, or customerId must be provided.      |
| `customer_id`                                                                                            | *Optional[str]*                                                                                          | :heavy_minus_sign:                                                                                       | Filter by customer ID. At least one of merchantId, subscriptionIds, or customerId must be provided.      |
| `subscription_ids`                                                                                       | List[*str*]                                                                                              | :heavy_minus_sign:                                                                                       | Filter by subscription IDs. At least one of merchantId, subscriptionIds, or customerId must be provided. |
| `group_by`                                                                                               | [Optional[models.GroupBy]](../../models/groupby.md)                                                      | :heavy_minus_sign:                                                                                       | Group invoice data by dimension. Max 5 groups (top 4 + 'other' when exceeding).                          |
| `retries`                                                                                                | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                         | :heavy_minus_sign:                                                                                       | Configuration to override the default retry behavior of the client.                                      |

### Response

**[models.RevenueSummaryResponse](../../models/revenuesummaryresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |