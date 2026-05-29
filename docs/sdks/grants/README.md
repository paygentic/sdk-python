# Entitlements.Grants

## Overview

### Available Operations

* [list](#list) - List Grants
* [create](#create) - Create Grant
* [purchase](#purchase) - Purchase Grant
* [get](#get) - Get Grant
* [void](#void) - Void Grant

## list

List grants for a metered entitlement. Active grants are returned by default; pass `includeVoided=true` to include voided grants.

### Example Usage

<!-- UsageSnippet language="python" operationID="listEntitlementGrants" method="get" path="/v1/entitlements/{entitlementId}/grants" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.entitlements.grants.list(entitlement_id="<id>", limit=20, offset=0, include_voided=False)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `entitlement_id`                                                    | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the entitlement.                           |
| `limit`                                                             | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | Maximum number of grants to return per page.                        |
| `offset`                                                            | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | Number of grants to skip.                                           |
| `include_voided`                                                    | *Optional[bool]*                                                    | :heavy_minus_sign:                                                  | When true, voided grants are included in the response.              |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.ListEntitlementGrantsResponse](../../models/listentitlementgrantsresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## create

Create a grant directly for a metered entitlement, crediting the customer's balance immediately. The entitlement must belong to an active v1 subscription.

### Example Usage: minimal

<!-- UsageSnippet language="python" operationID="createEntitlementGrant" method="post" path="/v1/entitlements/{entitlementId}/grants" example="minimal" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.entitlements.grants.create(entitlement_id="<id>", amount=100, idempotency_key="grant-initial-100")

    # Handle response
    print(res)

```
### Example Usage: withExpiry

<!-- UsageSnippet language="python" operationID="createEntitlementGrant" method="post" path="/v1/entitlements/{entitlementId}/grants" example="withExpiry" -->
```python
import os
from paygentic_sdk import Paygentic
from paygentic_sdk.utils import parse_datetime


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.entitlements.grants.create(entitlement_id="<id>", amount=500, idempotency_key="grant-march-2026-promo", effective_at=parse_datetime("2026-03-14T00:00:00Z"), expires_at=parse_datetime("2026-04-14T00:00:00Z"))

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                                                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `entitlement_id`                                                                                                                                                                                                                                                                                                                                             | *str*                                                                                                                                                                                                                                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                           | The unique identifier of the entitlement to grant credits to.                                                                                                                                                                                                                                                                                                |
| `amount`                                                                                                                                                                                                                                                                                                                                                     | *float*                                                                                                                                                                                                                                                                                                                                                      | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                           | The number of credits to grant.                                                                                                                                                                                                                                                                                                                              |
| `idempotency_key`                                                                                                                                                                                                                                                                                                                                            | *str*                                                                                                                                                                                                                                                                                                                                                        | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                           | Idempotency key to prevent duplicate grants. Must be unique per entitlement.                                                                                                                                                                                                                                                                                 |
| `effective_at`                                                                                                                                                                                                                                                                                                                                               | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                                                                                                                                                                                         | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                           | When the grant becomes effective. Defaults to now.                                                                                                                                                                                                                                                                                                           |
| `expires_at`                                                                                                                                                                                                                                                                                                                                                 | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                                                                                                                                                                                         | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                           | When the grant expires. If omitted, the grant does not expire.                                                                                                                                                                                                                                                                                               |
| `reset_max_rollover`                                                                                                                                                                                                                                                                                                                                         | *Optional[float]*                                                                                                                                                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                           | Maximum balance carried over at the entitlement's reset boundary. If omitted, the entire balance rolls over until consumed or expired. Set to 0 to discard any remaining balance at each reset. Ignored when the target entitlement has no `usagePeriod` (one-time entitlement) — one-time entitlements have no reset boundary, so this field has no effect. |
| `reset_min_rollover`                                                                                                                                                                                                                                                                                                                                         | *Optional[float]*                                                                                                                                                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                           | Minimum balance at the entitlement's reset boundary; balances below this are floored up. Defaults to 0 (no floor). Ignored when the target entitlement has no `usagePeriod` (one-time entitlement).                                                                                                                                                          |
| `retries`                                                                                                                                                                                                                                                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                           | Configuration to override the default retry behavior of the client.                                                                                                                                                                                                                                                                                          |

### Response

**[models.Grant](../../models/grant.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404, 409                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## purchase

Create an ad-hoc invoice with a payment session for a grant purchase. The customer pays via the returned payment URL; the grant is created automatically on payment completion. If payment expires, the invoice is cancelled and no grant is created.

To confirm payment completion, subscribe to the `invoice.paid.v0` webhook. The payload includes the original `invoiceId` and the created `grantId`, so you can correlate the purchase response with downstream fulfilment without an extra fetch. As a fallback if you cannot consume webhooks, poll `GET /v2/invoices/{invoiceId}` (interval 2s, timeout 60s) and check for `status === "PAID"`.

### Example Usage: basic

<!-- UsageSnippet language="python" operationID="purchaseEntitlementGrant" method="post" path="/v1/entitlements/{entitlementId}/grants/purchase" example="basic" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.entitlements.grants.purchase(entitlement_id="<id>", amount=1000, price="5.00", idempotency_key="purchase-march-2026-topup")

    # Handle response
    print(res)

```
### Example Usage: withOptions

<!-- UsageSnippet language="python" operationID="purchaseEntitlementGrant" method="post" path="/v1/entitlements/{entitlementId}/grants/purchase" example="withOptions" -->
```python
import os
from paygentic_sdk import Paygentic
from paygentic_sdk.utils import parse_datetime


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.entitlements.grants.purchase(entitlement_id="<id>", amount=500, price="2.50", idempotency_key="purchase-promo-500", effective_at=parse_datetime("2026-03-14T00:00:00Z"), expires_at=parse_datetime("2026-04-14T00:00:00Z"), success_url="https://example.com/success", cancel_url="https://example.com/cancel", payment_expires_at=parse_datetime("2026-03-15T00:00:00Z"))

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                                                                                                                             | Type                                                                                                                                                                                                                                                                                                                                                                  | Required                                                                                                                                                                                                                                                                                                                                                              | Description                                                                                                                                                                                                                                                                                                                                                           |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `entitlement_id`                                                                                                                                                                                                                                                                                                                                                      | *str*                                                                                                                                                                                                                                                                                                                                                                 | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                                    | The unique identifier of the entitlement to purchase credits for.                                                                                                                                                                                                                                                                                                     |
| `amount`                                                                                                                                                                                                                                                                                                                                                              | *float*                                                                                                                                                                                                                                                                                                                                                               | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                                    | The number of credits to grant upon payment completion.                                                                                                                                                                                                                                                                                                               |
| `price`                                                                                                                                                                                                                                                                                                                                                               | *str*                                                                                                                                                                                                                                                                                                                                                                 | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                                    | The price in decimal format (e.g., '5.00' for $5.00 USD). Must be at least $0.50.                                                                                                                                                                                                                                                                                     |
| `idempotency_key`                                                                                                                                                                                                                                                                                                                                                     | *str*                                                                                                                                                                                                                                                                                                                                                                 | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                                    | Caller-provided deduplication key. Retrying with the same key returns the existing invoice.                                                                                                                                                                                                                                                                           |
| `effective_at`                                                                                                                                                                                                                                                                                                                                                        | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                                                                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                    | When the grant becomes effective. Defaults to now.                                                                                                                                                                                                                                                                                                                    |
| `expires_at`                                                                                                                                                                                                                                                                                                                                                          | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                                                                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                    | When the grant expires. If omitted, the grant does not expire.                                                                                                                                                                                                                                                                                                        |
| `success_url`                                                                                                                                                                                                                                                                                                                                                         | *Optional[str]*                                                                                                                                                                                                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                    | URL to redirect the customer to after successful payment.                                                                                                                                                                                                                                                                                                             |
| `cancel_url`                                                                                                                                                                                                                                                                                                                                                          | *Optional[str]*                                                                                                                                                                                                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                    | URL to redirect the customer to if payment is cancelled.                                                                                                                                                                                                                                                                                                              |
| `payment_expires_at`                                                                                                                                                                                                                                                                                                                                                  | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                                                                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                    | When the payment session expires. If omitted, uses the default expiry.                                                                                                                                                                                                                                                                                                |
| `reset_max_rollover`                                                                                                                                                                                                                                                                                                                                                  | *Optional[float]*                                                                                                                                                                                                                                                                                                                                                     | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                    | Maximum balance carried over at the entitlement's reset boundary. If omitted, the purchased grant balance rolls over until consumed or expired. Set to 0 to discard any remaining balance at each reset. Ignored when the target entitlement has no `usagePeriod` (one-time entitlement) — one-time entitlements have no reset boundary, so this field has no effect. |
| `reset_min_rollover`                                                                                                                                                                                                                                                                                                                                                  | *Optional[float]*                                                                                                                                                                                                                                                                                                                                                     | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                    | Minimum balance at the entitlement's reset boundary; balances below this are floored up. Defaults to 0 (no floor). Ignored when the target entitlement has no `usagePeriod` (one-time entitlement).                                                                                                                                                                   |
| `retries`                                                                                                                                                                                                                                                                                                                                                             | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                                                                                                                      | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                    | Configuration to override the default retry behavior of the client.                                                                                                                                                                                                                                                                                                   |

### Response

**[models.PurchaseGrantResponse](../../models/purchasegrantresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404, 409                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get

Retrieve a specific grant by ID.

### Example Usage

<!-- UsageSnippet language="python" operationID="getEntitlementGrant" method="get" path="/v1/entitlements/{entitlementId}/grants/{grantId}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.entitlements.grants.get(entitlement_id="<id>", grant_id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `entitlement_id`                                                    | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the entitlement.                           |
| `grant_id`                                                          | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the grant.                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.Grant](../../models/grant.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## void

Void a grant, removing it from the customer's balance. This operation is idempotent — voiding an already-voided grant returns the voided grant without error.

### Example Usage

<!-- UsageSnippet language="python" operationID="voidEntitlementGrant" method="delete" path="/v1/entitlements/{entitlementId}/grants/{grantId}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.entitlements.grants.void(entitlement_id="<id>", grant_id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `entitlement_id`                                                    | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the entitlement.                           |
| `grant_id`                                                          | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the grant to void.                         |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.Grant](../../models/grant.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |