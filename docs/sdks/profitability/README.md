# Profitability

## Overview

Per-customer profitability summaries

### Available Operations

* [get_profitability](#get_profitability) - Get profitability summary

## get_profitability

Returns a per-customer profitability summary for a merchant over a date range. Each row aggregates revenue (from issued + paid invoices), cost (from metered cost discovery), profit, and margin. Customers are ranked by profit descending and capped at topN; the remainder is rolled into a single self-consistent 'Other' row whose revenue, cost, and profit reflect the same set of customers. Rows are inner-joined against the merchant's customer list, so orphaned meter subjects from deleted or unknown customers are dropped.

### Example Usage

<!-- UsageSnippet language="python" operationID="getProfitability" method="get" path="/v0/profitability" -->
```python
import os
from paygentic_sdk import Paygentic
from paygentic_sdk.utils import parse_datetime


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.profitability.get_profitability(merchant_id="<id>", from_=parse_datetime("2026-09-10T15:32:06.535Z"), to=parse_datetime("2026-10-20T08:45:45.521Z"), top_n=10, bucket_width="day")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                              | Type                                                                                                                                   | Required                                                                                                                               | Description                                                                                                                            |
| -------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `merchant_id`                                                                                                                          | *str*                                                                                                                                  | :heavy_check_mark:                                                                                                                     | Merchant whose customers to summarize                                                                                                  |
| `from_`                                                                                                                                | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                   | :heavy_check_mark:                                                                                                                     | Start of the time range (ISO 8601 format)                                                                                              |
| `to`                                                                                                                                   | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                   | :heavy_check_mark:                                                                                                                     | End of the time range (ISO 8601 format)                                                                                                |
| `top_n`                                                                                                                                | *Optional[int]*                                                                                                                        | :heavy_minus_sign:                                                                                                                     | Number of top customers (by profit) to return individually. The rest are rolled into a single 'Other' row.                             |
| `currency`                                                                                                                             | *Optional[str]*                                                                                                                        | :heavy_minus_sign:                                                                                                                     | ISO 4217 currency code to scope the summary. Defaults to the merchant's primary currency.                                              |
| `bucket_width`                                                                                                                         | [Optional[models.GetProfitabilityBucketWidth]](../../models/getprofitabilitybucketwidth.md)                                            | :heavy_minus_sign:                                                                                                                     | Time bucket granularity for the per-customer revenue trend. When omitted, the server picks a reasonable bucket from the window length. |
| `retries`                                                                                                                              | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                       | :heavy_minus_sign:                                                                                                                     | Configuration to override the default retry behavior of the client.                                                                    |

### Response

**[models.ProfitabilitySummaryResponse](../../models/profitabilitysummaryresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |