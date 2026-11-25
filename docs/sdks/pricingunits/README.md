# PricingUnits

## Overview

A `PricingUnit` is a merchant-scoped catalog object that names a credit denomination and the rate (`conversionRate`) at which it converts to an invoicing `currency`. Credit-denominated prices draw a customer's balance for the unit; the unit holds no balance itself.

### Available Operations

* [create_pricing_unit](#create_pricing_unit) - Create
* [list_pricing_units](#list_pricing_units) - List
* [get_pricing_unit](#get_pricing_unit) - Get

## create_pricing_unit

Create

### Example Usage

<!-- UsageSnippet language="python" operationID="createPricingUnit" method="post" path="/v0/pricingUnits" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.pricing_units.create_pricing_unit(merchant_id="<id>", identifier="<value>", display_name="Jay.Kerluke70", short_name="<value>", conversion_rate="<value>", currency="Seychelles Rupee")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                     | Type                                                                                          | Required                                                                                      | Description                                                                                   |
| --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| `merchant_id`                                                                                 | *str*                                                                                         | :heavy_check_mark:                                                                            | Unique identifier for an organization                                                         |
| `identifier`                                                                                  | *str*                                                                                         | :heavy_check_mark:                                                                            | Programmatic identifier, a slug unique per merchant (e.g. `credits`).                         |
| `display_name`                                                                                | *str*                                                                                         | :heavy_check_mark:                                                                            | Human-readable name shown in the UI.                                                          |
| `short_name`                                                                                  | *str*                                                                                         | :heavy_check_mark:                                                                            | Short label used on invoice lines (e.g. `credits`).                                           |
| `conversion_rate`                                                                             | *str*                                                                                         | :heavy_check_mark:                                                                            | Default rate converting one credit to the invoicing currency ($/credit), as a decimal string. |
| `currency`                                                                                    | *str*                                                                                         | :heavy_check_mark:                                                                            | ISO 4217 currency code that `conversionRate` maps to (e.g. `USD`).                            |
| `retries`                                                                                     | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                              | :heavy_minus_sign:                                                                            | Configuration to override the default retry behavior of the client.                           |

### Response

**[models.PricingUnit](../../models/pricingunit.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404, 409           | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## list_pricing_units

List

### Example Usage

<!-- UsageSnippet language="python" operationID="listPricingUnits" method="get" path="/v0/pricingUnits" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.pricing_units.list_pricing_units(request={})

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                 | Type                                                                      | Required                                                                  | Description                                                               |
| ------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| `request`                                                                 | [models.ListPricingUnitsRequest](../../models/listpricingunitsrequest.md) | :heavy_check_mark:                                                        | The request object to use for the request.                                |
| `retries`                                                                 | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)          | :heavy_minus_sign:                                                        | Configuration to override the default retry behavior of the client.       |

### Response

**[models.ListPricingUnitsResponse](../../models/listpricingunitsresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get_pricing_unit

Get

### Example Usage

<!-- UsageSnippet language="python" operationID="getPricingUnit" method="get" path="/v0/pricingUnits/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.pricing_units.get_pricing_unit(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.PricingUnit](../../models/pricingunit.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |