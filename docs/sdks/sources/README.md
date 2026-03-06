# Sources

## Overview

A `Source` is an external data provider capable of automatically creating usage events. Configuration occurs at the plan level, enabling data retrieval from third-party platforms such as Stripe to produce billable events.

### Available Operations

* [create](#create) - Create
* [list](#list) - List
* [get](#get) - Get
* [update](#update) - Update

## create

Create a new source for automated usage event generation from external data sources.

### Example Usage

<!-- UsageSnippet language="python" operationID="createSource" method="post" path="/v0/sources" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.sources.create(name="<value>", plan_id="<id>", type_="stripe_revenue", enabled=True, processing_mode="automatic")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                       | Type                                                                                                                                                                                                                                            | Required                                                                                                                                                                                                                                        | Description                                                                                                                                                                                                                                     |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `name`                                                                                                                                                                                                                                          | *str*                                                                                                                                                                                                                                           | :heavy_check_mark:                                                                                                                                                                                                                              | Display label for the external data source. Sample values: 'Stripe Revenue Integration', 'LLM Usage Tracker', 'Data Processing Monitor', 'ML Compute Usage Source'                                                                              |
| `plan_id`                                                                                                                                                                                                                                       | *str*                                                                                                                                                                                                                                           | :heavy_check_mark:                                                                                                                                                                                                                              | Unique identifier for a plan                                                                                                                                                                                                                    |
| `type`                                                                                                                                                                                                                                          | [models.CreateSourceType](../../models/createsourcetype.md)                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                                              | The type of source. Currently only 'stripe_revenue' is supported.                                                                                                                                                                               |
| `config`                                                                                                                                                                                                                                        | Dict[str, *Any*]                                                                                                                                                                                                                                | :heavy_minus_sign:                                                                                                                                                                                                                              | Configuration specific to the source type. For stripe_revenue, must include ampersandProjectId.                                                                                                                                                 |
| `description`                                                                                                                                                                                                                                   | *Optional[str]*                                                                                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                                                                                              | Optional explanation of the source's purpose. Sample values: 'Automated usage tracking from Stripe revenue data', 'Language model token consumption monitoring', 'Data warehouse query tracking', 'Machine learning inference usage collection' |
| `enabled`                                                                                                                                                                                                                                       | *Optional[bool]*                                                                                                                                                                                                                                | :heavy_minus_sign:                                                                                                                                                                                                                              | Whether the source is enabled                                                                                                                                                                                                                   |
| `metadata`                                                                                                                                                                                                                                      | Dict[str, *Any*]                                                                                                                                                                                                                                | :heavy_minus_sign:                                                                                                                                                                                                                              | Metadata for the source. For stripe_revenue, must include billableMetricMapping with revenue (billable metric ID).                                                                                                                              |
| `processing_mode`                                                                                                                                                                                                                               | [Optional[models.CreateSourceProcessingMode]](../../models/createsourceprocessingmode.md)                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                                              | How events are processed - automatic (immediate) or manual (requires approval)                                                                                                                                                                  |
| `retries`                                                                                                                                                                                                                                       | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                | :heavy_minus_sign:                                                                                                                                                                                                                              | Configuration to override the default retry behavior of the client.                                                                                                                                                                             |

### Response

**[models.Source](../../models/source.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## list

List

### Example Usage

<!-- UsageSnippet language="python" operationID="listSources" method="get" path="/v0/sources" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.sources.list(request={})

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `request`                                                           | [models.ListSourcesRequest](../../models/listsourcesrequest.md)     | :heavy_check_mark:                                                  | The request object to use for the request.                          |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.ListSourcesResponse](../../models/listsourcesresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 403                          | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get

Get

### Example Usage

<!-- UsageSnippet language="python" operationID="getSource" method="get" path="/v0/sources/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.sources.get(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the source                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.Source](../../models/source.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## update

Update

### Example Usage

<!-- UsageSnippet language="python" operationID="updateSource" method="patch" path="/v0/sources/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.sources.update(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                 | Type                                                                                      | Required                                                                                  | Description                                                                               |
| ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| `id`                                                                                      | *str*                                                                                     | :heavy_check_mark:                                                                        | The unique identifier of the source                                                       |
| `config`                                                                                  | Dict[str, *Any*]                                                                          | :heavy_minus_sign:                                                                        | Configuration specific to the source type                                                 |
| `description`                                                                             | *Optional[str]*                                                                           | :heavy_minus_sign:                                                                        | Description of the source                                                                 |
| `enabled`                                                                                 | *Optional[bool]*                                                                          | :heavy_minus_sign:                                                                        | Whether the source is enabled                                                             |
| `metadata`                                                                                | Dict[str, *Any*]                                                                          | :heavy_minus_sign:                                                                        | Metadata for the source                                                                   |
| `name`                                                                                    | *Optional[str]*                                                                           | :heavy_minus_sign:                                                                        | Display name for the source                                                               |
| `processing_mode`                                                                         | [Optional[models.UpdateSourceProcessingMode]](../../models/updatesourceprocessingmode.md) | :heavy_minus_sign:                                                                        | How events are processed - automatic (immediate) or manual (requires approval)            |
| `retries`                                                                                 | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                          | :heavy_minus_sign:                                                                        | Configuration to override the default retry behavior of the client.                       |

### Response

**[models.Source](../../models/source.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |