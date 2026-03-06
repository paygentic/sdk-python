# Payments

## Overview

Create and manage one-off payments. A payment represents a single charge that a merchant wants to collect from a customer.

### Available Operations

* [list](#list) - List Payments
* [create](#create) - Create Payment
* [get](#get) - Get Payment

## list

List payments for the authenticated merchant with optional filters.

### Example Usage

<!-- UsageSnippet language="python" operationID="listPayments" method="get" path="/v0/payments" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.payments.list(request={})

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `request`                                                           | [models.ListPaymentsRequest](../../models/listpaymentsrequest.md)   | :heavy_check_mark:                                                  | The request object to use for the request.                          |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.ListPaymentsResponse](../../models/listpaymentsresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## create

Create a new payment for collecting a one-off charge. Returns a payment URL that can be shared with the customer.

### Example Usage

<!-- UsageSnippet language="python" operationID="createPayment" method="post" path="/v0/payments" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.payments.create(amount="10.50", currency="USD", idempotency_key="order_12345", reference="Order #12345", metadata={
        "orderId": "order_12345",
    }, success_redirect_url="https://example.com/success", save_payment_method=False, expires_in="P7D")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                          | Type                                                                                                                               | Required                                                                                                                           | Description                                                                                                                        |
| ---------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `amount`                                                                                                                           | *str*                                                                                                                              | :heavy_check_mark:                                                                                                                 | Payment amount in decimal format (e.g. '10.50'). Minimum 1.00, maximum 5,000.00. Contact support for higher limits.                |
| `currency`                                                                                                                         | [models.Currency](../../models/currency.md)                                                                                        | :heavy_check_mark:                                                                                                                 | ISO 4217 currency code.                                                                                                            |
| `merchant_id`                                                                                                                      | *Optional[str]*                                                                                                                    | :heavy_minus_sign:                                                                                                                 | Merchant organization ID. Required when using an API key that is not scoped to a single merchant.                                  |
| `customer_id`                                                                                                                      | *Optional[str]*                                                                                                                    | :heavy_minus_sign:                                                                                                                 | Optional customer ID. Must belong to this merchant.                                                                                |
| `idempotency_key`                                                                                                                  | *Optional[str]*                                                                                                                    | :heavy_minus_sign:                                                                                                                 | Client-provided key for safe retries. If a payment with the same key already exists, the existing payment is returned.             |
| `reference`                                                                                                                        | *Optional[str]*                                                                                                                    | :heavy_minus_sign:                                                                                                                 | Merchant-defined reference for this payment (e.g. order ID, invoice number).                                                       |
| `metadata`                                                                                                                         | Dict[str, *str*]                                                                                                                   | :heavy_minus_sign:                                                                                                                 | Arbitrary key-value string pairs to attach to the payment.                                                                         |
| `line_items`                                                                                                                       | List[[models.CreatePaymentLineItem](../../models/createpaymentlineitem.md)]                                                        | :heavy_minus_sign:                                                                                                                 | Optional breakdown of what the customer is being charged for.                                                                      |
| `success_redirect_url`                                                                                                             | *Optional[str]*                                                                                                                    | :heavy_minus_sign:                                                                                                                 | URL to redirect the customer to after a successful payment.                                                                        |
| `failure_redirect_url`                                                                                                             | *Optional[str]*                                                                                                                    | :heavy_minus_sign:                                                                                                                 | URL to redirect the customer to after a failed payment.                                                                            |
| `save_payment_method`                                                                                                              | *Optional[bool]*                                                                                                                   | :heavy_minus_sign:                                                                                                                 | Whether to save the customer's payment method for future use. Defaults to false.                                                   |
| `expires_in`                                                                                                                       | *Optional[str]*                                                                                                                    | :heavy_minus_sign:                                                                                                                 | ISO 8601 duration for the payment lifetime. Defaults to P30D (30 days). Maximum is P31D (31 days). Examples: PT1H, P1D, P7D, P30D. |
| `retries`                                                                                                                          | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                   | :heavy_minus_sign:                                                                                                                 | Configuration to override the default retry behavior of the client.                                                                |

### Response

**[models.Payment](../../models/payment.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get

Retrieve a single payment by ID.

### Example Usage

<!-- UsageSnippet language="python" operationID="getPayment" method="get" path="/v0/payments/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.payments.get(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | Payment session ID                                                  |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.Payment](../../models/payment.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |