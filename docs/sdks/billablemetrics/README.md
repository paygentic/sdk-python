# BillableMetrics

## Overview

### Available Operations

* [create](#create) - Create
* [list](#list) - List
* [get](#get) - Get
* [update](#update) - Update
* [meter](#meter) - Query Meter Usage

## create

Create a new billable metric for a merchant organization. A `Billable Metric` represents a metric that can be used to measure the usage of a `Product`. It contains information about the metric, such as its name, description, and units.

### Example Usage

<!-- UsageSnippet language="python" operationID="createBillableMetric" method="post" path="/v0/billableMetrics" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billable_metrics.create(aggregation="SUM", description="orange daily out slow nor smoothly", merchant_id="<id>", name="<value>", product_id="<id>", unit="meter")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                                                                                                                                                   | Type                                                                                                                                                                                                                                                                                                                                                                                        | Required                                                                                                                                                                                                                                                                                                                                                                                    | Description                                                                                                                                                                                                                                                                                                                                                                                 |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `aggregation`                                                                                                                                                                                                                                                                                                                                                                               | [models.CreateBillableMetricAggregation](../../models/createbillablemetricaggregation.md)                                                                                                                                                                                                                                                                                                   | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                                                          | Aggregation calculation method for metric values.                                                                                                                                                                                                                                                                                                                                           |
| `description`                                                                                                                                                                                                                                                                                                                                                                               | *str*                                                                                                                                                                                                                                                                                                                                                                                       | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                                                          | Explanatory text describing what the metric tracks and how it's used for billing. Sample values: 'Total tokens consumed by Claude language model interactions', 'Gigabytes of cloud storage utilized', 'Count of machine learning inference requests processed', 'Quantity of AI-generated images created', 'Compute hours spent training neural networks', 'Terabytes of data transferred' |
| `merchant_id`                                                                                                                                                                                                                                                                                                                                                                               | *str*                                                                                                                                                                                                                                                                                                                                                                                       | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                                                          | Unique identifier for an organization                                                                                                                                                                                                                                                                                                                                                       |
| `name`                                                                                                                                                                                                                                                                                                                                                                                      | *str*                                                                                                                                                                                                                                                                                                                                                                                       | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                                                          | Human-readable label identifying what this metric measures. Sample values: 'Claude Tokens', 'Storage Capacity', 'Model Inference Calls', 'Generated Images', 'Training Compute Hours', 'Data Transfer Volume'                                                                                                                                                                               |
| `product_id`                                                                                                                                                                                                                                                                                                                                                                                | *str*                                                                                                                                                                                                                                                                                                                                                                                       | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                                                          | Unique identifier for a product                                                                                                                                                                                                                                                                                                                                                             |
| `unit`                                                                                                                                                                                                                                                                                                                                                                                      | *str*                                                                                                                                                                                                                                                                                                                                                                                       | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                                                          | Measurement unit used when aggregating this metric's values. Common examples: 'tokens', 'GB', 'calls', 'images', 'hours', 'TB', 'queries', 'requests'                                                                                                                                                                                                                                       |
| `event_type`                                                                                                                                                                                                                                                                                                                                                                                | *Optional[str]*                                                                                                                                                                                                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                          | CloudEvents type for meter routing. Links this billable metric to the metering service.                                                                                                                                                                                                                                                                                                     |
| `value_property`                                                                                                                                                                                                                                                                                                                                                                            | *Optional[str]*                                                                                                                                                                                                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                          | JSONPath to extract numeric value from event data. Required for SUM/AVG/MIN/MAX/LATEST aggregations.                                                                                                                                                                                                                                                                                        |
| `group_by`                                                                                                                                                                                                                                                                                                                                                                                  | Dict[str, *str*]                                                                                                                                                                                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                          | Map of dimension name to JSONPath for group-by queries.                                                                                                                                                                                                                                                                                                                                     |
| `event_from`                                                                                                                                                                                                                                                                                                                                                                                | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                                                                                                                                                                                                                        | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                          | Only count events after this timestamp. Used for meter versioning.                                                                                                                                                                                                                                                                                                                          |
| `retries`                                                                                                                                                                                                                                                                                                                                                                                   | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                          | Configuration to override the default retry behavior of the client.                                                                                                                                                                                                                                                                                                                         |

### Response

**[models.BillableMetric](../../models/billablemetric.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## list

List

### Example Usage

<!-- UsageSnippet language="python" operationID="listBillableMetrics" method="get" path="/v0/billableMetrics" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billable_metrics.list(merchant_id="<id>", limit=10, offset=0)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `merchant_id`                                                       | *str*                                                               | :heavy_check_mark:                                                  | Filter billable metrics by merchant organization ID.                |
| `limit`                                                             | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | Number of billable metrics to return.                               |
| `offset`                                                            | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | Number of billable metrics to skip.                                 |
| `product_id`                                                        | *Optional[str]*                                                     | :heavy_minus_sign:                                                  | Filter billable metrics by product ID.                              |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.ListBillableMetricsResponse](../../models/listbillablemetricsresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get

Get

### Example Usage

<!-- UsageSnippet language="python" operationID="getBillableMetric" method="get" path="/v0/billableMetrics/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billable_metrics.get(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.BillableMetric](../../models/billablemetric.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## update

Update

### Example Usage

<!-- UsageSnippet language="python" operationID="updateBillableMetric" method="patch" path="/v0/billableMetrics/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billable_metrics.update(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                     | Type                                                                                                                                                                                                          | Required                                                                                                                                                                                                      | Description                                                                                                                                                                                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                                                                                          | *str*                                                                                                                                                                                                         | :heavy_check_mark:                                                                                                                                                                                            | N/A                                                                                                                                                                                                           |
| `description`                                                                                                                                                                                                 | *Optional[str]*                                                                                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                                            | Revised explanation of what the metric represents. Sample values: 'Language model token consumption', 'Database storage capacity used', 'Machine learning prediction API calls', 'AI-generated content items' |
| `name`                                                                                                                                                                                                        | *Optional[str]*                                                                                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                                            | Updated label for the metric. Sample values: 'LLM Tokens', 'Database Storage', 'Prediction Requests', 'Content Generations'                                                                                   |
| `unit`                                                                                                                                                                                                        | *Optional[str]*                                                                                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                                            | Updated measurement unit. Common examples: 'tokens', 'GB', 'requests', 'items', 'hours'                                                                                                                       |
| `event_type`                                                                                                                                                                                                  | *OptionalNullable[str]*                                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                            | CloudEvents type for meter routing.                                                                                                                                                                           |
| `value_property`                                                                                                                                                                                              | *OptionalNullable[str]*                                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                            | JSONPath to extract numeric value from event data.                                                                                                                                                            |
| `group_by`                                                                                                                                                                                                    | Dict[str, *str*]                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                            | Map of dimension name to JSONPath for group-by queries.                                                                                                                                                       |
| `event_from`                                                                                                                                                                                                  | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                                            | Only count events after this timestamp.                                                                                                                                                                       |
| `retries`                                                                                                                                                                                                     | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                            | Configuration to override the default retry behavior of the client.                                                                                                                                           |

### Response

**[models.BillableMetric](../../models/billablemetric.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## meter

Query aggregated usage data for a billable metric from the metering service.

### Example Usage

<!-- UsageSnippet language="python" operationID="getBillableMetricMeter" method="get" path="/v0/billableMetrics/{id}/meter" -->
```python
import os
from paygentic_sdk import Paygentic
from paygentic_sdk.utils import parse_datetime


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billable_metrics.meter(id="<id>", from_=parse_datetime("2024-12-02T03:30:12.536Z"), to=parse_datetime("2024-06-19T00:01:21.924Z"))

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                            | Type                                                                 | Required                                                             | Description                                                          |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `id`                                                                 | *str*                                                                | :heavy_check_mark:                                                   | N/A                                                                  |
| `from_`                                                              | [date](https://docs.python.org/3/library/datetime.html#date-objects) | :heavy_check_mark:                                                   | Start of query window (ISO 8601)                                     |
| `to`                                                                 | [date](https://docs.python.org/3/library/datetime.html#date-objects) | :heavy_check_mark:                                                   | End of query window (ISO 8601)                                       |
| `subject`                                                            | *Optional[str]*                                                      | :heavy_minus_sign:                                                   | Filter by customer/user ID                                           |
| `window_size`                                                        | [Optional[models.WindowSize]](../../models/windowsize.md)            | :heavy_minus_sign:                                                   | Time bucket granularity                                              |
| `filter_group_by`                                                    | *Optional[str]*                                                      | :heavy_minus_sign:                                                   | JSON-encoded dimension filter (e.g. {"key":"value"})                 |
| `group_by`                                                           | *Optional[str]*                                                      | :heavy_minus_sign:                                                   | Comma-separated dimension keys                                       |
| `retries`                                                            | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)     | :heavy_minus_sign:                                                   | Configuration to override the default retry behavior of the client.  |

### Response

**[models.UsageResponse](../../models/usageresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403                          | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |