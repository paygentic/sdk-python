# Plans

## Overview

A `Plan` links a collection of `Prices` to a `Product`. It functions as a pricing structure document for a particular feature set or service offering.

### Available Operations

* [create](#create) - Create
* [list](#list) - List
* [list_available](#list_available) - List Available Plans
* [get](#get) - Get
* [update](#update) - Update

## create

Create

### Example Usage

<!-- UsageSnippet language="python" operationID="createPlan" method="post" path="/v0/plans" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.plans.create(currency="Won", merchant_id="<id>", name="<value>", default_tax_code="eservice", default_tax_rate=0, tax_behavior="exclusive", renewal_reminder_enabled=True, renewal_reminder_days=3, billing_version=0)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `currency`                                                                                                                                                                                                                                                                                                   | *str*                                                                                                                                                                                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                                                                                                           | Three-letter ISO 4217 currency code for plan pricing. Must be one of the merchant's supported currencies. Sample values: 'USD' for US dollars, 'EUR' for euros, 'GBP' for British pounds                                                                                                                     |
| `merchant_id`                                                                                                                                                                                                                                                                                                | *str*                                                                                                                                                                                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                                                                                                           | Unique identifier for an organization                                                                                                                                                                                                                                                                        |
| `name`                                                                                                                                                                                                                                                                                                       | *str*                                                                                                                                                                                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                                                                                                           | Plan identifier visible to customers. Sample values: 'Basic Tier', 'Business Package', 'Enterprise Solution', 'Metered Billing', 'Free Tier', 'Premium Access'                                                                                                                                               |
| `billing_interval`                                                                                                                                                                                                                                                                                           | *Optional[str]*                                                                                                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Recurring billing period frequency. Sample values: 'monthly' for monthly billing, 'yearly' for annual billing, 'weekly' for weekly billing                                                                                                                                                                   |
| `default_tax_code`                                                                                                                                                                                                                                                                                           | *Optional[str]*                                                                                                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Default tax code for plan line items. Common values: 'eservice' (electronically supplied services), 'saas' (software as a service), 'consulting', 'ebook', 'standard', 'reduced', 'exempt'. Full list available via GET /tax/codes endpoint.                                                                 |
| `default_tax_rate`                                                                                                                                                                                                                                                                                           | *Optional[float]*                                                                                                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Fallback tax rate percentage when automatic tax calculation fails. Sample values: 8.5 represents 8.5% tax, 10.0 represents 10% tax, 0 represents no tax                                                                                                                                                      |
| `description`                                                                                                                                                                                                                                                                                                | *Optional[str]*                                                                                                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Plan details explaining included features and limits. Sample values: 'Claude API access with 500K tokens monthly allowance', 'Unlimited cloud storage plus real-time analytics tools', 'Complete machine learning infrastructure with GPU access', 'Flexible usage-based pricing with no monthly commitment' |
| `invoice_display_name`                                                                                                                                                                                                                                                                                       | *Optional[str]*                                                                                                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Plan name shown on billing statements. Sample values: 'LLM API Basic Plan', 'Data Warehouse Business', 'ML Platform Enterprise', 'Pay-Per-Use Model'                                                                                                                                                         |
| `prices`                                                                                                                                                                                                                                                                                                     | List[*str*]                                                                                                                                                                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Array of price IDs to associate with this plan                                                                                                                                                                                                                                                               |
| `product_id`                                                                                                                                                                                                                                                                                                 | *Optional[str]*                                                                                                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Unique identifier for a product                                                                                                                                                                                                                                                                              |
| `tax_behavior`                                                                                                                                                                                                                                                                                               | [Optional[models.CreatePlanTaxBehavior]](../../models/createplantaxbehavior.md)                                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Whether tax is added on top of the price (exclusive) or included in the price (inclusive)                                                                                                                                                                                                                    |
| `renewal_reminder_enabled`                                                                                                                                                                                                                                                                                   | *Optional[bool]*                                                                                                                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Whether to send renewal reminder emails to customers before their subscription renews                                                                                                                                                                                                                        |
| `renewal_reminder_days`                                                                                                                                                                                                                                                                                      | *Optional[int]*                                                                                                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Number of days before renewal to send the reminder email                                                                                                                                                                                                                                                     |
| `billing_version`                                                                                                                                                                                                                                                                                            | [Optional[models.BillingVersion]](../../models/billingversion.md)                                                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Billing engine version. 0 = legacy fee-schedule billing (Legacy), 1 = line-item billing with metered usage support (Standard).                                                                                                                                                                               |
| `retries`                                                                                                                                                                                                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Configuration to override the default retry behavior of the client.                                                                                                                                                                                                                                          |

### Response

**[models.Plan](../../models/plan.md)**

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

<!-- UsageSnippet language="python" operationID="listPlans" method="get" path="/v0/plans" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.plans.list(request={})

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `request`                                                           | [models.ListPlansRequest](../../models/listplansrequest.md)         | :heavy_check_mark:                                                  | The request object to use for the request.                          |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.ListPlansResponse](../../models/listplansresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## list_available

Retrieves all plans for a merchant that the customer does not have an active or pending subscription for. When a customer has a subscription for any plan within a product, all plans from that product are excluded.

### Example Usage

<!-- UsageSnippet language="python" operationID="listAvailablePlans" method="get" path="/v0/plans/available" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.plans.list_available(customer_id="<id>", limit=10, offset=0)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                  | Type                                                                                       | Required                                                                                   | Description                                                                                |
| ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| `customer_id`                                                                              | *str*                                                                                      | :heavy_check_mark:                                                                         | The customer to check subscriptions for. The merchant is derived from the customer record. |
| `product_id`                                                                               | *Optional[str]*                                                                            | :heavy_minus_sign:                                                                         | Optional filter by product ID                                                              |
| `search`                                                                                   | *Optional[str]*                                                                            | :heavy_minus_sign:                                                                         | Optional search text to filter plan names (case-insensitive)                               |
| `limit`                                                                                    | *Optional[int]*                                                                            | :heavy_minus_sign:                                                                         | Number of plans to return                                                                  |
| `offset`                                                                                   | *Optional[int]*                                                                            | :heavy_minus_sign:                                                                         | Number of plans to skip                                                                    |
| `retries`                                                                                  | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                           | :heavy_minus_sign:                                                                         | Configuration to override the default retry behavior of the client.                        |

### Response

**[models.ListAvailablePlansResponse](../../models/listavailableplansresponse.md)**

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

<!-- UsageSnippet language="python" operationID="getPlan" method="get" path="/v0/plans/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.plans.get(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the plan                                   |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.Plan](../../models/plan.md)**

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

<!-- UsageSnippet language="python" operationID="updatePlan" method="patch" path="/v0/plans/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.plans.update(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `id`                                                                                                                                                                                                                                                                                                         | *str*                                                                                                                                                                                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                                                                                                           | The unique identifier of the plan                                                                                                                                                                                                                                                                            |
| `billing_interval`                                                                                                                                                                                                                                                                                           | *Optional[str]*                                                                                                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Recurring billing period frequency. Sample values: 'monthly' for monthly billing, 'yearly' for annual billing, 'weekly' for weekly billing                                                                                                                                                                   |
| `default_tax_code`                                                                                                                                                                                                                                                                                           | *Optional[str]*                                                                                                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Default tax code for plan line items. Common values: 'eservice' (electronically supplied services), 'saas' (software as a service), 'consulting', 'ebook', 'standard', 'reduced', 'exempt'. Full list available via GET /tax/codes endpoint.                                                                 |
| `default_tax_rate`                                                                                                                                                                                                                                                                                           | *Optional[float]*                                                                                                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Fallback tax rate (as percentage) if automatic tax calculation is unavailable                                                                                                                                                                                                                                |
| `description`                                                                                                                                                                                                                                                                                                | *Optional[str]*                                                                                                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Plan details explaining included features and limits. Sample values: 'Claude API access with 500K tokens monthly allowance', 'Unlimited cloud storage plus real-time analytics tools', 'Complete machine learning infrastructure with GPU access', 'Flexible usage-based pricing with no monthly commitment' |
| `invoice_display_name`                                                                                                                                                                                                                                                                                       | *Optional[str]*                                                                                                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Plan name shown on billing statements. Sample values: 'LLM API Basic Plan', 'Data Warehouse Business', 'ML Platform Enterprise', 'Pay-Per-Use Model'                                                                                                                                                         |
| `name`                                                                                                                                                                                                                                                                                                       | *Optional[str]*                                                                                                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Plan identifier visible to customers. Sample values: 'Basic Tier', 'Business Package', 'Enterprise Solution', 'Metered Billing', 'Free Tier', 'Premium Access'                                                                                                                                               |
| `prices`                                                                                                                                                                                                                                                                                                     | List[*str*]                                                                                                                                                                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Array of price IDs to associate with this plan                                                                                                                                                                                                                                                               |
| `tax_behavior`                                                                                                                                                                                                                                                                                               | [Optional[models.UpdatePlanTaxBehavior]](../../models/updateplantaxbehavior.md)                                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Whether tax is added on top of the price (exclusive) or included in the price (inclusive)                                                                                                                                                                                                                    |
| `renewal_reminder_enabled`                                                                                                                                                                                                                                                                                   | *Optional[bool]*                                                                                                                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Whether to send renewal reminder emails to customers before their subscription renews                                                                                                                                                                                                                        |
| `renewal_reminder_days`                                                                                                                                                                                                                                                                                      | *Optional[int]*                                                                                                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Number of days before renewal to send the reminder email                                                                                                                                                                                                                                                     |
| `retries`                                                                                                                                                                                                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                                                                                                           | Configuration to override the default retry behavior of the client.                                                                                                                                                                                                                                          |

### Response

**[models.Plan](../../models/plan.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |