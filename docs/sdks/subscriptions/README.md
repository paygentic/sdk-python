# Subscriptions

## Overview

A `Subscription` is a customer's commitment to purchase a `Product` following the terms of a `Plan` and its linked `Prices`.

### Available Operations

* [list](#list) - List
* [create](#create) - Create
* [get](#get) - Get
* [update_subscription](#update_subscription) - Update
* [generate_portal_link](#generate_portal_link) - Generate Portal Link
* [terminate](#terminate) - Terminate
* [reconcile_subscription_features](#reconcile_subscription_features) - Reconcile Features
* [list_subscription_adjustments](#list_subscription_adjustments) - List Adjustments
* [create_subscription_adjustment](#create_subscription_adjustment) - Create Adjustment
* [delete_subscription_adjustment](#delete_subscription_adjustment) - Delete Adjustment

## list

List

### Example Usage

<!-- UsageSnippet language="python" operationID="listSubscriptions" method="get" path="/v0/subscriptions" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.subscriptions.list(request={})

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                   | Type                                                                        | Required                                                                    | Description                                                                 |
| --------------------------------------------------------------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| `request`                                                                   | [models.ListSubscriptionsRequest](../../models/listsubscriptionsrequest.md) | :heavy_check_mark:                                                          | The request object to use for the request.                                  |
| `retries`                                                                   | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)            | :heavy_minus_sign:                                                          | Configuration to override the default retry behavior of the client.         |

### Response

**[models.ListSubscriptionsResponse](../../models/listsubscriptionsresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## create

Creates a subscription for an existing customer or creates a new customer as part of the action.

### Example Usage

<!-- UsageSnippet language="python" operationID="createSubscription" method="post" path="/v0/subscriptions" -->
```python
import os
from paygentic_sdk import Paygentic
from paygentic_sdk.utils import parse_datetime


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.subscriptions.create(name="Monthly API Service", plan_id="plan_abc123", started_at=parse_datetime("2024-01-15T00:00:00Z"), auto_charge=False, tax_exempt=False, customer_id="cus_abc123")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                                                  | Type                                                                                                                                                                                                                                                                                       | Required                                                                                                                                                                                                                                                                                   | Description                                                                                                                                                                                                                                                                                | Example                                                                                                                                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `name`                                                                                                                                                                                                                                                                                     | *str*                                                                                                                                                                                                                                                                                      | :heavy_check_mark:                                                                                                                                                                                                                                                                         | Subscription identifier combining customer and service details. Sample values: 'TechCorp - LLM API Access', 'Analytics Co - Data Platform Enterprise', 'StartupXYZ - Image Generation Service', 'Enterprise Inc - ML Training Platform'                                                    | Monthly API Service                                                                                                                                                                                                                                                                        |
| `plan_id`                                                                                                                                                                                                                                                                                  | *str*                                                                                                                                                                                                                                                                                      | :heavy_check_mark:                                                                                                                                                                                                                                                                         | Unique identifier for a plan                                                                                                                                                                                                                                                               |                                                                                                                                                                                                                                                                                            |
| `started_at`                                                                                                                                                                                                                                                                               | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                                                                                                                       | :heavy_check_mark:                                                                                                                                                                                                                                                                         | Subscription activation timestamp in ISO 8601 format. Sample values: '2024-01-15T10:30:00Z', '2024-02-01T00:00:00Z'                                                                                                                                                                        |                                                                                                                                                                                                                                                                                            |
| `auto_charge`                                                                                                                                                                                                                                                                              | *Optional[bool]*                                                                                                                                                                                                                                                                           | :heavy_minus_sign:                                                                                                                                                                                                                                                                         | Enable automatic charging of invoices using stored payment methods. When true, invoices will be automatically paid using off-session payment. Defaults to false.                                                                                                                           |                                                                                                                                                                                                                                                                                            |
| `tax_exempt`                                                                                                                                                                                                                                                                               | *Optional[bool]*                                                                                                                                                                                                                                                                           | :heavy_minus_sign:                                                                                                                                                                                                                                                                         | When true, forces tax rate to 0%. Use for customers with verified tax-exempt status.                                                                                                                                                                                                       |                                                                                                                                                                                                                                                                                            |
| `customer`                                                                                                                                                                                                                                                                                 | [Optional[models.CreateSubscriptionCustomer]](../../models/createsubscriptioncustomer.md)                                                                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                                                                                                                         | Fields to create a new customer and consumer. Will use an existing consumer if one exists with the same email address. Required if `customerId` is not provided. Address with complete tax information (country, state, zipCode) is required for tax calculation when using Paygentic Tax. |                                                                                                                                                                                                                                                                                            |
| `customer_id`                                                                                                                                                                                                                                                                              | *Optional[str]*                                                                                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                                                                                         | Unique identifier for a customer                                                                                                                                                                                                                                                           |                                                                                                                                                                                                                                                                                            |
| `ending_at`                                                                                                                                                                                                                                                                                | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                                                                                         | Subscription expiration timestamp in ISO 8601 format. Sample values: '2024-12-31T23:59:59Z', '2025-01-15T10:30:00Z'. Omit for indefinite subscriptions.                                                                                                                                    |                                                                                                                                                                                                                                                                                            |
| `prefund_amount`                                                                                                                                                                                                                                                                           | *Optional[str]*                                                                                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                                                                                         | : warning: ** DEPRECATED **: This will be removed in a future release, please migrate away from it as soon as possible.<br/><br/>Deprecated. This field is ignored and has no effect.                                                                                                      |                                                                                                                                                                                                                                                                                            |
| `minimum_account_balance`                                                                                                                                                                                                                                                                  | *Optional[str]*                                                                                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                                                                                         | : warning: ** DEPRECATED **: This will be removed in a future release, please migrate away from it as soon as possible.<br/><br/>Deprecated. This field is ignored and has no effect.                                                                                                      |                                                                                                                                                                                                                                                                                            |
| `redirect_urls`                                                                                                                                                                                                                                                                            | [Optional[models.RedirectUrls]](../../models/redirecturls.md)                                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                                         | Optional redirect URLs after payment completion or failure. If not provided, uses default platform behavior.                                                                                                                                                                               |                                                                                                                                                                                                                                                                                            |
| `test_clock_id`                                                                                                                                                                                                                                                                            | *Optional[str]*                                                                                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                                                                                         | Test clock identifier for simulating time-based billing scenarios. Sample values: 'tc_abc123xyz', 'tc_789def456'. Restricted to non-production environments (local, dev, sandbox). Must belong to the same merchant organization.                                                          |                                                                                                                                                                                                                                                                                            |
| `renewal_reminder_enabled`                                                                                                                                                                                                                                                                 | *OptionalNullable[bool]*                                                                                                                                                                                                                                                                   | :heavy_minus_sign:                                                                                                                                                                                                                                                                         | Override plan setting for renewal reminder emails. When set, this subscription's setting takes precedence over the plan default. Set to true to enable reminders, false to disable, or null/omit to use plan default.                                                                      |                                                                                                                                                                                                                                                                                            |
| `renewal_reminder_days`                                                                                                                                                                                                                                                                    | *OptionalNullable[int]*                                                                                                                                                                                                                                                                    | :heavy_minus_sign:                                                                                                                                                                                                                                                                         | Override plan setting for number of days before renewal to send the reminder. Only used if renewalReminderEnabled is true (or inherited from plan). Set to null to use plan default.                                                                                                       |                                                                                                                                                                                                                                                                                            |
| `payment_term_days`                                                                                                                                                                                                                                                                        | *Optional[int]*                                                                                                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                                                                                         | Payment term in days ("Net X") applied to every invoice the subscription generates: invoice dueAt = invoice issue date + paymentTermDays. Defaults to 0 ("due on issue"). A non-zero value is only valid alongside bankTransferOnly=true.                                                  |                                                                                                                                                                                                                                                                                            |
| `session_expiry_minutes`                                                                                                                                                                                                                                                                   | *Optional[float]*                                                                                                                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                                                                                                                         | Number of minutes until the payment session expires. Defaults to 240 minutes (4 hours) if not provided.                                                                                                                                                                                    |                                                                                                                                                                                                                                                                                            |
| `metadata`                                                                                                                                                                                                                                                                                 | Dict[str, [models.SubscriptionMetadata](../../models/subscriptionmetadata.md)]                                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                                                                                         | Free-form merchant metadata to attach to the subscription. Values must be strings, numbers, or booleans.                                                                                                                                                                                   |                                                                                                                                                                                                                                                                                            |
| `retries`                                                                                                                                                                                                                                                                                  | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                                           | :heavy_minus_sign:                                                                                                                                                                                                                                                                         | Configuration to override the default retry behavior of the client.                                                                                                                                                                                                                        |                                                                                                                                                                                                                                                                                            |

### Response

**[models.Subscription](../../models/subscription.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404, 409           | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get

Get

### Example Usage

<!-- UsageSnippet language="python" operationID="getSubscription" method="get" path="/v0/subscriptions/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.subscriptions.get(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.Subscription](../../models/subscription.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## update_subscription

Update

### Example Usage

<!-- UsageSnippet language="python" operationID="updateSubscription" method="patch" path="/v0/subscriptions/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.subscriptions.update_subscription(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                                        | Type                                                                                                                                                                                                                                                                             | Required                                                                                                                                                                                                                                                                         | Description                                                                                                                                                                                                                                                                      |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                                                                                                                                                             | *str*                                                                                                                                                                                                                                                                            | :heavy_check_mark:                                                                                                                                                                                                                                                               | N/A                                                                                                                                                                                                                                                                              |
| `ending_at`                                                                                                                                                                                                                                                                      | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                                                                               | N/A                                                                                                                                                                                                                                                                              |
| `status`                                                                                                                                                                                                                                                                         | [Optional[models.UpdateSubscriptionStatus]](../../models/updatesubscriptionstatus.md)                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                                                                               | N/A                                                                                                                                                                                                                                                                              |
| `terminated_at`                                                                                                                                                                                                                                                                  | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                                                                               | Effective termination timestamp. Capped at the current effective time (future values are clamped). Must be strictly after the subscription's start date — values at or before startedAt are rejected with 400.                                                                   |
| `terminated_by`                                                                                                                                                                                                                                                                  | *Optional[str]*                                                                                                                                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                                                                                                               | Identifier of entity that cancelled the subscription. Sample values: 'cust_abc123' for customer-initiated cancellation, 'org_xyz789' for merchant-initiated cancellation                                                                                                         |
| `termination_reason`                                                                                                                                                                                                                                                             | *Optional[str]*                                                                                                                                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                                                                                                               | Explanation for subscription cancellation. Sample values: 'Customer requested cancellation', 'Payment failure', 'Service migration', 'Contract expiration'                                                                                                                       |
| `auto_charge`                                                                                                                                                                                                                                                                    | *Optional[bool]*                                                                                                                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                                                                                                                               | Enable or disable automatic charging of invoices using stored payment methods.                                                                                                                                                                                                   |
| `tax_exempt`                                                                                                                                                                                                                                                                     | *Optional[bool]*                                                                                                                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                                                                                                                               | When true, forces tax rate to 0%.                                                                                                                                                                                                                                                |
| `minimum_account_balance`                                                                                                                                                                                                                                                        | *Optional[str]*                                                                                                                                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                                                                                                               | : warning: ** DEPRECATED **: This will be removed in a future release, please migrate away from it as soon as possible.<br/><br/>Deprecated. This field is ignored and has no effect.                                                                                            |
| `renewal_reminder_enabled`                                                                                                                                                                                                                                                       | *OptionalNullable[bool]*                                                                                                                                                                                                                                                         | :heavy_minus_sign:                                                                                                                                                                                                                                                               | Override plan setting for renewal reminder emails. Set to true to enable, false to disable, or null to use plan default.                                                                                                                                                         |
| `renewal_reminder_days`                                                                                                                                                                                                                                                          | *OptionalNullable[int]*                                                                                                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                                                                                                               | Override plan setting for number of days before renewal to send the reminder. Set to null to use plan default.                                                                                                                                                                   |
| `payment_term_days`                                                                                                                                                                                                                                                              | *Optional[int]*                                                                                                                                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                                                                                                               | Payment term in days ("Net X") applied to subsequently generated invoices: invoice dueAt = invoice issue date + paymentTermDays. A non-zero value is only valid alongside bankTransferOnly=true. Set 0 for "due on issue". Already-issued invoices keep their snapshotted dueAt. |
| `retries`                                                                                                                                                                                                                                                                        | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                                                                                                                               | Configuration to override the default retry behavior of the client.                                                                                                                                                                                                              |

### Response

**[models.Subscription](../../models/subscription.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## generate_portal_link

Generates a secure, time-limited URL that allows customers to access their subscription data without authentication.

### Example Usage

<!-- UsageSnippet language="python" operationID="generatePortalLink" method="post" path="/v0/subscriptions/{id}/portal" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.subscriptions.generate_portal_link(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                         | Type                                                                                                                              | Required                                                                                                                          | Description                                                                                                                       |
| --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                              | *str*                                                                                                                             | :heavy_check_mark:                                                                                                                | The subscription ID                                                                                                               |
| `expires_in`                                                                                                                      | *Optional[str]*                                                                                                                   | :heavy_minus_sign:                                                                                                                | Token lifetime as an ISO 8601 duration. Defaults to PT10M (10 minutes). Maximum is P7D (7 days). Examples: PT10M, PT1H, P1D, P7D. |
| `retries`                                                                                                                         | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                  | :heavy_minus_sign:                                                                                                                | Configuration to override the default retry behavior of the client.                                                               |

### Response

**[models.SubscriptionPortal](../../models/subscriptionportal.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404, 429           | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## terminate

Terminates a subscription with a required reason. This endpoint is for merchant-initiated termination only.

### Example Usage

<!-- UsageSnippet language="python" operationID="terminateSubscription" method="post" path="/v0/subscriptions/{id}/termination" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.subscriptions.terminate(id="<id>", reason="<value>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                      | Type                                                                                                                                           | Required                                                                                                                                       | Description                                                                                                                                    |
| ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                           | *str*                                                                                                                                          | :heavy_check_mark:                                                                                                                             | The subscription ID                                                                                                                            |
| `reason`                                                                                                                                       | *str*                                                                                                                                          | :heavy_check_mark:                                                                                                                             | Cancellation explanation text. Sample values: 'Customer requested cancellation', 'Payment failure', 'Service migration', 'Contract expiration' |
| `retries`                                                                                                                                      | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                               | :heavy_minus_sign:                                                                                                                             | Configuration to override the default retry behavior of the client.                                                                            |

### Response

**[models.Subscription](../../models/subscription.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404, 409           | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## reconcile_subscription_features

Creates a reconciliation that converges a subscription's feature entitlements to its current plan. Provisions a missing entitlement (and, for metered features, its initial grant) for every plan feature the subscription does not already have; cancels the entitlement and voids the grants of any feature no longer on the plan; then synchronizes the corresponding prices' billing. An already-present feature is left unchanged. Restricted to active subscriptions billed on their plan's line-item schedule.

### Example Usage

<!-- UsageSnippet language="python" operationID="reconcileSubscriptionFeatures" method="post" path="/v0/subscriptions/{id}/reconciliations" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.subscriptions.reconcile_subscription_features(id="<id>", dry_run=False)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `id`                                                                       | *str*                                                                      | :heavy_check_mark:                                                         | The subscription ID                                                        |
| `dry_run`                                                                  | *Optional[bool]*                                                           | :heavy_minus_sign:                                                         | Preview the outcome without creating any entitlement, grant, or line item. |
| `retries`                                                                  | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)           | :heavy_minus_sign:                                                         | Configuration to override the default retry behavior of the client.        |

### Response

**[models.SubscriptionReconciliation](../../models/subscriptionreconciliation.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## list_subscription_adjustments

Reads the adjustments on the subscription, oldest window first. A subscription with no adjustment returns an empty array. Paginated, because a long-running subscription accumulates one adjustment per rate change of every deal it has carried.

### Example Usage

<!-- UsageSnippet language="python" operationID="listSubscriptionAdjustments" method="get" path="/v0/subscriptions/{id}/adjustments" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.subscriptions.list_subscription_adjustments(id="<id>", limit="10", offset="0")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The subscription ID                                                 |
| `limit`                                                             | *Optional[str]*                                                     | :heavy_minus_sign:                                                  | Number of adjustments to return                                     |
| `offset`                                                            | *Optional[str]*                                                     | :heavy_minus_sign:                                                  | Number of adjustments to skip                                       |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.SubscriptionAdjustmentsResponse](../../models/subscriptionadjustmentsresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## create_subscription_adjustment

Attaches a percentage discount to the subscription for a dated window. Every invoice calculated while the window is open carries one discount line for each discounted charge, and tax is assessed on the reduced amount. An invoice that already exists is not changed, including one still in draft — the discount reaches the periods that close after it is created. There is no update operation, and a window cannot be changed after it is created. To change a rate before any invoice has issued under the discount, delete the adjustment and create a replacement. Once an invoice has issued the adjustment is permanent, so set effectiveTo at creation time whenever the deal has a known end date.

### Example Usage

<!-- UsageSnippet language="python" operationID="createSubscriptionAdjustment" method="post" path="/v0/subscriptions/{id}/adjustments" -->
```python
import os
from paygentic_sdk import Paygentic
from paygentic_sdk.utils import parse_datetime


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.subscriptions.create_subscription_adjustment(id="<id>", type_="percentageDiscount", percentage_discount="0.35", effective_from=parse_datetime("2026-01-01T00:00:00Z"), effective_to=None, description="FY26 Growth", idempotency_key="adj_fy26_growth_001")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                                                                                     | Type                                                                                                                                                                                                                                                                                                                          | Required                                                                                                                                                                                                                                                                                                                      | Description                                                                                                                                                                                                                                                                                                                   | Example                                                                                                                                                                                                                                                                                                                       |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                                                                                                                                                                                                          | *str*                                                                                                                                                                                                                                                                                                                         | :heavy_check_mark:                                                                                                                                                                                                                                                                                                            | The subscription ID                                                                                                                                                                                                                                                                                                           |                                                                                                                                                                                                                                                                                                                               |
| `type`                                                                                                                                                                                                                                                                                                                        | [models.CreateSubscriptionAdjustmentRequestType](../../models/createsubscriptionadjustmentrequesttype.md)                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                                                                                                                            | The kind of adjustment. `percentageDiscount` reduces every discountable charge by a rate.                                                                                                                                                                                                                                     |                                                                                                                                                                                                                                                                                                                               |
| `percentage_discount`                                                                                                                                                                                                                                                                                                         | *str*                                                                                                                                                                                                                                                                                                                         | :heavy_check_mark:                                                                                                                                                                                                                                                                                                            | The discount rate as a decimal fraction between 0 and 1, sent as a string. "0.35" means 35 percent. "1" means 100 percent, not 1 percent. At most 6 decimal places. A value of 0 or above 1 is rejected.                                                                                                                      |                                                                                                                                                                                                                                                                                                                               |
| `effective_from`                                                                                                                                                                                                                                                                                                              | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                                                                                                                                                          | :heavy_check_mark:                                                                                                                                                                                                                                                                                                            | The first instant the discount applies. Inclusive.                                                                                                                                                                                                                                                                            |                                                                                                                                                                                                                                                                                                                               |
| `effective_to`                                                                                                                                                                                                                                                                                                                | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                            | The instant the discount stops applying. Exclusive, so a window ending on the same date another begins neither overlaps nor leaves a gap. Null means the discount never stops, and it cannot be ended later — set an instant whenever the deal has a known end date. Must be after effectiveFrom.                             |                                                                                                                                                                                                                                                                                                                               |
| `description`                                                                                                                                                                                                                                                                                                                 | *OptionalNullable[str]*                                                                                                                                                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                            | The deal's own name, shown on each discount line of the invoice.                                                                                                                                                                                                                                                              |                                                                                                                                                                                                                                                                                                                               |
| `idempotency_key`                                                                                                                                                                                                                                                                                                             | *Optional[str]*                                                                                                                                                                                                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                            | A key of your choosing that makes a retry safe. Sending the same key against the same subscription returns the adjustment already created and creates no second one. Without a key a retried request creates a second adjustment, and two percentage discounts compound — two of 0.35 bill 57.75 percent off, not 35 percent. | adj_fy26_growth_001                                                                                                                                                                                                                                                                                                           |
| `retries`                                                                                                                                                                                                                                                                                                                     | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                                                                              | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                            | Configuration to override the default retry behavior of the client.                                                                                                                                                                                                                                                           |                                                                                                                                                                                                                                                                                                                               |

### Response

**[models.SubscriptionAdjustment](../../models/subscriptionadjustment.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## delete_subscription_adjustment

Deletes an adjustment that has not yet reached an issued invoice. No invoice changes: an invoice still in draft keeps its numbers, and loses the discount only when its period is calculated again. An adjustment that has already discounted an issued invoice cannot be deleted, because the invoice records why the customer was charged that amount. Its window cannot be shortened afterwards either, so set effectiveTo at creation time whenever the deal has a known end date.

### Example Usage

<!-- UsageSnippet language="python" operationID="deleteSubscriptionAdjustment" method="delete" path="/v0/subscriptions/{id}/adjustments/{adjustmentId}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    paygentic.subscriptions.delete_subscription_adjustment(id="<id>", adjustment_id="<id>")

    # Use the SDK ...

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The subscription ID                                                 |
| `adjustment_id`                                                     | *str*                                                               | :heavy_check_mark:                                                  | The adjustment ID                                                   |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404, 409           | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |