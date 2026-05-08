# Customers

## Overview

A `Customer` is an entity connected to a `Merchant` via a `Subscription`. This represents the merchant-facing perspective of `Consumers` who purchase their `Products`.

### Available Operations

* [list](#list) - List by Merchant
* [create](#create) - Create
* [get](#get) - Get
* [delete](#delete) - Delete
* [update](#update) - Update
* [list_customer_payment_methods](#list_customer_payment_methods) - List payment methods
* [create_customer_payment_method](#create_customer_payment_method) - Set up a payment method

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

| Parameter                                                                                                                                                                                                     | Type                                                                                                                                                                                                          | Required                                                                                                                                                                                                      | Description                                                                                                                                                                                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `organization_id`                                                                                                                                                                                             | *str*                                                                                                                                                                                                         | :heavy_check_mark:                                                                                                                                                                                            | ID of the merchant organization to filter customers by                                                                                                                                                        |
| `limit`                                                                                                                                                                                                       | *Optional[int]*                                                                                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                                            | Number of customers to return                                                                                                                                                                                 |
| `offset`                                                                                                                                                                                                      | *Optional[int]*                                                                                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                                            | Number of customers to skip                                                                                                                                                                                   |
| `name`                                                                                                                                                                                                        | *Optional[str]*                                                                                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                                            | Filter customers by consumer name (case-insensitive substring match). Minimum 3 characters required for efficient index usage.                                                                                |
| `email`                                                                                                                                                                                                       | *Optional[str]*                                                                                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                                            | Filter customers by billing email (case-insensitive substring match). Minimum 3 characters required for efficient index usage. Accepts partial values — e.g. a domain ("acme.com") or local part ("billing"). |
| `external_id`                                                                                                                                                                                                 | *Optional[str]*                                                                                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                                            | Filter customers by exact external ID match.                                                                                                                                                                  |
| `retries`                                                                                                                                                                                                     | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                            | Configuration to override the default retry behavior of the client.                                                                                                                                           |

### Response

**[models.ListCustomersResponse](../../models/listcustomersresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
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

    res = paygentic.customers.create(merchant_id="org_YS8jkP59V71TdUvj", consumer={
        "name": "Jane Smith",
        "email": "jane@example.com",
        "address": {
            "city": "San Francisco",
            "state": "CA",
            "country": "US",
        },
    })

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                                     | Type                                                                                                                                                                                                                                                                          | Required                                                                                                                                                                                                                                                                      | Description                                                                                                                                                                                                                                                                   |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `merchant_id`                                                                                                                                                                                                                                                                 | *str*                                                                                                                                                                                                                                                                         | :heavy_check_mark:                                                                                                                                                                                                                                                            | Unique identifier for an organization                                                                                                                                                                                                                                         |
| `consumer`                                                                                                                                                                                                                                                                    | [Optional[models.CreateCustomerConsumer]](../../models/createcustomerconsumer.md)                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                                                                            | Fields to create a new consumer. Will use an existing consumer if one exists with the same email address. Required if `consumerId` is not provided. Address with complete tax information (country, state, zipCode) is required for tax calculation when using Paygentic Tax. |
| `consumer_id`                                                                                                                                                                                                                                                                 | *Optional[str]*                                                                                                                                                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                                                                                                            | Unique identifier for an organization                                                                                                                                                                                                                                         |
| `tax_id`                                                                                                                                                                                                                                                                      | *Optional[str]*                                                                                                                                                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                                                                                                            | Optional business tax registration identifier. Sample values: 'GB123456789' for UK VAT, 'DE123456789' for German VAT, 'FR12345678901' for French VAT. Supplying this value enables inter-company tax handling and exemption from standard tax collection.                     |
| `external_id`                                                                                                                                                                                                                                                                 | *Optional[str]*                                                                                                                                                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                                                                                                            | Merchant-defined identifier for this customer in their own system.                                                                                                                                                                                                            |
| `tax_rates`                                                                                                                                                                                                                                                                   | Dict[str, *float*]                                                                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                                                                            | An object mapping plan IDs, metric IDs, or 'default' to a tax rate percentage (e.g., 13 for 13%)                                                                                                                                                                              |
| `retries`                                                                                                                                                                                                                                                                     | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                            | Configuration to override the default retry behavior of the client.                                                                                                                                                                                                           |

### Response

**[models.CreateCustomerResponse](../../models/createcustomerresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404, 409                | application/json             |
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
| `external_id`                                                                                                                                                                                                                                                     | *OptionalNullable[str]*                                                                                                                                                                                                                                           | :heavy_minus_sign:                                                                                                                                                                                                                                                | Merchant-defined identifier for this customer in their own system. Set to null to clear.                                                                                                                                                                          |
| `tax_rates`                                                                                                                                                                                                                                                       | [Optional[models.TaxRates]](../../models/taxrates.md)                                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                                                                | N/A                                                                                                                                                                                                                                                               |
| `notification_settings`                                                                                                                                                                                                                                           | [Optional[models.UpdateCustomerNotificationSettings]](../../models/updatecustomernotificationsettings.md)                                                                                                                                                         | :heavy_minus_sign:                                                                                                                                                                                                                                                | Notification preferences for this customer. Only provided fields are updated.                                                                                                                                                                                     |
| `retries`                                                                                                                                                                                                                                                         | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                                                                                                | Configuration to override the default retry behavior of the client.                                                                                                                                                                                               |

### Response

**[models.Customer](../../models/customer.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404, 409           | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## list_customer_payment_methods

List off-session payment methods saved for this customer.

### Example Usage

<!-- UsageSnippet language="python" operationID="listCustomerPaymentMethods" method="get" path="/v0/customers/{id}/paymentMethods" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.customers.list_customer_payment_methods(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the customer.                              |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.ListCustomerPaymentMethodsResponse](../../models/listcustomerpaymentmethodsresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## create_customer_payment_method

Create a payment session that captures a new off-session payment method for this customer without charging. The response contains a hosted-page URL — redirect the customer to it, or load it inside an iframe (when iframed, the page reports outcomes via `postMessage` to the parent window).

### Example Usage

<!-- UsageSnippet language="python" operationID="createCustomerPaymentMethod" method="post" path="/v0/customers/{id}/paymentMethods" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.customers.create_customer_payment_method(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                              | Type                                                                                                                   | Required                                                                                                               | Description                                                                                                            |
| ---------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                   | *str*                                                                                                                  | :heavy_check_mark:                                                                                                     | The unique identifier of the customer.                                                                                 |
| `success_redirect_url`                                                                                                 | *Optional[str]*                                                                                                        | :heavy_minus_sign:                                                                                                     | URL the customer is redirected to on success. When the page is iframed, success is reported via `postMessage` instead. |
| `failure_redirect_url`                                                                                                 | *Optional[str]*                                                                                                        | :heavy_minus_sign:                                                                                                     | URL the customer is redirected to on failure. When the page is iframed, failure is reported via `postMessage` instead. |
| `metadata`                                                                                                             | Dict[str, *Any*]                                                                                                       | :heavy_minus_sign:                                                                                                     | Arbitrary key/value pairs to attach to the session.                                                                    |
| `retries`                                                                                                              | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                       | :heavy_minus_sign:                                                                                                     | Configuration to override the default retry behavior of the client.                                                    |

### Response

**[models.PaymentSession](../../models/paymentsession.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |