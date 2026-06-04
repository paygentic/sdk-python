# PaymentSessions

## Overview

Handle payment session lifecycle and processing across various entity types including invoices and subscriptions

### Available Operations

* [list_payment_sessions](#list_payment_sessions) - List

## list_payment_sessions

List payment sessions for the authenticated merchant with optional filters. Supports filtering by subscriptionId, customerId, status, and entityType. When subscriptionId is provided the result includes both the subscription's own activation session (entityType='subscription') and any session attached to invoices for that subscription (entityType='invoice'). When customerId is provided the result covers the customer's full payment history: payment-link sessions (entityType='payment'), the activation sessions of the customer's subscriptions, and the sessions of those subscriptions' invoices.

### Example Usage

<!-- UsageSnippet language="python" operationID="listPaymentSessions" method="get" path="/v0/paymentSessions" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.payment_sessions.list_payment_sessions(request={})

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                       | Type                                                                            | Required                                                                        | Description                                                                     |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| `request`                                                                       | [models.ListPaymentSessionsRequest](../../models/listpaymentsessionsrequest.md) | :heavy_check_mark:                                                              | The request object to use for the request.                                      |
| `retries`                                                                       | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                | :heavy_minus_sign:                                                              | Configuration to override the default retry behavior of the client.             |

### Response

**[models.ListPaymentSessionsResponse](../../models/listpaymentsessionsresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |