# Fees

## Overview

A `Fee` defines a recurring or one-time charge tied to a `Product`. Fees are linked to prices, and cadence is defined on the Price.

### Available Operations

* [create](#create) - Create
* [list](#list) - List
* [get](#get) - Get
* [update](#update) - Update
* [delete](#delete) - Delete
* [get_price](#get_price) - Get Fee Price

## create

Create a new fee for a merchant organization. A `Fee` represents a charge that can be applied to subscriptions. Cadence is defined when creating a Price for the fee.

### Example Usage

<!-- UsageSnippet language="python" operationID="createFee" method="post" path="/v0/fees" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.fees.create(name="<value>", description="obnoxiously boldly that fort as minus bob adventurously", merchant_id="<id>", product_id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                   | Type                                                                                                                                                                                        | Required                                                                                                                                                                                    | Description                                                                                                                                                                                 |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `name`                                                                                                                                                                                      | *str*                                                                                                                                                                                       | :heavy_check_mark:                                                                                                                                                                          | Human-readable label identifying the fee. Sample values: 'Setup Fee', 'Monthly Subscription', 'Compliance Update', 'Annual License'                                                         |
| `description`                                                                                                                                                                               | *str*                                                                                                                                                                                       | :heavy_check_mark:                                                                                                                                                                          | Explanatory text describing what the fee represents. Sample values: 'One-time setup fee for new customers', 'Monthly base subscription charge', 'Yearly compliance and security update fee' |
| `merchant_id`                                                                                                                                                                               | *str*                                                                                                                                                                                       | :heavy_check_mark:                                                                                                                                                                          | Unique identifier for an organization                                                                                                                                                       |
| `product_id`                                                                                                                                                                                | *str*                                                                                                                                                                                       | :heavy_check_mark:                                                                                                                                                                          | Unique identifier for a product                                                                                                                                                             |
| `retries`                                                                                                                                                                                   | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                          | Configuration to override the default retry behavior of the client.                                                                                                                         |

### Response

**[models.Fee](../../models/fee.md)**

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

<!-- UsageSnippet language="python" operationID="listFees" method="get" path="/v0/fees" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.fees.list(merchant_id="<id>", limit=10, offset=0)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `merchant_id`                                                       | *str*                                                               | :heavy_check_mark:                                                  | Filter fees by merchant organization ID.                            |
| `limit`                                                             | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | Number of fees to return.                                           |
| `offset`                                                            | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | Number of fees to skip.                                             |
| `product_id`                                                        | *Optional[str]*                                                     | :heavy_minus_sign:                                                  | Filter fees by product ID.                                          |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.ListFeesResponse](../../models/listfeesresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get

Get

### Example Usage

<!-- UsageSnippet language="python" operationID="getFee" method="get" path="/v0/fees/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.fees.get(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the fee                                    |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.Fee](../../models/fee.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## update

Update

### Example Usage

<!-- UsageSnippet language="python" operationID="updateFee" method="patch" path="/v0/fees/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.fees.update(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the fee                                    |
| `description`                                                       | *Optional[str]*                                                     | :heavy_minus_sign:                                                  | Revised explanation of what the fee represents.                     |
| `name`                                                              | *Optional[str]*                                                     | :heavy_minus_sign:                                                  | Updated label for the fee.                                          |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.Fee](../../models/fee.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## delete

Delete

### Example Usage

<!-- UsageSnippet language="python" operationID="deleteFee" method="delete" path="/v0/fees/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    paygentic.fees.delete(id="<id>")

    # Use the SDK ...

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the fee                                    |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Errors

| Error Type                    | Status Code                   | Content Type                  |
| ----------------------------- | ----------------------------- | ----------------------------- |
| errors.Error                  | 403, 404                      | application/json              |
| errors.DeleteFeeConflictError | 409                           | application/json              |
| errors.Error                  | 500                           | application/json              |
| errors.PaygenticDefaultError  | 4XX, 5XX                      | \*/\*                         |

## get_price

Get the price for a fee in the context of a subscription. This returns the price configured for the fee in the subscription's plan, including the tax rate.

### Example Usage

<!-- UsageSnippet language="python" operationID="getFeePrice" method="get" path="/v0/fees/{id}/price/{subscriptionId}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.fees.get_price(id="<id>", subscription_id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the fee.                                   |
| `subscription_id`                                                   | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the subscription.                          |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.FeePrice](../../models/feeprice.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |