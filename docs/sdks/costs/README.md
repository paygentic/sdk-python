# Costs

## Overview

A Cost represents the operational or infrastructure expense of serving customers for a given product. Costs are metered (driven by event-based usage) and are tracked in parallel with billable metrics to give merchants visibility into both revenue and cost per customer.

### Available Operations

* [create_cost](#create_cost) - Create
* [list_costs](#list_costs) - List
* [get_cost](#get_cost) - Get
* [update_cost](#update_cost) - Update
* [delete_cost](#delete_cost) - Delete
* [get_cost_summary](#get_cost_summary) - Query Summary

## create_cost

Create a new metered cost for a product.

### Example Usage

<!-- UsageSnippet language="python" operationID="createCost" method="post" path="/v0/costs" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.costs.create_cost(type_="metered", name="<value>", unit_cost=6810, currency="Swedish Krona", product_id="<id>", aggregation="MIN", event_type="<value>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                            | Type                                                                                                 | Required                                                                                             | Description                                                                                          |
| ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| `type`                                                                                               | [models.CreateCostType](../../models/createcosttype.md)                                              | :heavy_check_mark:                                                                                   | The cost type. Only `metered` costs are supported; they track usage via events.                      |
| `name`                                                                                               | *str*                                                                                                | :heavy_check_mark:                                                                                   | Human-readable name for the cost.                                                                    |
| `unit_cost`                                                                                          | *float*                                                                                              | :heavy_check_mark:                                                                                   | Cost per unit, multiplied by measured quantity to compute total cost. Must be non-negative.          |
| `currency`                                                                                           | *str*                                                                                                | :heavy_check_mark:                                                                                   | ISO 4217 currency code (e.g. USD, EUR).                                                              |
| `product_id`                                                                                         | *str*                                                                                                | :heavy_check_mark:                                                                                   | Unique identifier for a product                                                                      |
| `aggregation`                                                                                        | [models.CreateCostAggregation](../../models/createcostaggregation.md)                                | :heavy_check_mark:                                                                                   | Aggregation method for the metered event.                                                            |
| `event_type`                                                                                         | *str*                                                                                                | :heavy_check_mark:                                                                                   | CloudEvents type that identifies the metered event.                                                  |
| `unit`                                                                                               | *Optional[str]*                                                                                      | :heavy_minus_sign:                                                                                   | Unit label for metered costs (e.g. 'token', 'request'). Only valid for metered costs.                |
| `value_property`                                                                                     | *Optional[str]*                                                                                      | :heavy_minus_sign:                                                                                   | JSONPath to extract numeric value from event data. Required for SUM/AVG/MIN/MAX/LATEST aggregations. |
| `group_by`                                                                                           | Dict[str, *str*]                                                                                     | :heavy_minus_sign:                                                                                   | Map of dimension name to JSONPath for group-by queries. Only valid for metered costs.                |
| `merchant_id`                                                                                        | *Optional[str]*                                                                                      | :heavy_minus_sign:                                                                                   | Unique identifier for an organization                                                                |
| `retries`                                                                                            | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                     | :heavy_minus_sign:                                                                                   | Configuration to override the default retry behavior of the client.                                  |

### Response

**[models.Cost](../../models/cost.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## list_costs

List

### Example Usage

<!-- UsageSnippet language="python" operationID="listCosts" method="get" path="/v0/costs" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.costs.list_costs(request={})

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `request`                                                           | [models.ListCostsRequest](../../models/listcostsrequest.md)         | :heavy_check_mark:                                                  | The request object to use for the request.                          |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.ListCostsResponse](../../models/listcostsresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get_cost

Get

### Example Usage

<!-- UsageSnippet language="python" operationID="getCost" method="get" path="/v0/costs/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.costs.get_cost(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the cost                                   |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.Cost](../../models/cost.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## update_cost

Update

### Example Usage

<!-- UsageSnippet language="python" operationID="updateCost" method="patch" path="/v0/costs/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.costs.update_cost(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                               | Type                                                                                    | Required                                                                                | Description                                                                             |
| --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `id`                                                                                    | *str*                                                                                   | :heavy_check_mark:                                                                      | The unique identifier of the cost                                                       |
| `name`                                                                                  | *Optional[str]*                                                                         | :heavy_minus_sign:                                                                      | Updated name for the cost.                                                              |
| `unit_cost`                                                                             | *Optional[float]*                                                                       | :heavy_minus_sign:                                                                      | Updated unit cost.                                                                      |
| `currency`                                                                              | *Optional[str]*                                                                         | :heavy_minus_sign:                                                                      | Updated ISO 4217 currency code.                                                         |
| `unit`                                                                                  | *OptionalNullable[str]*                                                                 | :heavy_minus_sign:                                                                      | Updated unit label (metered costs only).                                                |
| `aggregation`                                                                           | [OptionalNullable[models.UpdateCostAggregation]](../../models/updatecostaggregation.md) | :heavy_minus_sign:                                                                      | Updated aggregation method (metered costs only).                                        |
| `event_type`                                                                            | *OptionalNullable[str]*                                                                 | :heavy_minus_sign:                                                                      | Updated CloudEvents type (metered costs only).                                          |
| `value_property`                                                                        | *OptionalNullable[str]*                                                                 | :heavy_minus_sign:                                                                      | Updated JSONPath for value extraction (metered costs only).                             |
| `group_by`                                                                              | Dict[str, *str*]                                                                        | :heavy_minus_sign:                                                                      | Updated group-by dimension map (metered costs only).                                    |
| `retries`                                                                               | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                        | :heavy_minus_sign:                                                                      | Configuration to override the default retry behavior of the client.                     |

### Response

**[models.Cost](../../models/cost.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## delete_cost

Delete

### Example Usage

<!-- UsageSnippet language="python" operationID="deleteCost" method="delete" path="/v0/costs/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    paygentic.costs.delete_cost(id="<id>")

    # Use the SDK ...

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the cost                                   |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get_cost_summary

Query usage data and compute cost for a specific cost configuration. To retrieve summaries for all costs belonging to a merchant, first call listCosts to obtain cost IDs, then call this endpoint in parallel for each ID.

### Example Usage

<!-- UsageSnippet language="python" operationID="getCostSummary" method="get" path="/v0/costs/{id}/summary" -->
```python
import os
from paygentic_sdk import Paygentic
from paygentic_sdk.utils import parse_datetime


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.costs.get_cost_summary(id="<id>", from_=parse_datetime("2024-06-26T21:12:15.723Z"), to=parse_datetime("2026-01-05T23:33:29.000Z"))

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                        | Type                                                                                                                                                                                             | Required                                                                                                                                                                                         | Description                                                                                                                                                                                      |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `id`                                                                                                                                                                                             | *str*                                                                                                                                                                                            | :heavy_check_mark:                                                                                                                                                                               | The unique identifier of the cost                                                                                                                                                                |
| `from_`                                                                                                                                                                                          | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                             | :heavy_check_mark:                                                                                                                                                                               | Start of the query window (ISO 8601). Required together with 'to'.                                                                                                                               |
| `to`                                                                                                                                                                                             | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                             | :heavy_check_mark:                                                                                                                                                                               | End of the query window (ISO 8601). Required together with 'from'.                                                                                                                               |
| `subject`                                                                                                                                                                                        | *Optional[str]*                                                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                               | Filter usage to a specific subject (billing entity). When provided, only cost events matching this subject are included. When omitted, usage is aggregated across all subjects for the merchant. |
| `group_by`                                                                                                                                                                                       | *Optional[str]*                                                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                               | Comma-separated dimension keys to group results by.                                                                                                                                              |
| `window`                                                                                                                                                                                         | [Optional[models.Window]](../../models/window.md)                                                                                                                                                | :heavy_minus_sign:                                                                                                                                                                               | Time window granularity for time-series breakdown.                                                                                                                                               |
| `filter_group_by`                                                                                                                                                                                | *Optional[str]*                                                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                               | JSON-encoded dimension filter (e.g. {"model":"gpt-4","region":"us-east"}). Keys must match those defined in the cost's groupBy configuration. Retrieve the cost first to determine valid keys.   |
| `retries`                                                                                                                                                                                        | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                                               | Configuration to override the default retry behavior of the client.                                                                                                                              |

### Response

**[models.CostUsageResponse](../../models/costusageresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |