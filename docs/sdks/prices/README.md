# Prices

## Overview

A `Price` determines the monetary value for a single unit of a `Billable Metric`. Prices are exclusively grouped within a `Plan`.

### Available Operations

* [create](#create) - Create
* [list](#list) - List
* [get](#get) - Get
* [update](#update) - Update
* [delete](#delete) - Delete

## create

Create

### Example Usage

<!-- UsageSnippet language="python" operationID="createPrice" method="post" path="/v0/prices" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.prices.create(invoice_display_name="<value>", payment_term="in_arrears", properties={
        "default": "<value>",
        "parameters": {
            "function": "linear",
            "gradient": "<value>",
            "max": "<value>",
            "min": "<value>",
        },
    }, grant_discount_enabled=False)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                                                                          | Type                                                                                                                                                                                                                                                                                                               | Required                                                                                                                                                                                                                                                                                                           | Description                                                                                                                                                                                                                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `invoice_display_name`                                                                                                                                                                                                                                                                                             | *str*                                                                                                                                                                                                                                                                                                              | :heavy_check_mark:                                                                                                                                                                                                                                                                                                 | Line item label shown on customer invoices. Sample values: 'Claude Token Consumption', 'Storage Usage (GB)', 'Inference API Calls', 'Image Generation Count', 'Training Compute Hours', 'Data Transfer (TB)'                                                                                                       |
| `payment_term`                                                                                                                                                                                                                                                                                                     | [models.CreatePricePaymentTerm](../../models/createpricepaymentterm.md)                                                                                                                                                                                                                                            | :heavy_check_mark:                                                                                                                                                                                                                                                                                                 | Billing timing preference: 'in_advance' (prepaid — charged upfront or drawn from a prepaid commitment) or 'in_arrears' (charged at period end).                                                                                                                                                                    |
| `properties`                                                                                                                                                                                                                                                                                                       | [models.PricePropertiesUnion](../../models/pricepropertiesunion.md)                                                                                                                                                                                                                                                | :heavy_check_mark:                                                                                                                                                                                                                                                                                                 | N/A                                                                                                                                                                                                                                                                                                                |
| `billable_metric_id`                                                                                                                                                                                                                                                                                               | *Optional[str]*                                                                                                                                                                                                                                                                                                    | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                 | Unique identifier for a billable metric                                                                                                                                                                                                                                                                            |
| `fee_id`                                                                                                                                                                                                                                                                                                           | *Optional[str]*                                                                                                                                                                                                                                                                                                    | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                 | The unique identifier for the fee referred to by this price. Either billableMetricId or feeId must be provided.                                                                                                                                                                                                    |
| `pricing_unit_id`                                                                                                                                                                                                                                                                                                  | *Optional[str]*                                                                                                                                                                                                                                                                                                    | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                 | Unique identifier for a pricing unit                                                                                                                                                                                                                                                                               |
| `model`                                                                                                                                                                                                                                                                                                            | [Optional[models.PriceModelInput]](../../models/pricemodelinput.md)                                                                                                                                                                                                                                                | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                 | Pricing calculation model. Required for billable metrics, optional for fees (defaults to 'standard'). Only 'standard' is accepted; for percentage/revenue-share use 'standard' with a unit-price multiplier. Legacy prices using 'dynamic'/'volume'/'percentage' stay readable and billable but cannot be created. |
| `billing_cadence`                                                                                                                                                                                                                                                                                                  | *OptionalNullable[str]*                                                                                                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                 | ISO 8601 duration for recurring charges (e.g., 'P1M' for monthly, 'P1Y' for yearly) or 'P0D' for one-time charges. Required for fees, optional for billable metrics. Sample values: 'P0D' for one-time, 'P1M' for monthly recurring, 'P1Y' for yearly recurring                                                    |
| `feature`                                                                                                                                                                                                                                                                                                          | [Optional[models.PriceFeatureInput]](../../models/pricefeatureinput.md)                                                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                 | N/A                                                                                                                                                                                                                                                                                                                |
| `grant_discount_enabled`                                                                                                                                                                                                                                                                                           | *Optional[bool]*                                                                                                                                                                                                                                                                                                   | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                 | When true, grants applied to a subscription will discount usage charged by this price. Only supported for standard metered prices.                                                                                                                                                                                 |
| `quantity`                                                                                                                                                                                                                                                                                                         | *Optional[int]*                                                                                                                                                                                                                                                                                                    | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                 | Quantity for invoice line items. Total per period = quantity × unitPrice. Only supported for fee prices; metered prices derive quantity from usage. Defaults to 1.                                                                                                                                                 |
| `retries`                                                                                                                                                                                                                                                                                                          | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                                                                   | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                 | Configuration to override the default retry behavior of the client.                                                                                                                                                                                                                                                |

### Response

**[models.SchemasPrice](../../models/schemasprice.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## list

List

### Example Usage

<!-- UsageSnippet language="python" operationID="listPrices" method="get" path="/v0/prices" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.prices.list(request={})

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `request`                                                           | [models.ListPricesRequest](../../models/listpricesrequest.md)       | :heavy_check_mark:                                                  | The request object to use for the request.                          |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.ListPricesResponse](../../models/listpricesresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get

Get

### Example Usage

<!-- UsageSnippet language="python" operationID="getPrice" method="get" path="/v0/prices/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.prices.get(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the price                                  |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.SchemasPrice](../../models/schemasprice.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## update

Update

### Example Usage

<!-- UsageSnippet language="python" operationID="updatePrice" method="patch" path="/v0/prices/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.prices.update(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                          | Type                                                                                                                                                                                                                                                               | Required                                                                                                                                                                                                                                                           | Description                                                                                                                                                                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `id`                                                                                                                                                                                                                                                               | *str*                                                                                                                                                                                                                                                              | :heavy_check_mark:                                                                                                                                                                                                                                                 | The unique identifier of the price                                                                                                                                                                                                                                 |
| `billable_metric_id`                                                                                                                                                                                                                                               | *Optional[str]*                                                                                                                                                                                                                                                    | :heavy_minus_sign:                                                                                                                                                                                                                                                 | Unique identifier for a billable metric                                                                                                                                                                                                                            |
| `pricing_unit_id`                                                                                                                                                                                                                                                  | *OptionalNullable[str]*                                                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                                                                 | Denominate this metered price in a pricing unit (credits). Set to a pricing unit ID to draw down a credit pool, null to revert to real currency, or omit to leave unchanged.                                                                                       |
| `invoice_display_name`                                                                                                                                                                                                                                             | *Optional[str]*                                                                                                                                                                                                                                                    | :heavy_minus_sign:                                                                                                                                                                                                                                                 | Updated invoice line item label. Sample values: 'LLM Token Usage', 'Storage Charges', 'API Call Fees'                                                                                                                                                              |
| `model`                                                                                                                                                                                                                                                            | [Optional[models.PriceModelInput]](../../models/pricemodelinput.md)                                                                                                                                                                                                | :heavy_minus_sign:                                                                                                                                                                                                                                                 | The pricing model to set. Only 'standard' is accepted. Legacy 'dynamic'/'volume'/'percentage' prices can still be edited (other fields) but cannot be switched to those models. Percentage/revenue-share is expressed via 'standard' with a unit-price multiplier. |
| `properties`                                                                                                                                                                                                                                                       | [Optional[models.PricePropertiesUnion]](../../models/pricepropertiesunion.md)                                                                                                                                                                                      | :heavy_minus_sign:                                                                                                                                                                                                                                                 | N/A                                                                                                                                                                                                                                                                |
| `payment_term`                                                                                                                                                                                                                                                     | [Optional[models.UpdatePricePaymentTerm]](../../models/updatepricepaymentterm.md)                                                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                                                                                                 | Billing timing preference: 'in_advance' (prepaid — charged upfront or drawn from a prepaid commitment) or 'in_arrears' (charged at period end).                                                                                                                    |
| `billing_cadence`                                                                                                                                                                                                                                                  | *OptionalNullable[str]*                                                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                                                                 | ISO 8601 duration for recurring fees (e.g., 'P1M' for monthly, 'P1Y' for yearly, or 'P0D' for one-time)                                                                                                                                                            |
| `feature`                                                                                                                                                                                                                                                          | [OptionalNullable[models.PriceFeatureInput]](../../models/pricefeatureinput.md)                                                                                                                                                                                    | :heavy_minus_sign:                                                                                                                                                                                                                                                 | Feature to associate. Set to null to remove existing feature. Omit to leave unchanged.                                                                                                                                                                             |
| `grant_discount_enabled`                                                                                                                                                                                                                                           | *Optional[bool]*                                                                                                                                                                                                                                                   | :heavy_minus_sign:                                                                                                                                                                                                                                                 | When true, grants applied to a subscription will discount usage charged by this price. Only supported for standard metered prices.                                                                                                                                 |
| `quantity`                                                                                                                                                                                                                                                         | *Optional[int]*                                                                                                                                                                                                                                                    | :heavy_minus_sign:                                                                                                                                                                                                                                                 | Quantity for invoice line items. Total per period = quantity × unitPrice. Only supported for fee prices; metered prices derive quantity from usage. Defaults to 1.                                                                                                 |
| `retries`                                                                                                                                                                                                                                                          | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                   | :heavy_minus_sign:                                                                                                                                                                                                                                                 | Configuration to override the default retry behavior of the client.                                                                                                                                                                                                |

### Response

**[models.SchemasPrice](../../models/schemasprice.md)**

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

<!-- UsageSnippet language="python" operationID="deletePrice" method="delete" path="/v0/prices/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    paygentic.prices.delete(id="<id>")

    # Use the SDK ...

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the price                                  |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Errors

| Error Type                      | Status Code                     | Content Type                    |
| ------------------------------- | ------------------------------- | ------------------------------- |
| errors.Error                    | 400                             | application/json                |
| errors.ValidationError          | 400                             | application/json                |
| errors.Error                    | 401, 403, 404                   | application/json                |
| errors.DeletePriceConflictError | 409                             | application/json                |
| errors.Error                    | 500                             | application/json                |
| errors.PaygenticDefaultError    | 4XX, 5XX                        | \*/\*                           |