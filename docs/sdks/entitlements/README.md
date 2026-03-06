# Entitlements

## Overview

An `Entitlement` grants a customer the right to access and use a specific product feature.

### Available Operations

* [list](#list) - List Entitlements
* [issue](#issue) - Issue Entitlement
* [get](#get) - Get Entitlement

## list

Retrieve all entitlements for a customer, optionally filtered by feature or product.

### Example Usage: emptyResult

<!-- UsageSnippet language="python" operationID="listEntitlements" method="get" path="/v1/entitlements" example="emptyResult" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.entitlements.list(customer_id="cus_q3r4s5t6u7v8w9x0", limit=10, offset=0)

    # Handle response
    print(res)

```
### Example Usage: expiredEntitlement

<!-- UsageSnippet language="python" operationID="listEntitlements" method="get" path="/v1/entitlements" example="expiredEntitlement" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.entitlements.list(customer_id="cus_q3r4s5t6u7v8w9x0", limit=10, offset=0)

    # Handle response
    print(res)

```
### Example Usage: multipleEntitlements

<!-- UsageSnippet language="python" operationID="listEntitlements" method="get" path="/v1/entitlements" example="multipleEntitlements" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.entitlements.list(customer_id="cus_q3r4s5t6u7v8w9x0", limit=10, offset=0)

    # Handle response
    print(res)

```
### Example Usage: staticFeatureWithConfig

<!-- UsageSnippet language="python" operationID="listEntitlements" method="get" path="/v1/entitlements" example="staticFeatureWithConfig" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.entitlements.list(customer_id="cus_q3r4s5t6u7v8w9x0", limit=10, offset=0)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                    | Type                                                                                                                                         | Required                                                                                                                                     | Description                                                                                                                                  | Example                                                                                                                                      |
| -------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| `customer_id`                                                                                                                                | *str*                                                                                                                                        | :heavy_check_mark:                                                                                                                           | The unique identifier of the customer to retrieve entitlements for.                                                                          | cus_q3r4s5t6u7v8w9x0                                                                                                                         |
| `feature_key`                                                                                                                                | *Optional[str]*                                                                                                                              | :heavy_minus_sign:                                                                                                                           | Filter results to a specific feature by its key. When specified, `productId` is also required. Use this to check access to a single feature. |                                                                                                                                              |
| `product_id`                                                                                                                                 | *Optional[str]*                                                                                                                              | :heavy_minus_sign:                                                                                                                           | Filter results to entitlements for a specific product. Required when `featureKey` is specified since feature keys are scoped to products.    |                                                                                                                                              |
| `subscription_id`                                                                                                                            | *Optional[str]*                                                                                                                              | :heavy_minus_sign:                                                                                                                           | Filter results to entitlements for a specific subscription.                                                                                  |                                                                                                                                              |
| `limit`                                                                                                                                      | *Optional[int]*                                                                                                                              | :heavy_minus_sign:                                                                                                                           | Maximum number of entitlements to return per page. Use with `offset` for pagination.                                                         |                                                                                                                                              |
| `offset`                                                                                                                                     | *Optional[int]*                                                                                                                              | :heavy_minus_sign:                                                                                                                           | Number of entitlements to skip. Use with `limit` for pagination through large result sets.                                                   |                                                                                                                                              |
| `retries`                                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                             | :heavy_minus_sign:                                                                                                                           | Configuration to override the default retry behavior of the client.                                                                          |                                                                                                                                              |

### Response

**[models.ListEntitlementsResponse](../../models/listentitlementsresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403                          | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## issue

Issue a new entitlement to a customer, granting them access to a specific feature. The feature must exist and belong to the same merchant as the customer.

### Example Usage: booleanEntitlement

<!-- UsageSnippet language="python" operationID="issueEntitlement" method="post" path="/v1/entitlements" example="booleanEntitlement" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.entitlements.issue(customer_id="cus_q3r4s5t6u7v8w9x0", feature_id="feat_a1b2c3d4e5f6g7h8", template={
        "type": "boolean",
    })

    # Handle response
    print(res)

```
### Example Usage: staticEntitlement

<!-- UsageSnippet language="python" operationID="issueEntitlement" method="post" path="/v1/entitlements" example="staticEntitlement" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.entitlements.issue(customer_id="cus_q3r4s5t6u7v8w9x0", feature_id="feat_a1b2c3d4e5f6g7h8", template={
        "type": "static",
        "config": {
            "limit": 25,
            "tier": "pro",
        },
    })

    # Handle response
    print(res)

```
### Example Usage: timedEntitlement

<!-- UsageSnippet language="python" operationID="issueEntitlement" method="post" path="/v1/entitlements" example="timedEntitlement" -->
```python
import os
from paygentic_sdk import Paygentic
from paygentic_sdk.utils import parse_datetime


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.entitlements.issue(customer_id="cus_q3r4s5t6u7v8w9x0", feature_id="feat_a1b2c3d4e5f6g7h8", template={
        "type": "boolean",
    }, active_from=parse_datetime("2024-01-01T00:00:00Z"), active_to=parse_datetime("2025-01-01T00:00:00Z"))

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                   | Type                                                                                                                                        | Required                                                                                                                                    | Description                                                                                                                                 |
| ------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| `customer_id`                                                                                                                               | *str*                                                                                                                                       | :heavy_check_mark:                                                                                                                          | Unique identifier for a customer                                                                                                            |
| `feature_id`                                                                                                                                | *str*                                                                                                                                       | :heavy_check_mark:                                                                                                                          | The feature to grant access to.                                                                                                             |
| `template`                                                                                                                                  | [models.EntitlementTemplate](../../models/entitlementtemplate.md)                                                                           | :heavy_check_mark:                                                                                                                          | Template for the entitlement. Boolean for simple on/off features, static for features with configuration, metered for usage-based features. |
| `active_from`                                                                                                                               | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                        | :heavy_minus_sign:                                                                                                                          | When the entitlement becomes active. Defaults to now.                                                                                       |
| `active_to`                                                                                                                                 | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                        | :heavy_minus_sign:                                                                                                                          | When the entitlement expires. Null means no expiration.                                                                                     |
| `subscription_id`                                                                                                                           | *OptionalNullable[str]*                                                                                                                     | :heavy_minus_sign:                                                                                                                          | Optional subscription ID to associate with this entitlement.                                                                                |
| `metadata`                                                                                                                                  | Dict[str, *str*]                                                                                                                            | :heavy_minus_sign:                                                                                                                          | Additional metadata for the entitlement.                                                                                                    |
| `retries`                                                                                                                                   | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                            | :heavy_minus_sign:                                                                                                                          | Configuration to override the default retry behavior of the client.                                                                         |

### Response

**[models.SchemasEntitlement](../../models/schemasentitlement.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404, 409                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get

Retrieve a specific entitlement by ID. For metered entitlements, the response includes live balance, usage, and access status for the current billing period.

### Example Usage: booleanEntitlement

<!-- UsageSnippet language="python" operationID="getEntitlement" method="get" path="/v1/entitlements/{entitlementId}" example="booleanEntitlement" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.entitlements.get(entitlement_id="<id>")

    # Handle response
    print(res)

```
### Example Usage: meteredEntitlement

<!-- UsageSnippet language="python" operationID="getEntitlement" method="get" path="/v1/entitlements/{entitlementId}" example="meteredEntitlement" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.entitlements.get(entitlement_id="<id>")

    # Handle response
    print(res)

```
### Example Usage: staticEntitlement

<!-- UsageSnippet language="python" operationID="getEntitlement" method="get" path="/v1/entitlements/{entitlementId}" example="staticEntitlement" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.entitlements.get(entitlement_id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `entitlement_id`                                                    | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the entitlement.                           |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.EntitlementDetail](../../models/entitlementdetail.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |