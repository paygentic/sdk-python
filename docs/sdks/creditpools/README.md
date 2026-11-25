# CreditPools

## Overview

A `CreditPool` is the `(customer, pricingUnit)` identity that credit-denominated prices draw down. The balance itself lives on grants, not on the pool; the pool survives subscription changes. There is one pool per `(customer, pricingUnit)`.

### Available Operations

* [create_credit_pool](#create_credit_pool) - Create or resolve
* [list_credit_pools](#list_credit_pools) - List
* [get_credit_pool](#get_credit_pool) - Get
* [list_credit_pool_grants](#list_credit_pool_grants) - List grants
* [create_credit_pool_grant](#create_credit_pool_grant) - Grant credits
* [get_credit_pool_ledger](#get_credit_pool_ledger) - Get ledger
* [create_credit_pool_purchase](#create_credit_pool_purchase) - Purchase credits

## create_credit_pool

Resolve-or-create the credit pool for a `(customer, pricingUnit)` pair. Idempotent: returns `201` with a newly created pool, or `200` with the existing pool. Works with no subscription.

### Example Usage

<!-- UsageSnippet language="python" operationID="createCreditPool" method="post" path="/v0/creditPools" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.credit_pools.create_credit_pool(customer_id="<id>", pricing_unit_id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `customer_id`                                                       | *str*                                                               | :heavy_check_mark:                                                  | Unique identifier for a customer                                    |
| `pricing_unit_id`                                                   | *str*                                                               | :heavy_check_mark:                                                  | Unique identifier for a pricing unit                                |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.CreditPool](../../models/creditpool.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## list_credit_pools

List

### Example Usage

<!-- UsageSnippet language="python" operationID="listCreditPools" method="get" path="/v0/creditPools" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.credit_pools.list_credit_pools(request={})

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                               | Type                                                                    | Required                                                                | Description                                                             |
| ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `request`                                                               | [models.ListCreditPoolsRequest](../../models/listcreditpoolsrequest.md) | :heavy_check_mark:                                                      | The request object to use for the request.                              |
| `retries`                                                               | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)        | :heavy_minus_sign:                                                      | Configuration to override the default retry behavior of the client.     |

### Response

**[models.ListCreditPoolsResponse](../../models/listcreditpoolsresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get_credit_pool

Get

### Example Usage

<!-- UsageSnippet language="python" operationID="getCreditPool" method="get" path="/v0/creditPools/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.credit_pools.get_credit_pool(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.CreditPool](../../models/creditpool.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## list_credit_pool_grants

Lists the grants on the pool, with the credits left on each. Active and scheduled grants come first, in the order they are spent: lowest priority first, then soonest expiry (no expiry last), then oldest. Expired and voided grants come after, newest first. `remainingBalance` is the grant's balance from the same replay the ledger runs, computed at read time from the usage so far. It is 0 unless the grant is active. Statuses and balances are computed at one instant, returned as `asOf`. It defaults to the pool's current time: the test clock time of the customer's newest active subscription if it has one, otherwise now. A later `at` is read as the pool's current time. Pass `at` to read at a different instant.

### Example Usage

<!-- UsageSnippet language="python" operationID="listCreditPoolGrants" method="get" path="/v0/creditPools/{id}/grants" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.credit_pools.list_credit_pool_grants(id="<id>", limit=50, offset=0)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                | Type                                                                                                                                                                                                                                     | Required                                                                                                                                                                                                                                 | Description                                                                                                                                                                                                                              |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                                                                                                                     | *str*                                                                                                                                                                                                                                    | :heavy_check_mark:                                                                                                                                                                                                                       | N/A                                                                                                                                                                                                                                      |
| `status`                                                                                                                                                                                                                                 | [Optional[models.CreditPoolGrantStatus]](../../models/creditpoolgrantstatus.md)                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                                                                       | Return only grants with this status.                                                                                                                                                                                                     |
| `limit`                                                                                                                                                                                                                                  | *Optional[int]*                                                                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                                                                       | Maximum grants to return.                                                                                                                                                                                                                |
| `offset`                                                                                                                                                                                                                                 | *Optional[int]*                                                                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                                                                       | Zero-based offset for pagination.                                                                                                                                                                                                        |
| `at`                                                                                                                                                                                                                                     | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                                                                     | :heavy_minus_sign:                                                                                                                                                                                                                       | The instant to compute statuses and balances at. Defaults to the pool's current time: the test clock time of the customer's newest active subscription if it has one, otherwise now. A later instant is read as the pool's current time. |
| `retries`                                                                                                                                                                                                                                | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                         | :heavy_minus_sign:                                                                                                                                                                                                                       | Configuration to override the default retry behavior of the client.                                                                                                                                                                      |

### Response

**[models.CreditPoolGrantList](../../models/creditpoolgrantlist.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## create_credit_pool_grant

Mint a credit grant on the pool. Set `recurrencePeriod` (+ optional `recurrenceAnchor`, defaults to `effectiveAt`) for a recurring grant that re-adds `amount` each interval; set `expiresAt` for a per-grant expiry. Standalone of any plan or subscription.

### Example Usage

<!-- UsageSnippet language="python" operationID="createCreditPoolGrant" method="post" path="/v0/creditPools/{id}/grants" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.credit_pools.create_credit_pool_grant(id="<id>", amount=5717.01)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                 | Type                                                                                                      | Required                                                                                                  | Description                                                                                               |
| --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                      | *str*                                                                                                     | :heavy_check_mark:                                                                                        | N/A                                                                                                       |
| `amount`                                                                                                  | *float*                                                                                                   | :heavy_check_mark:                                                                                        | Credits to allocate (in the pool's pricing unit).                                                         |
| `priority`                                                                                                | *Optional[int]*                                                                                           | :heavy_minus_sign:                                                                                        | Drawdown priority (lower = consumed first). Defaults to 0.                                                |
| `effective_at`                                                                                            | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                      | :heavy_minus_sign:                                                                                        | When the block becomes active. Defaults to now (or the customer's active-subscription test-clock time).   |
| `recurrence_period`                                                                                       | *Optional[str]*                                                                                           | :heavy_minus_sign:                                                                                        | ISO-8601 duration (e.g. `P1M`). When set, `amount` is re-added each interval within the block's envelope. |
| `recurrence_anchor`                                                                                       | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                      | :heavy_minus_sign:                                                                                        | Recurrence phase anchor. Defaults to `effectiveAt`. Only valid with `recurrencePeriod`.                   |
| `expires_at`                                                                                              | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                      | :heavy_minus_sign:                                                                                        | When the block expires (per-block expiry).                                                                |
| `idempotency_key`                                                                                         | *Optional[str]*                                                                                           | :heavy_minus_sign:                                                                                        | Idempotency key; a repeat with the same key returns the existing grant.                                   |
| `retries`                                                                                                 | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                          | :heavy_minus_sign:                                                                                        | Configuration to override the default retry behavior of the client.                                       |

### Response

**[models.CreditPoolGrant](../../models/creditpoolgrant.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404, 409           | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get_credit_pool_ledger

Returns a chronologically-ordered ledger of the pool's balance history within a required time window: `increment` (a grant funded the pool, including recurrence refills), `decrement` (usage drawdown), `void` (a grant was cancelled early), and `expiration` (a grant's unused balance lapsed at expiry). Each entry carries the pool's running balance immediately before and after it, and the response reports the window's boundary balances at the top level. Pass `granularity` to receive calendar-aligned buckets instead of itemized entries. There is no full-history view in a single call — page through successive windows to see a pool's complete history.

### Example Usage

<!-- UsageSnippet language="python" operationID="getCreditPoolLedger" method="get" path="/v0/creditPools/{id}/ledger" -->
```python
import os
from paygentic_sdk import Paygentic
from paygentic_sdk.utils import parse_datetime


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.credit_pools.get_credit_pool_ledger(id="<id>", from_=parse_datetime("2025-01-03T19:47:34.571Z"), to=parse_datetime("2025-06-15T09:32:08.085Z"), limit=50, offset=0)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                                                                                                                                                | Type                                                                                                                                                                                                                                                                                                                                                                                     | Required                                                                                                                                                                                                                                                                                                                                                                                 | Description                                                                                                                                                                                                                                                                                                                                                                              |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                                                                                                                                                                                                                                                                     | *str*                                                                                                                                                                                                                                                                                                                                                                                    | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                                                       | N/A                                                                                                                                                                                                                                                                                                                                                                                      |
| `from_`                                                                                                                                                                                                                                                                                                                                                                                  | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                                                       | Start of the requested window (inclusive). Required — this endpoint has no full-lifetime view. Must be before the pool's current time: the test clock time of the customer's newest active subscription if it has one, otherwise now.                                                                                                                                                    |
| `to`                                                                                                                                                                                                                                                                                                                                                                                     | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                                                       | End of the requested window. Must be strictly after `from`. The window is capped at a maximum supported span; a wider request is rejected. A `to` after the pool's current time is read as the current time, so the ledger never includes projected refills or expirations.                                                                                                              |
| `entry_type`                                                                                                                                                                                                                                                                                                                                                                             | [Optional[models.GetCreditPoolLedgerEntryType]](../../models/getcreditpoolledgerentrytype.md)                                                                                                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                       | Restrict the response to a single entry type: `increment` (grant funding, including recurrence refills), `decrement` (usage drawdown), `void` (early grant termination), or `expiration` (unused balance lapsing at a grant's expiry). When `granularity` is also set, this filter scopes which entries feed each bucket's net fields and `entryCount`, but never the reported balances. |
| `granularity`                                                                                                                                                                                                                                                                                                                                                                            | [Optional[models.Granularity]](../../models/granularity.md)                                                                                                                                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                       | Roll the ledger up into calendar-aligned buckets (UTC) instead of itemized entries. Calendar periods with no activity are omitted from the response. To see the individual entries behind a bucket, request the itemized ledger (omit `granularity`) with the same `entryType` filter and `from`/`to` narrowed to that bucket's `period`.                                                |
| `limit`                                                                                                                                                                                                                                                                                                                                                                                  | *Optional[int]*                                                                                                                                                                                                                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                       | Maximum number of entries (or buckets, when `granularity` is set) to return.                                                                                                                                                                                                                                                                                                             |
| `offset`                                                                                                                                                                                                                                                                                                                                                                                 | *Optional[int]*                                                                                                                                                                                                                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                       | Zero-based offset for pagination.                                                                                                                                                                                                                                                                                                                                                        |
| `retries`                                                                                                                                                                                                                                                                                                                                                                                | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                                                                                                                                         | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                       | Configuration to override the default retry behavior of the client.                                                                                                                                                                                                                                                                                                                      |

### Response

**[models.GetCreditPoolLedgerResponse](../../models/getcreditpoolledgerresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## create_credit_pool_purchase

Create a grant-purchase invoice for the pool's customer and advance it to a payment session. Price is server-derived from the pricing unit's conversion rate — the caller never supplies a price. On successful payment, the existing billing-worker settlement path mints the purchased credits as a grant on the pool; this endpoint does not mint the grant itself.

### Example Usage

<!-- UsageSnippet language="python" operationID="createCreditPoolPurchase" method="post" path="/v0/creditPools/{id}/purchase" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.credit_pools.create_credit_pool_purchase(id="<id>", grant_amount=5185.68, idempotency_key="<value>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                           | Type                                                                                                                                | Required                                                                                                                            | Description                                                                                                                         |
| ----------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                | *str*                                                                                                                               | :heavy_check_mark:                                                                                                                  | N/A                                                                                                                                 |
| `grant_amount`                                                                                                                      | *float*                                                                                                                             | :heavy_check_mark:                                                                                                                  | The number of credits to grant upon payment completion.                                                                             |
| `idempotency_key`                                                                                                                   | *str*                                                                                                                               | :heavy_check_mark:                                                                                                                  | Caller-provided deduplication key. Retrying with the same key returns the existing invoice.                                         |
| `subscription_id`                                                                                                                   | *Optional[str]*                                                                                                                     | :heavy_minus_sign:                                                                                                                  | The subscription to anchor the invoice to. Required to disambiguate when the pool's customer has more than one active subscription. |
| `effective_at`                                                                                                                      | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                | :heavy_minus_sign:                                                                                                                  | When the grant becomes effective. Defaults to now.                                                                                  |
| `expires_at`                                                                                                                        | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                | :heavy_minus_sign:                                                                                                                  | When the grant expires. If omitted, the grant does not expire.                                                                      |
| `success_url`                                                                                                                       | *Optional[str]*                                                                                                                     | :heavy_minus_sign:                                                                                                                  | URL to redirect the customer to after successful payment.                                                                           |
| `cancel_url`                                                                                                                        | *Optional[str]*                                                                                                                     | :heavy_minus_sign:                                                                                                                  | URL to redirect the customer to if payment is cancelled.                                                                            |
| `payment_expires_at`                                                                                                                | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                | :heavy_minus_sign:                                                                                                                  | When the payment session expires. If omitted, uses the default expiry.                                                              |
| `retries`                                                                                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                    | :heavy_minus_sign:                                                                                                                  | Configuration to override the default retry behavior of the client.                                                                 |

### Response

**[models.CreateCreditPoolPurchaseResponse](../../models/createcreditpoolpurchaseresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404, 409           | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |