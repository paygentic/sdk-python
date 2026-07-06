# BillingSchedules

## Overview

Owner-polymorphic billing schedules with intervals and staged invoice projections. A BillingSchedule belongs to exactly one Order or one Subscription (XOR). Cadence lives on ScheduleIntervals (cadence-on-the-line).

### Available Operations

* [list_billing_schedules](#list_billing_schedules) - List billing schedules
* [create_billing_schedule](#create_billing_schedule) - Create a billing schedule
* [get_billing_schedule](#get_billing_schedule) - Get a billing schedule
* [update_billing_schedule](#update_billing_schedule) - Update a billing schedule
* [delete_billing_schedule](#delete_billing_schedule) - Delete a billing schedule
* [list_schedule_intervals](#list_schedule_intervals) - List schedule intervals
* [replace_schedule_intervals](#replace_schedule_intervals) - Replace schedule intervals
* [list_schedule_invoices](#list_schedule_invoices) - List staged invoices
* [generate_schedule_invoices](#generate_schedule_invoices) - Generate staged invoices

## list_billing_schedules

List billing schedules

### Example Usage

<!-- UsageSnippet language="python" operationID="listBillingSchedules" method="get" path="/v0/billingSchedules" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billing_schedules.list_billing_schedules()

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                         | Type                                                                              | Required                                                                          | Description                                                                       |
| --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| `request`                                                                         | [models.ListBillingSchedulesRequest](../../models/listbillingschedulesrequest.md) | :heavy_check_mark:                                                                | The request object to use for the request.                                        |
| `retries`                                                                         | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                  | :heavy_minus_sign:                                                                | Configuration to override the default retry behavior of the client.               |

### Response

**[models.ListBillingSchedulesResponse](../../models/listbillingschedulesresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## create_billing_schedule

Create a billing schedule

### Example Usage

<!-- UsageSnippet language="python" operationID="createBillingSchedule" method="post" path="/v0/billingSchedules" -->
```python
import os
from paygentic_sdk import Paygentic
from paygentic_sdk.utils import parse_datetime


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billing_schedules.create_billing_schedule(start_date=parse_datetime("2025-12-16T18:30:43.578Z"), end_date=parse_datetime("2024-09-07T07:24:23.517Z"), billing_anchor=parse_datetime("2025-10-01T16:17:23.367Z"))

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                   | Type                                                                                                                        | Required                                                                                                                    | Description                                                                                                                 |
| --------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| `start_date`                                                                                                                | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                        | :heavy_check_mark:                                                                                                          | N/A                                                                                                                         |
| `end_date`                                                                                                                  | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                        | :heavy_check_mark:                                                                                                          | N/A                                                                                                                         |
| `billing_anchor`                                                                                                            | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                        | :heavy_check_mark:                                                                                                          | N/A                                                                                                                         |
| `order_id`                                                                                                                  | *Optional[str]*                                                                                                             | :heavy_minus_sign:                                                                                                          | N/A                                                                                                                         |
| `subscription_id`                                                                                                           | *Optional[str]*                                                                                                             | :heavy_minus_sign:                                                                                                          | N/A                                                                                                                         |
| `alignment_policy`                                                                                                          | [Optional[models.CreateBillingScheduleRequestAlignmentPolicy]](../../models/createbillingschedulerequestalignmentpolicy.md) | :heavy_minus_sign:                                                                                                          | N/A                                                                                                                         |
| `proration_policy`                                                                                                          | [Optional[models.CreateBillingScheduleRequestProrationPolicy]](../../models/createbillingschedulerequestprorationpolicy.md) | :heavy_minus_sign:                                                                                                          | N/A                                                                                                                         |
| `payment_term_days`                                                                                                         | *OptionalNullable[int]*                                                                                                     | :heavy_minus_sign:                                                                                                          | N/A                                                                                                                         |
| `period_preset`                                                                                                             | [Optional[models.CreateBillingScheduleRequestPeriodPreset]](../../models/createbillingschedulerequestperiodpreset.md)       | :heavy_minus_sign:                                                                                                          | N/A                                                                                                                         |
| `custom_period_windows`                                                                                                     | List[*Any*]                                                                                                                 | :heavy_minus_sign:                                                                                                          | N/A                                                                                                                         |
| `metadata`                                                                                                                  | Dict[str, *Any*]                                                                                                            | :heavy_minus_sign:                                                                                                          | N/A                                                                                                                         |
| `retries`                                                                                                                   | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                            | :heavy_minus_sign:                                                                                                          | Configuration to override the default retry behavior of the client.                                                         |

### Response

**[models.SchemasBillingSchedule](../../models/schemasbillingschedule.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404, 409           | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get_billing_schedule

Get a billing schedule

### Example Usage

<!-- UsageSnippet language="python" operationID="getBillingSchedule" method="get" path="/v0/billingSchedules/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billing_schedules.get_billing_schedule(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.SchemasBillingSchedule](../../models/schemasbillingschedule.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## update_billing_schedule

Update a billing schedule

### Example Usage

<!-- UsageSnippet language="python" operationID="updateBillingSchedule" method="patch" path="/v0/billingSchedules/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billing_schedules.update_billing_schedule(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                   | Type                                                                                                                        | Required                                                                                                                    | Description                                                                                                                 |
| --------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                        | *str*                                                                                                                       | :heavy_check_mark:                                                                                                          | N/A                                                                                                                         |
| `status`                                                                                                                    | [Optional[models.UpdateBillingScheduleRequestStatus]](../../models/updatebillingschedulerequeststatus.md)                   | :heavy_minus_sign:                                                                                                          | N/A                                                                                                                         |
| `start_date`                                                                                                                | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                        | :heavy_minus_sign:                                                                                                          | N/A                                                                                                                         |
| `end_date`                                                                                                                  | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                        | :heavy_minus_sign:                                                                                                          | N/A                                                                                                                         |
| `billing_anchor`                                                                                                            | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                        | :heavy_minus_sign:                                                                                                          | N/A                                                                                                                         |
| `alignment_policy`                                                                                                          | [Optional[models.UpdateBillingScheduleRequestAlignmentPolicy]](../../models/updatebillingschedulerequestalignmentpolicy.md) | :heavy_minus_sign:                                                                                                          | N/A                                                                                                                         |
| `proration_policy`                                                                                                          | [Optional[models.UpdateBillingScheduleRequestProrationPolicy]](../../models/updatebillingschedulerequestprorationpolicy.md) | :heavy_minus_sign:                                                                                                          | N/A                                                                                                                         |
| `payment_term_days`                                                                                                         | *OptionalNullable[int]*                                                                                                     | :heavy_minus_sign:                                                                                                          | N/A                                                                                                                         |
| `period_preset`                                                                                                             | [Optional[models.UpdateBillingScheduleRequestPeriodPreset]](../../models/updatebillingschedulerequestperiodpreset.md)       | :heavy_minus_sign:                                                                                                          | N/A                                                                                                                         |
| `custom_period_windows`                                                                                                     | List[*Any*]                                                                                                                 | :heavy_minus_sign:                                                                                                          | N/A                                                                                                                         |
| `metadata`                                                                                                                  | Dict[str, *Any*]                                                                                                            | :heavy_minus_sign:                                                                                                          | N/A                                                                                                                         |
| `retries`                                                                                                                   | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                            | :heavy_minus_sign:                                                                                                          | Configuration to override the default retry behavior of the client.                                                         |

### Response

**[models.SchemasBillingSchedule](../../models/schemasbillingschedule.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404, 409           | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## delete_billing_schedule

Delete a billing schedule

### Example Usage

<!-- UsageSnippet language="python" operationID="deleteBillingSchedule" method="delete" path="/v0/billingSchedules/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    paygentic.billing_schedules.delete_billing_schedule(id="<id>")

    # Use the SDK ...

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## list_schedule_intervals

List schedule intervals

### Example Usage

<!-- UsageSnippet language="python" operationID="listScheduleIntervals" method="get" path="/v0/billingSchedules/{id}/intervals" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billing_schedules.list_schedule_intervals(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.ListScheduleIntervalsResponse](../../models/listscheduleintervalsresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## replace_schedule_intervals

Replace (PUT semantics) the full interval set for a schedule. Wipes existing intervals and recreates from the supplied list. Reverts any in-flight order approval for order-owned schedules.

### Example Usage

<!-- UsageSnippet language="python" operationID="replaceScheduleIntervals" method="put" path="/v0/billingSchedules/{id}/intervals" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billing_schedules.replace_schedule_intervals(id="<id>", intervals=[])

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                        | Type                                                                             | Required                                                                         | Description                                                                      |
| -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `id`                                                                             | *str*                                                                            | :heavy_check_mark:                                                               | N/A                                                                              |
| `intervals`                                                                      | List[[models.Interval](../../models/interval.md)]                                | :heavy_check_mark:                                                               | N/A                                                                              |
| `order_line_item_id`                                                             | *Optional[str]*                                                                  | :heavy_minus_sign:                                                               | When set, scope the wipe to this line's intervals only (per-line cell-edit path) |
| `retries`                                                                        | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                 | :heavy_minus_sign:                                                               | Configuration to override the default retry behavior of the client.              |

### Response

**[models.ReplaceScheduleIntervalsResponse](../../models/replacescheduleintervalsresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404, 409           | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## list_schedule_invoices

List the staged invoice projections for a schedule, newest period first.

### Example Usage

<!-- UsageSnippet language="python" operationID="listScheduleInvoices" method="get" path="/v0/billingSchedules/{id}/invoices" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billing_schedules.list_schedule_invoices(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.ListScheduleInvoicesResponse](../../models/listscheduleinvoicesresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## generate_schedule_invoices

Generate (or regenerate) staged invoice projections for a schedule from its current intervals. Idempotent — replaces any existing staged rows. Schedule must have at least one interval.

### Example Usage

<!-- UsageSnippet language="python" operationID="generateScheduleInvoices" method="post" path="/v0/billingSchedules/{id}/invoices" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billing_schedules.generate_schedule_invoices(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.GenerateScheduleInvoicesResponse](../../models/generatescheduleinvoicesresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404, 409           | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |