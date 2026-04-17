# EntitlementsV0

## Overview

### Available Operations

* [list_active](#list_active) - List by Customer
* [create](#create) - Create

## list_active

List by Customer

### Example Usage

<!-- UsageSnippet language="python" operationID="getActiveEntitlements" method="get" path="/v0/entitlements/activeEntitlements" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.entitlements_v0.list_active(customer_id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `customer_id`                                                       | *str*                                                               | :heavy_check_mark:                                                  | The customer ID to get active entitlements for.                     |
| `product_id`                                                        | *Optional[str]*                                                     | :heavy_minus_sign:                                                  | The product ID to get active entitlements for.                      |
| `subscription_id`                                                   | *Optional[str]*                                                     | :heavy_minus_sign:                                                  | The subscription ID to get active entitlements for.                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.GetActiveEntitlementsResponse](../../models/getactiveentitlementsresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403                          | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## create

Create an entitlement for a customer. This temporarily reserves funds in the customer's wallet to guarantee payment for future usage.

### Example Usage

<!-- UsageSnippet language="python" operationID="createEntitlement" method="post" path="/v0/entitlements" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.entitlements_v0.create(customer_id="<id>", entitlement_data=[], merchant_id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                              | Type                                                                                                                                   | Required                                                                                                                               | Description                                                                                                                            |
| -------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `customer_id`                                                                                                                          | *str*                                                                                                                                  | :heavy_check_mark:                                                                                                                     | Unique identifier for a customer                                                                                                       |
| `entitlement_data`                                                                                                                     | List[[models.EntitlementDatum](../../models/entitlementdatum.md)]                                                                      | :heavy_check_mark:                                                                                                                     | Array of consumption metrics with quantities to pre-authorize payment for.                                                             |
| `merchant_id`                                                                                                                          | *str*                                                                                                                                  | :heavy_check_mark:                                                                                                                     | Unique identifier for a merchant/organization                                                                                          |
| `max_uses`                                                                                                                             | *Optional[int]*                                                                                                                        | :heavy_minus_sign:                                                                                                                     | Maximum consumption events allowed before expiration (optional). Defaults to 1 for global entitlements, 100 for regional entitlements. |
| `retries`                                                                                                                              | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                       | :heavy_minus_sign:                                                                                                                     | Configuration to override the default retry behavior of the client.                                                                    |

### Response

**[models.Entitlement](../../models/entitlement.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403                          | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |