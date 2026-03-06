# Customers

## Overview

A `Customer` is an entity connected to a `Merchant` via a `Subscription`. This represents the merchant-facing perspective of `Consumers` who purchase their `Products`.

### Available Operations

* [list](#list) - List by Merchant
* [create](#create) - Create
* [get](#get) - Get
* [delete](#delete) - Delete
* [update](#update) - Update

## list

List by Merchant

### Example Usage

<!-- UsageSnippet language="python" operationID="listCustomers" method="get" path="/v0/customers" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.customers.list(organization_id="<id>", limit=10, offset=0)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `organization_id`                                                   | *str*                                                               | :heavy_check_mark:                                                  | ID of the merchant organization to filter customers by              |
| `limit`                                                             | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | Number of customers to return                                       |
| `offset`                                                            | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | Number of customers to skip                                         |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.ListCustomersResponse](../../models/listcustomersresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 403                          | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## create

Create a new customer for a merchant organization. This endpoint is currently only used by the Paygentic platform as part of the subscription flow.

### Example Usage

<!-- UsageSnippet language="python" operationID="createCustomer" method="post" path="/v0/customers" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.customers.create(merchant_id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                                     | Type                                                                                                                                                                                                                                                                          | Required                                                                                                                                                                                                                                                                      | Description                                                                                                                                                                                                                                                                   |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `merchant_id`                                                                                                                                                                                                                                                                 | *str*                                                                                                                                                                                                                                                                         | :heavy_check_mark:                                                                                                                                                                                                                                                            | Unique identifier for an organization                                                                                                                                                                                                                                         |
| `consumer`                                                                                                                                                                                                                                                                    | [Optional[models.Consumer]](../../models/consumer.md)                                                                                                                                                                                                                         | :heavy_minus_sign:                                                                                                                                                                                                                                                            | Fields to create a new consumer. Will use an existing consumer if one exists with the same email address. Required if `consumerId` is not provided. Address with complete tax information (country, state, zipCode) is required for tax calculation when using Paygentic Tax. |
| `consumer_id`                                                                                                                                                                                                                                                                 | *Optional[str]*                                                                                                                                                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                                                                                                            | Unique identifier for an organization                                                                                                                                                                                                                                         |
| `tax_id`                                                                                                                                                                                                                                                                      | *Optional[str]*                                                                                                                                                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                                                                                                            | Optional business tax registration identifier. Sample values: 'GB123456789' for UK VAT, 'DE123456789' for German VAT, 'FR12345678901' for French VAT. Supplying this value enables inter-company tax handling and exemption from standard tax collection.                     |
| `tax_rates`                                                                                                                                                                                                                                                                   | Dict[str, *float*]                                                                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                                                                            | An object mapping plan IDs, metric IDs, or 'default' to a tax rate percentage (e.g., 13 for 13%)                                                                                                                                                                              |
| `retries`                                                                                                                                                                                                                                                                     | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                            | Configuration to override the default retry behavior of the client.                                                                                                                                                                                                           |

### Response

**[models.CreateCustomerResponse](../../models/createcustomerresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get

Get

### Example Usage

<!-- UsageSnippet language="python" operationID="getCustomer" method="get" path="/v0/customers/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.customers.get(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the customer.                              |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.Customer](../../models/customer.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## delete

Delete

### Example Usage

<!-- UsageSnippet language="python" operationID="deleteCustomer" method="delete" path="/v0/customers/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    paygentic.customers.delete(id="<id>")

    # Use the SDK ...

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the customer.                              |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Errors

| Error Type                         | Status Code                        | Content Type                       |
| ---------------------------------- | ---------------------------------- | ---------------------------------- |
| errors.Error                       | 401, 403, 404                      | application/json                   |
| errors.DeleteCustomerConflictError | 409                                | application/json                   |
| errors.Error                       | 500                                | application/json                   |
| errors.PaygenticDefaultError       | 4XX, 5XX                           | \*/\*                              |

## update

Update

### Example Usage

<!-- UsageSnippet language="python" operationID="updateCustomer" method="patch" path="/v0/customers/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.customers.update(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                         | Type                                                                                                                                                                                                                                                              | Required                                                                                                                                                                                                                                                          | Description                                                                                                                                                                                                                                                       |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                                                                                                                                              | *str*                                                                                                                                                                                                                                                             | :heavy_check_mark:                                                                                                                                                                                                                                                | The unique identifier of the customer.                                                                                                                                                                                                                            |
| `tax_id`                                                                                                                                                                                                                                                          | *OptionalNullable[str]*                                                                                                                                                                                                                                           | :heavy_minus_sign:                                                                                                                                                                                                                                                | Business tax registration identifier. Sample values: 'GB123456789' for UK VAT, 'DE123456789' for German VAT, 'FR12345678901' for French VAT. Enables inter-company tax handling and exemption from standard tax collection. Assign null to delete the identifier. |
| `tax_rates`                                                                                                                                                                                                                                                       | [Optional[models.TaxRates]](../../models/taxrates.md)                                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                                                                | N/A                                                                                                                                                                                                                                                               |
| `retries`                                                                                                                                                                                                                                                         | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                                                                                                | Configuration to override the default retry behavior of the client.                                                                                                                                                                                               |

### Response

**[models.Customer](../../models/customer.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |