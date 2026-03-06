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

    res = paygentic.prices.create(invoice_display_name="<value>", payment_term="instant", properties={
        "default": "<value>",
        "parameters": {
            "function": "linear",
            "gradient": "<value>",
            "max": "<value>",
            "min": "<value>",
        },
    })

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                       | Type                                                                                                                                                                                                                                                            | Required                                                                                                                                                                                                                                                        | Description                                                                                                                                                                                                                                                     |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `invoice_display_name`                                                                                                                                                                                                                                          | *str*                                                                                                                                                                                                                                                           | :heavy_check_mark:                                                                                                                                                                                                                                              | Line item label shown on customer invoices. Sample values: 'Claude Token Consumption', 'Storage Usage (GB)', 'Inference API Calls', 'Image Generation Count', 'Training Compute Hours', 'Data Transfer (TB)'                                                    |
| `payment_term`                                                                                                                                                                                                                                                  | [models.CreatePricePaymentTerm](../../models/createpricepaymentterm.md)                                                                                                                                                                                         | :heavy_check_mark:                                                                                                                                                                                                                                              | Billing timing preference. For billable metrics: 'instant' (charges immediately) or 'in_arrears' (charges at period end). For fees: 'in_advance' (charges upfront) or 'in_arrears' (charges at period end).                                                     |
| `properties`                                                                                                                                                                                                                                                    | [models.PricePropertiesUnion](../../models/pricepropertiesunion.md)                                                                                                                                                                                             | :heavy_check_mark:                                                                                                                                                                                                                                              | N/A                                                                                                                                                                                                                                                             |
| `billable_metric_id`                                                                                                                                                                                                                                            | *Optional[str]*                                                                                                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                                                                                                              | Unique identifier for a billable metric                                                                                                                                                                                                                         |
| `fee_id`                                                                                                                                                                                                                                                        | *Optional[str]*                                                                                                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                                                                                                              | The unique identifier for the fee referred to by this price. Either billableMetricId or feeId must be provided.                                                                                                                                                 |
| `model`                                                                                                                                                                                                                                                         | [Optional[models.CreatePriceModel]](../../models/createpricemodel.md)                                                                                                                                                                                           | :heavy_minus_sign:                                                                                                                                                                                                                                              | Pricing calculation model. Required for billable metrics, optional for fees (defaults to 'standard').                                                                                                                                                           |
| `billing_cadence`                                                                                                                                                                                                                                               | *OptionalNullable[str]*                                                                                                                                                                                                                                         | :heavy_minus_sign:                                                                                                                                                                                                                                              | ISO 8601 duration for recurring charges (e.g., 'P1M' for monthly, 'P1Y' for yearly) or 'P0D' for one-time charges. Required for fees, optional for billable metrics. Sample values: 'P0D' for one-time, 'P1M' for monthly recurring, 'P1Y' for yearly recurring |
| `feature`                                                                                                                                                                                                                                                       | [Optional[models.PriceFeatureInput]](../../models/pricefeatureinput.md)                                                                                                                                                                                         | :heavy_minus_sign:                                                                                                                                                                                                                                              | N/A                                                                                                                                                                                                                                                             |
| `retries`                                                                                                                                                                                                                                                       | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                | :heavy_minus_sign:                                                                                                                                                                                                                                              | Configuration to override the default retry behavior of the client.                                                                                                                                                                                             |

### Response

**[models.SchemasPrice](../../models/schemasprice.md)**

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
| errors.Error                 | 401, 403                     | application/json             |
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

| Parameter                                                                                                                                                                                                   | Type                                                                                                                                                                                                        | Required                                                                                                                                                                                                    | Description                                                                                                                                                                                                 |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                                                                                        | *str*                                                                                                                                                                                                       | :heavy_check_mark:                                                                                                                                                                                          | The unique identifier of the price                                                                                                                                                                          |
| `billable_metric_id`                                                                                                                                                                                        | *Optional[str]*                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                          | Unique identifier for a billable metric                                                                                                                                                                     |
| `invoice_display_name`                                                                                                                                                                                      | *Optional[str]*                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                          | Updated invoice line item label. Sample values: 'LLM Token Usage', 'Storage Charges', 'API Call Fees'                                                                                                       |
| `model`                                                                                                                                                                                                     | [Optional[models.UpdatePriceModel]](../../models/updatepricemodel.md)                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                          | The pricing model to be used, which can be standard, dynamic, volume-based, or percentage-based.                                                                                                            |
| `properties`                                                                                                                                                                                                | [Optional[models.PricePropertiesUnion]](../../models/pricepropertiesunion.md)                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                                          | N/A                                                                                                                                                                                                         |
| `payment_term`                                                                                                                                                                                              | [Optional[models.UpdatePricePaymentTerm]](../../models/updatepricepaymentterm.md)                                                                                                                           | :heavy_minus_sign:                                                                                                                                                                                          | Billing timing preference. For billable metrics: 'instant' (charges immediately) or 'in_arrears' (charges at period end). For fees: 'in_advance' (charges upfront) or 'in_arrears' (charges at period end). |
| `billing_cadence`                                                                                                                                                                                           | *OptionalNullable[str]*                                                                                                                                                                                     | :heavy_minus_sign:                                                                                                                                                                                          | ISO 8601 duration for recurring fees (e.g., 'P1M' for monthly, 'P1Y' for yearly, or 'P0D' for one-time)                                                                                                     |
| `feature`                                                                                                                                                                                                   | [OptionalNullable[models.PriceFeatureInput]](../../models/pricefeatureinput.md)                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                          | Feature to associate. Set to null to remove existing feature. Omit to leave unchanged.                                                                                                                      |
| `retries`                                                                                                                                                                                                   | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                          | Configuration to override the default retry behavior of the client.                                                                                                                                         |

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

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |