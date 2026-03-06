# Features

## Overview

A `Feature` represents a specific capability or functionality provided by a `Product`. Features can be metered (usage-based), static (fixed allocation), or boolean (enabled/disabled).

### Available Operations

* [list](#list) - List
* [create](#create) - Create
* [get](#get) - Get
* [update](#update) - Update
* [delete](#delete) - Delete

## list

List features by productId, optionally filtered by key

### Example Usage

<!-- UsageSnippet language="python" operationID="listFeatures" method="get" path="/v0/features" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.features.list(product_id="<id>", limit=10, offset=0)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                | Type                                                                                                     | Required                                                                                                 | Description                                                                                              |
| -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| `product_id`                                                                                             | *str*                                                                                                    | :heavy_check_mark:                                                                                       | The product ID to filter features by                                                                     |
| `key`                                                                                                    | *Optional[str]*                                                                                          | :heavy_minus_sign:                                                                                       | Optional feature key to filter by. If provided, returns only the feature matching both productId and key |
| `limit`                                                                                                  | *Optional[int]*                                                                                          | :heavy_minus_sign:                                                                                       | Number of features to return.                                                                            |
| `offset`                                                                                                 | *Optional[int]*                                                                                          | :heavy_minus_sign:                                                                                       | Number of features to skip.                                                                              |
| `retries`                                                                                                | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                         | :heavy_minus_sign:                                                                                       | Configuration to override the default retry behavior of the client.                                      |

### Response

**[models.ListFeaturesResponse](../../models/listfeaturesresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## create

Create

### Example Usage

<!-- UsageSnippet language="python" operationID="createFeature" method="post" path="/v0/features" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.features.create(key="<key>", name="<value>", merchant_id="<id>", product_id="<id>", type_="boolean")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                        | Type                                                                                                             | Required                                                                                                         | Description                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| `key`                                                                                                            | *str*                                                                                                            | :heavy_check_mark:                                                                                               | Unique slug identifier for the feature within the product. Must be lowercase letters, numbers, and hyphens only. |
| `name`                                                                                                           | *str*                                                                                                            | :heavy_check_mark:                                                                                               | Human-readable feature name shown to customers.                                                                  |
| `merchant_id`                                                                                                    | *str*                                                                                                            | :heavy_check_mark:                                                                                               | Unique identifier for an organization                                                                            |
| `product_id`                                                                                                     | *str*                                                                                                            | :heavy_check_mark:                                                                                               | Unique identifier for a product                                                                                  |
| `type`                                                                                                           | [Optional[models.CreateFeatureType]](../../models/createfeaturetype.md)                                          | :heavy_minus_sign:                                                                                               | Feature type: 'metered' for usage-based features, 'static' for fixed allocations, 'boolean' for on/off features  |
| `metadata`                                                                                                       | Dict[str, *str*]                                                                                                 | :heavy_minus_sign:                                                                                               | Optional key-value metadata storage for feature information.                                                     |
| `retries`                                                                                                        | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                 | :heavy_minus_sign:                                                                                               | Configuration to override the default retry behavior of the client.                                              |

### Response

**[models.Feature](../../models/feature.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404, 409           | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get

Get

### Example Usage

<!-- UsageSnippet language="python" operationID="getFeature" method="get" path="/v0/features/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.features.get(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the feature                                |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.Feature](../../models/feature.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## update

Update

### Example Usage

<!-- UsageSnippet language="python" operationID="updateFeature" method="patch" path="/v0/features/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.features.update(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                          | Type                                                                               | Required                                                                           | Description                                                                        |
| ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| `id`                                                                               | *str*                                                                              | :heavy_check_mark:                                                                 | The unique identifier of the feature                                               |
| `key`                                                                              | *Optional[str]*                                                                    | :heavy_minus_sign:                                                                 | Updated feature key slug. Sample values: 'increased-api-limit', 'new-storage-tier' |
| `name`                                                                             | *Optional[str]*                                                                    | :heavy_minus_sign:                                                                 | Updated feature name.                                                              |
| `type`                                                                             | [Optional[models.UpdateFeatureType]](../../models/updatefeaturetype.md)            | :heavy_minus_sign:                                                                 | Updated feature type                                                               |
| `metadata`                                                                         | Dict[str, *str*]                                                                   | :heavy_minus_sign:                                                                 | Updated metadata for the feature                                                   |
| `retries`                                                                          | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                   | :heavy_minus_sign:                                                                 | Configuration to override the default retry behavior of the client.                |

### Response

**[models.Feature](../../models/feature.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## delete

Delete

### Example Usage

<!-- UsageSnippet language="python" operationID="deleteFeature" method="delete" path="/v0/features/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    paygentic.features.delete(id="<id>")

    # Use the SDK ...

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the feature                                |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |