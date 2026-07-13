# paygentic-sdk

The official Python SDK for the [Paygentic API](https://paygentic.io) — build billing, subscriptions, and usage-based monetization into your product.

[![Built by Speakeasy](https://img.shields.io/badge/Built_by-SPEAKEASY-374151?style=for-the-badge&labelColor=f3f4f6)](https://www.speakeasy.com/?utm_source=paygentic-sdk&utm_campaign=python)
[![License: MIT](https://img.shields.io/badge/LICENSE_//_MIT-3b5bdb?style=for-the-badge&labelColor=eff6ff)](https://opensource.org/licenses/MIT)


<br /><br />
<!-- Start Summary [summary] -->
## Summary

Paygentic API: The Paygentic API provides billing infrastructure for usage-based and subscription monetization — customers, subscriptions, usage metering, invoicing, entitlements, and payments.

See the [Quickstart](https://docs.paygentic.io/getting-started/quickstart) to go from zero to billing in a handful of steps.
<!-- End Summary [summary] -->

## How it works

Paygentic models your billing around five connected concepts:

| Concept | What it is |
|---------|------------|
| **Product** | The service you sell (e.g., "LLM Inference Engine") |
| **Plan** | A subscribable package with pricing, billing interval, and currency |
| **Customer** | An organization you bill, connected to a Plan via a Subscription |
| **Subscription** | Ties a Customer to a Plan; activates once any upfront invoice is paid |
| **Meter Events** | Fire-and-forget events that record consumption for metered billing |

Typical flow: define a Product → configure a Plan → create a Customer → create a Subscription → send Meter Events → Paygentic handles invoicing automatically.

See the [Quickstart](https://docs.paygentic.io/getting-started/quickstart) for a step-by-step walkthrough.

<!-- Start Table of Contents [toc] -->
## Table of Contents
<!-- $toc-max-depth=2 -->
* [paygentic-sdk](https://github.com/paygentic/sdk-python/blob/master/#paygentic-sdk)
  * [How it works](https://github.com/paygentic/sdk-python/blob/master/#how-it-works)
  * [SDK Installation](https://github.com/paygentic/sdk-python/blob/master/#sdk-installation)
  * [IDE Support](https://github.com/paygentic/sdk-python/blob/master/#ide-support)
  * [SDK Example Usage](https://github.com/paygentic/sdk-python/blob/master/#sdk-example-usage)
  * [Authentication](https://github.com/paygentic/sdk-python/blob/master/#authentication)
  * [Available Resources and Operations](https://github.com/paygentic/sdk-python/blob/master/#available-resources-and-operations)
  * [Retries](https://github.com/paygentic/sdk-python/blob/master/#retries)
  * [Error Handling](https://github.com/paygentic/sdk-python/blob/master/#error-handling)
  * [Server Selection](https://github.com/paygentic/sdk-python/blob/master/#server-selection)
  * [Custom HTTP Client](https://github.com/paygentic/sdk-python/blob/master/#custom-http-client)
  * [Resource Management](https://github.com/paygentic/sdk-python/blob/master/#resource-management)
  * [Debugging](https://github.com/paygentic/sdk-python/blob/master/#debugging)
* [Development](https://github.com/paygentic/sdk-python/blob/master/#development)
  * [Maturity](https://github.com/paygentic/sdk-python/blob/master/#maturity)
  * [Contributions](https://github.com/paygentic/sdk-python/blob/master/#contributions)

<!-- End Table of Contents [toc] -->

<!-- Start SDK Installation [installation] -->
## SDK Installation

> [!NOTE]
> **Python version upgrade policy**
>
> Once a Python version reaches its [official end of life date](https://devguide.python.org/versions/), a 3-month grace period is provided for users to upgrade. Following this grace period, the minimum python version supported in the SDK will be updated.

The SDK can be installed with *uv*, *pip*, or *poetry* package managers.

### uv

*uv* is a fast Python package installer and resolver, designed as a drop-in replacement for pip and pip-tools. It's recommended for its speed and modern Python tooling capabilities.

```bash
uv add paygentic-sdk
```

### PIP

*PIP* is the default package installer for Python, enabling easy installation and management of packages from PyPI via the command line.

```bash
pip install paygentic-sdk
```

### Poetry

*Poetry* is a modern tool that simplifies dependency management and package publishing by using a single `pyproject.toml` file to handle project metadata and dependencies.

```bash
poetry add paygentic-sdk
```

### Shell and script usage with `uv`

You can use this SDK in a Python shell with [uv](https://docs.astral.sh/uv/) and the `uvx` command that comes with it like so:

```shell
uvx --from paygentic-sdk python
```

It's also possible to write a standalone Python script without needing to set up a whole project like so:

```python
#!/usr/bin/env -S uv run --script
# /// script
# requires-python = ">=3.10"
# dependencies = [
#     "paygentic-sdk",
# ]
# ///

from paygentic_sdk import Paygentic

sdk = Paygentic(
  # SDK arguments
)

# Rest of script here...
```

Once that is saved to a file, you can run it with `uv run script.py` where
`script.py` can be replaced with the actual file name.
<!-- End SDK Installation [installation] -->

<!-- Start IDE Support [idesupport] -->
## IDE Support

### PyCharm

Generally, the SDK will work well with most IDEs out of the box. However, when using PyCharm, you can enjoy much better integration with Pydantic by installing an additional plugin.

- [PyCharm Pydantic Plugin](https://docs.pydantic.dev/latest/integrations/pycharm/)
<!-- End IDE Support [idesupport] -->

<!-- Start SDK Example Usage [usage] -->
## SDK Example Usage

### Create a customer

Create a customer for each organization you bill. This is the first step in the billing setup — see the [Quickstart](https://docs.paygentic.io/getting-started/quickstart) for the full flow.

```python
# Synchronous Example
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

</br>

The same SDK client can also be used to make asynchronous requests by importing asyncio.

```python
# Asynchronous Example
import asyncio
import os
from paygentic_sdk import Paygentic

async def main():

    async with Paygentic(
        bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
    ) as paygentic:

        res = await paygentic.customers.create_async(merchant_id="org_YS8jkP59V71TdUvj", consumer={
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

asyncio.run(main())
```

### Create a subscription

Subscribe a customer to a plan. If the plan includes in-advance charges, Paygentic generates an initial invoice and the subscription activates once paid.

```python
# Synchronous Example
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

</br>

The same SDK client can also be used to make asynchronous requests by importing asyncio.

```python
# Asynchronous Example
import asyncio
import os
from paygentic_sdk import Paygentic
from paygentic_sdk.utils import parse_datetime

async def main():

    async with Paygentic(
        bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
    ) as paygentic:

        res = await paygentic.subscriptions.create_async(name="Monthly API Service", plan_id="plan_abc123", started_at=parse_datetime("2024-01-15T00:00:00Z"), auto_charge=False, tax_exempt=False, customer_id="cus_abc123")

        # Handle response
        print(res)

asyncio.run(main())
```

### Report usage

Send meter events to record consumption once a subscription is active. The endpoint is fire-and-forget — it always returns `202 Accepted`.

```python
# Synchronous Example
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.events.ingest(type_="ai.inference", source="https://api.myapp.com", subject="cus_abc123", data={
        "tokens": 1500,
        "model": "gpt-4o",
    })

    # Handle response
    print(res)
```

</br>

The same SDK client can also be used to make asynchronous requests by importing asyncio.

```python
# Asynchronous Example
import asyncio
import os
from paygentic_sdk import Paygentic

async def main():

    async with Paygentic(
        bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
    ) as paygentic:

        res = await paygentic.events.ingest_async(type_="ai.inference", source="https://api.myapp.com", subject="cus_abc123", data={
            "tokens": 1500,
            "model": "gpt-4o",
        })

        # Handle response
        print(res)

asyncio.run(main())
```
<!-- End SDK Example Usage [usage] -->

<!-- Start Authentication [security] -->
## Authentication

### Per-Client Security Schemes

This SDK supports the following security scheme globally:

| Name          | Type | Scheme      | Environment Variable    |
| ------------- | ---- | ----------- | ----------------------- |
| `bearer_auth` | http | HTTP Bearer | `PAYGENTIC_BEARER_AUTH` |

To authenticate with the API the `bearer_auth` parameter must be set when initializing the SDK client instance. For example:
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billable_metrics.create(aggregation="SUM", description="Tracks total tokens consumed per API call.", merchant_id="org_YS8jkP59V71TdUvj", name="Token Counter", product_id="prod_abc123", unit="tokens")

    # Handle response
    print(res)

```
<!-- End Authentication [security] -->

<!-- Start Available Resources and Operations [operations] -->
## Available Resources and Operations

<details open>
<summary>Available methods</summary>

### [Approvals](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/approvals/README.md)

* [create_approval](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/approvals/README.md#create_approval) - Submit a resource for approval
* [list_approvals](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/approvals/README.md#list_approvals) - List approvals
* [get_approval](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/approvals/README.md#get_approval) - Get an approval
* [update_approval](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/approvals/README.md#update_approval) - Update an approval (approve, reject, or cancel)

### [BillableMetrics](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/billablemetrics/README.md)

* [create](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/billablemetrics/README.md#create) - Create
* [list](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/billablemetrics/README.md#list) - List
* [get](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/billablemetrics/README.md#get) - Get
* [update](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/billablemetrics/README.md#update) - Update
* [meter](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/billablemetrics/README.md#meter) - Query Meter Usage
* [list_events](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/billablemetrics/README.md#list_events) - List Meter Events

### [BillingSchedules](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/billingschedules/README.md)

* [list_billing_schedules](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/billingschedules/README.md#list_billing_schedules) - List billing schedules
* [create_billing_schedule](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/billingschedules/README.md#create_billing_schedule) - Create a billing schedule
* [get_billing_schedule](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/billingschedules/README.md#get_billing_schedule) - Get a billing schedule
* [update_billing_schedule](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/billingschedules/README.md#update_billing_schedule) - Update a billing schedule
* [delete_billing_schedule](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/billingschedules/README.md#delete_billing_schedule) - Delete a billing schedule
* [list_schedule_intervals](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/billingschedules/README.md#list_schedule_intervals) - List schedule intervals
* [replace_schedule_intervals](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/billingschedules/README.md#replace_schedule_intervals) - Replace schedule intervals
* [list_schedule_invoices](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/billingschedules/README.md#list_schedule_invoices) - List staged invoices
* [generate_schedule_invoices](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/billingschedules/README.md#generate_schedule_invoices) - Generate staged invoices

### [Costs](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/costs/README.md)

* [create_cost](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/costs/README.md#create_cost) - Create
* [list_costs](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/costs/README.md#list_costs) - List
* [get_cost](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/costs/README.md#get_cost) - Get
* [update_cost](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/costs/README.md#update_cost) - Update
* [delete_cost](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/costs/README.md#delete_cost) - Delete
* [get_cost_summary](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/costs/README.md#get_cost_summary) - Query Summary
* [get_cost_report](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/costs/README.md#get_cost_report) - Report

### [Customers](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/customers/README.md)

* [list](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/customers/README.md#list) - List by Merchant
* [create](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/customers/README.md#create) - Create
* [get](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/customers/README.md#get) - Get
* [delete](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/customers/README.md#delete) - Delete
* [update](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/customers/README.md#update) - Update
* [list_customer_payment_methods](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/customers/README.md#list_customer_payment_methods) - List payment methods
* [create_customer_payment_method](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/customers/README.md#create_customer_payment_method) - Set up a payment method

### [Entitlements](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/entitlements/README.md)

* [list](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/entitlements/README.md#list) - List Entitlements
* [issue](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/entitlements/README.md#issue) - Issue Entitlement
* [get](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/entitlements/README.md#get) - Get Entitlement

### [Entitlements.Grants](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/grants/README.md)

* [list](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/grants/README.md#list) - List Grants
* [create](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/grants/README.md#create) - Create Grant
* [purchase](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/grants/README.md#purchase) - Purchase Grant
* [get](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/grants/README.md#get) - Get Grant
* [void](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/grants/README.md#void) - Void Grant

### [Events](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/events/README.md)

* [ingest](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/events/README.md#ingest) - Ingest Event

### [ExternalReferences](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/externalreferences/README.md)

* [create_external_reference](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/externalreferences/README.md#create_external_reference) - Create
* [list_external_references](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/externalreferences/README.md#list_external_references) - List
* [get_external_reference](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/externalreferences/README.md#get_external_reference) - Get
* [update_external_reference](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/externalreferences/README.md#update_external_reference) - Update
* [delete_external_reference](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/externalreferences/README.md#delete_external_reference) - Delete

### [Features](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/featuressdk/README.md)

* [list](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/featuressdk/README.md#list) - List
* [create](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/featuressdk/README.md#create) - Create
* [get](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/featuressdk/README.md#get) - Get
* [update](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/featuressdk/README.md#update) - Update
* [delete](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/featuressdk/README.md#delete) - Delete

### [Fees](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/fees/README.md)

* [create](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/fees/README.md#create) - Create
* [list](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/fees/README.md#list) - List
* [get](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/fees/README.md#get) - Get
* [update](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/fees/README.md#update) - Update
* [delete](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/fees/README.md#delete) - Delete
* [get_price](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/fees/README.md#get_price) - Get Fee Price

### [InvoicesV2](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/invoicesv2/README.md)

* [list](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/invoicesv2/README.md#list) - List
* [list_line_items](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/invoicesv2/README.md#list_line_items) - List Line Items
* [create_line_item](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/invoicesv2/README.md#create_line_item) - Create Manual Line Item
* [get](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/invoicesv2/README.md#get) - Get
* [get_line_items](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/invoicesv2/README.md#get_line_items) - Get Line Items
* [create_invoice_refund](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/invoicesv2/README.md#create_invoice_refund) - Refund Invoice
* [list_invoice_refunds](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/invoicesv2/README.md#list_invoice_refunds) - List Invoice Refunds
* [void_invoice_refund](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/invoicesv2/README.md#void_invoice_refund) - Void Invoice Refund

### [Items](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/items/README.md)

* [create_item](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/items/README.md#create_item) - Create
* [list_items](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/items/README.md#list_items) - List
* [get_item](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/items/README.md#get_item) - Get
* [update_item](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/items/README.md#update_item) - Update
* [delete_item](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/items/README.md#delete_item) - Delete

### [MerchantIntegrations](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/merchantintegrations/README.md)

* [list_merchant_integrations](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/merchantintegrations/README.md#list_merchant_integrations) - List
* [upsert_merchant_integration](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/merchantintegrations/README.md#upsert_merchant_integration) - Upsert
* [get_merchant_integration](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/merchantintegrations/README.md#get_merchant_integration) - Get
* [disconnect_merchant_integration](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/merchantintegrations/README.md#disconnect_merchant_integration) - Disconnect

### [Orders](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/orders/README.md)

* [create_order](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/orders/README.md#create_order) - Create an order
* [list_orders](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/orders/README.md#list_orders) - List orders
* [get_order](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/orders/README.md#get_order) - Get an order
* [update_order](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/orders/README.md#update_order) - Update an order
* [delete_order](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/orders/README.md#delete_order) - Delete an order
* [create_order_line_item](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/orders/README.md#create_order_line_item) - Add a line item
* [update_order_line_item](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/orders/README.md#update_order_line_item) - Update a line item
* [delete_order_line_item](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/orders/README.md#delete_order_line_item) - Delete a line item
* [create_order_approval](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/orders/README.md#create_order_approval) - Create an approval for the order

### [PaymentSessions](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/paymentsessions/README.md)

* [list_payment_sessions](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/paymentsessions/README.md#list_payment_sessions) - List

### [Payments](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/payments/README.md)

* [list](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/payments/README.md#list) - List Payments
* [create](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/payments/README.md#create) - Create Payment
* [get](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/payments/README.md#get) - Get Payment

### [Plans](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/plans/README.md)

* [create](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/plans/README.md#create) - Create
* [list](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/plans/README.md#list) - List
* [list_available](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/plans/README.md#list_available) - List Available Plans
* [get](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/plans/README.md#get) - Get
* [update](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/plans/README.md#update) - Update

### [Prices](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/prices/README.md)

* [create](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/prices/README.md#create) - Create
* [list](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/prices/README.md#list) - List
* [get](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/prices/README.md#get) - Get
* [update](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/prices/README.md#update) - Update
* [delete](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/prices/README.md#delete) - Delete

### [Products](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/products/README.md)

* [create](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/products/README.md#create) - Create
* [list](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/products/README.md#list) - List
* [get](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/products/README.md#get) - Get
* [update](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/products/README.md#update) - Update

### [Profitability](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/profitability/README.md)

* [get_profitability](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/profitability/README.md#get_profitability) - Get profitability summary

### [Revenue](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/revenue/README.md)

* [get](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/revenue/README.md#get) - Get revenue summary

### [Salesforce](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/salesforce/README.md)

* [list_salesforce_accounts](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/salesforce/README.md#list_salesforce_accounts) - List Salesforce accounts

### [Sources](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/sources/README.md)

* [create](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/sources/README.md#create) - Create
* [list](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/sources/README.md#list) - List
* [get](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/sources/README.md#get) - Get
* [update](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/sources/README.md#update) - Update

### [Sources.Events](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/sourcesevents/README.md)

* [list](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/sourcesevents/README.md#list) - List Events
* [approve](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/sourcesevents/README.md#approve) - Approve
* [reject](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/sourcesevents/README.md#reject) - Reject
* [bulk_approve](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/sourcesevents/README.md#bulk_approve) - Bulk Approve
* [bulk_reject](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/sourcesevents/README.md#bulk_reject) - Bulk Reject

### [Sources.Rules](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/rules/README.md)

* [list](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/rules/README.md#list) - List Rules
* [create](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/rules/README.md#create) - Create Rule
* [get](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/rules/README.md#get) - Get Rule
* [update](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/rules/README.md#update) - Update Rule
* [delete](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/rules/README.md#delete) - Delete Rule

### [Subscriptions](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/subscriptions/README.md)

* [list](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/subscriptions/README.md#list) - List
* [create](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/subscriptions/README.md#create) - Create
* [get](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/subscriptions/README.md#get) - Get
* [update_subscription](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/subscriptions/README.md#update_subscription) - Update
* [generate_portal_link](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/subscriptions/README.md#generate_portal_link) - Generate Portal Link
* [terminate](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/subscriptions/README.md#terminate) - Terminate
* [reconcile_subscription_features](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/subscriptions/README.md#reconcile_subscription_features) - Reconcile Features

### [TestClocks](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/testclocks/README.md)

* [list](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/testclocks/README.md#list) - List
* [create](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/testclocks/README.md#create) - Create
* [get](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/testclocks/README.md#get) - Get
* [advance](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/testclocks/README.md#advance) - Advance
* [delete](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/testclocks/README.md#delete) - Delete

### [Users](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/users/README.md)

* [get](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/users/README.md#get) - Get
* [update](https://github.com/paygentic/sdk-python/blob/master/docs/sdks/users/README.md#update) - Update

</details>
<!-- End Available Resources and Operations [operations] -->

<!-- Start Retries [retries] -->
## Retries

Some of the endpoints in this SDK support retries. If you use the SDK without any configuration, it will fall back to the default retry strategy provided by the API. However, the default retry strategy can be overridden on a per-operation basis, or across the entire SDK.

To change the default retry strategy for a single API call, simply provide a `RetryConfig` object to the call:
```python
import os
from paygentic_sdk import Paygentic
from paygentic_sdk.utils import BackoffStrategy, RetryConfig


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billable_metrics.create(aggregation="SUM", description="Tracks total tokens consumed per API call.", merchant_id="org_YS8jkP59V71TdUvj", name="Token Counter", product_id="prod_abc123", unit="tokens",
        RetryConfig("backoff", BackoffStrategy(1, 50, 1.1, 100), False))

    # Handle response
    print(res)

```

If you'd like to override the default retry strategy for all operations that support retries, you can use the `retry_config` optional parameter when initializing the SDK:
```python
import os
from paygentic_sdk import Paygentic
from paygentic_sdk.utils import BackoffStrategy, RetryConfig


with Paygentic(
    retry_config=RetryConfig("backoff", BackoffStrategy(1, 50, 1.1, 100), False),
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billable_metrics.create(aggregation="SUM", description="Tracks total tokens consumed per API call.", merchant_id="org_YS8jkP59V71TdUvj", name="Token Counter", product_id="prod_abc123", unit="tokens")

    # Handle response
    print(res)

```
<!-- End Retries [retries] -->

<!-- Start Error Handling [errors] -->
## Error Handling

[`PaygenticError`](https://github.com/paygentic/sdk-python/blob/master/./src/paygentic_sdk/errors/paygenticerror.py) is the base class for all HTTP error responses. It has the following properties:

| Property           | Type             | Description                                                                             |
| ------------------ | ---------------- | --------------------------------------------------------------------------------------- |
| `err.message`      | `str`            | Error message                                                                           |
| `err.status_code`  | `int`            | HTTP response status code eg `404`                                                      |
| `err.headers`      | `httpx.Headers`  | HTTP response headers                                                                   |
| `err.body`         | `str`            | HTTP body. Can be empty string if no body is returned.                                  |
| `err.raw_response` | `httpx.Response` | Raw HTTP response                                                                       |
| `err.data`         |                  | Optional. Some errors may contain structured data. [See Error Classes](https://github.com/paygentic/sdk-python/blob/master/#error-classes). |

### Example
```python
import os
from paygentic_sdk import Paygentic, errors


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:
    res = None
    try:

        res = paygentic.billable_metrics.create(aggregation="SUM", description="Tracks total tokens consumed per API call.", merchant_id="org_YS8jkP59V71TdUvj", name="Token Counter", product_id="prod_abc123", unit="tokens")

        # Handle response
        print(res)


    except errors.PaygenticError as e:
        # The base class for HTTP error responses
        print(e.message)
        print(e.status_code)
        print(e.body)
        print(e.headers)
        print(e.raw_response)

        # Depending on the method different errors may be thrown
        if isinstance(e, errors.Error):
            print(e.data.error)  # Optional[str]
            print(e.data.message)  # str
            print(e.data.code)  # Optional[str]
            print(e.data.details)  # Optional[Dict[str, Any]]
```

### Error Classes
**Primary errors:**
* [`PaygenticError`](https://github.com/paygentic/sdk-python/blob/master/./src/paygentic_sdk/errors/paygenticerror.py): The base class for HTTP error responses.
  * [`Error`](https://github.com/paygentic/sdk-python/blob/master/./src/paygentic_sdk/errors/error.py): *

<details><summary>Less common errors (8)</summary>

<br />

**Network errors:**
* [`httpx.RequestError`](https://www.python-httpx.org/exceptions/#httpx.RequestError): Base class for request errors.
    * [`httpx.ConnectError`](https://www.python-httpx.org/exceptions/#httpx.ConnectError): HTTP client was unable to make a request to a server.
    * [`httpx.TimeoutException`](https://www.python-httpx.org/exceptions/#httpx.TimeoutException): HTTP request timed out.


**Inherit from [`PaygenticError`](https://github.com/paygentic/sdk-python/blob/master/./src/paygentic_sdk/errors/paygenticerror.py)**:
* [`ValidationError`](https://github.com/paygentic/sdk-python/blob/master/./src/paygentic_sdk/errors/validationerror.py): Bad Request - The request could not be understood or was missing required parameters. Status code `400`. Applicable to 81 of 133 methods.*
* [`DeleteCustomerConflictError`](https://github.com/paygentic/sdk-python/blob/master/./src/paygentic_sdk/errors/deletecustomerconflicterror.py): Customer cannot be deleted due to active dependencies. Status code `409`. Applicable to 1 of 133 methods.*
* [`DeleteFeeConflictError`](https://github.com/paygentic/sdk-python/blob/master/./src/paygentic_sdk/errors/deletefeeconflicterror.py): Fee cannot be deleted because it has associated prices. Status code `409`. Applicable to 1 of 133 methods.*
* [`ResponseValidationError`](https://github.com/paygentic/sdk-python/blob/master/./src/paygentic_sdk/errors/responsevalidationerror.py): Type mismatch between the response data and the expected Pydantic model. Provides access to the Pydantic validation error via the `cause` attribute.

</details>

\* Check [the method documentation](https://github.com/paygentic/sdk-python/blob/master/#available-resources-and-operations) to see if the error is applicable.
<!-- End Error Handling [errors] -->

<!-- Start Server Selection [server] -->
## Server Selection

### Select Server by Index

You can override the default server globally by passing a server index to the `server_idx: int` optional parameter when initializing the SDK client instance. The selected server will then be used as the default on the operations that use it. This table lists the indexes associated with the available servers:

| #   | Server                             | Description    |
| --- | ---------------------------------- | -------------- |
| 0   | `https://api.paygentic.io`         | Production API |
| 1   | `https://api.sandbox.paygentic.io` | Sandbox API    |

#### Example

```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    server_idx=0,
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billable_metrics.create(aggregation="SUM", description="Tracks total tokens consumed per API call.", merchant_id="org_YS8jkP59V71TdUvj", name="Token Counter", product_id="prod_abc123", unit="tokens")

    # Handle response
    print(res)

```

### Override Server URL Per-Client

The default server can also be overridden globally by passing a URL to the `server_url: str` optional parameter when initializing the SDK client instance. For example:
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    server_url="https://api.sandbox.paygentic.io",
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billable_metrics.create(aggregation="SUM", description="Tracks total tokens consumed per API call.", merchant_id="org_YS8jkP59V71TdUvj", name="Token Counter", product_id="prod_abc123", unit="tokens")

    # Handle response
    print(res)

```
<!-- End Server Selection [server] -->

<!-- Start Custom HTTP Client [http-client] -->
## Custom HTTP Client

The Python SDK makes API calls using the [httpx](https://www.python-httpx.org/) HTTP library.  In order to provide a convenient way to configure timeouts, cookies, proxies, custom headers, and other low-level configuration, you can initialize the SDK client with your own HTTP client instance.
Depending on whether you are using the sync or async version of the SDK, you can pass an instance of `HttpClient` or `AsyncHttpClient` respectively, which are Protocol's ensuring that the client has the necessary methods to make API calls.
This allows you to wrap the client with your own custom logic, such as adding custom headers, logging, or error handling, or you can just pass an instance of `httpx.Client` or `httpx.AsyncClient` directly.

For example, you could specify a header for every request that this sdk makes as follows:
```python
from paygentic_sdk import Paygentic
import httpx

http_client = httpx.Client(headers={"x-custom-header": "someValue"})
s = Paygentic(client=http_client)
```

or you could wrap the client with your own custom logic:
```python
from paygentic_sdk import Paygentic
from paygentic_sdk.httpclient import AsyncHttpClient
import httpx

class CustomClient(AsyncHttpClient):
    client: AsyncHttpClient

    def __init__(self, client: AsyncHttpClient):
        self.client = client

    async def send(
        self,
        request: httpx.Request,
        *,
        stream: bool = False,
        auth: Union[
            httpx._types.AuthTypes, httpx._client.UseClientDefault, None
        ] = httpx.USE_CLIENT_DEFAULT,
        follow_redirects: Union[
            bool, httpx._client.UseClientDefault
        ] = httpx.USE_CLIENT_DEFAULT,
    ) -> httpx.Response:
        request.headers["Client-Level-Header"] = "added by client"

        return await self.client.send(
            request, stream=stream, auth=auth, follow_redirects=follow_redirects
        )

    def build_request(
        self,
        method: str,
        url: httpx._types.URLTypes,
        *,
        content: Optional[httpx._types.RequestContent] = None,
        data: Optional[httpx._types.RequestData] = None,
        files: Optional[httpx._types.RequestFiles] = None,
        json: Optional[Any] = None,
        params: Optional[httpx._types.QueryParamTypes] = None,
        headers: Optional[httpx._types.HeaderTypes] = None,
        cookies: Optional[httpx._types.CookieTypes] = None,
        timeout: Union[
            httpx._types.TimeoutTypes, httpx._client.UseClientDefault
        ] = httpx.USE_CLIENT_DEFAULT,
        extensions: Optional[httpx._types.RequestExtensions] = None,
    ) -> httpx.Request:
        return self.client.build_request(
            method,
            url,
            content=content,
            data=data,
            files=files,
            json=json,
            params=params,
            headers=headers,
            cookies=cookies,
            timeout=timeout,
            extensions=extensions,
        )

s = Paygentic(async_client=CustomClient(httpx.AsyncClient()))
```
<!-- End Custom HTTP Client [http-client] -->

<!-- Start Resource Management [resource-management] -->
## Resource Management

The `Paygentic` class implements the context manager protocol and registers a finalizer function to close the underlying sync and async HTTPX clients it uses under the hood. This will close HTTP connections, release memory and free up other resources held by the SDK. In short-lived Python programs and notebooks that make a few SDK method calls, resource management may not be a concern. However, in longer-lived programs, it is beneficial to create a single SDK instance via a [context manager][context-manager] and reuse it across the application.

[context-manager]: https://docs.python.org/3/reference/datamodel.html#context-managers

```python
import os
from paygentic_sdk import Paygentic
def main():

    with Paygentic(
        bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
    ) as paygentic:
        # Rest of application here...


# Or when using async:
async def amain():

    async with Paygentic(
        bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
    ) as paygentic:
        # Rest of application here...
```
<!-- End Resource Management [resource-management] -->

<!-- Start Debugging [debug] -->
## Debugging

You can setup your SDK to emit debug logs for SDK requests and responses.

You can pass your own logger class directly into your SDK.
```python
from paygentic_sdk import Paygentic
import logging

logging.basicConfig(level=logging.DEBUG)
s = Paygentic(debug_logger=logging.getLogger("paygentic_sdk"))
```

You can also enable a default debug logger by setting an environment variable `PAYGENTIC_DEBUG` to true.
<!-- End Debugging [debug] -->

<!-- Placeholder for Future Speakeasy SDK Sections -->

# Development

## Maturity

This SDK is generally available. We follow semantic versioning — breaking changes will only occur in major version bumps. We recommend pinning to a specific minor version in production.

## Contributions

While we value open-source contributions to this SDK, this library is generated programmatically. Any manual changes added to internal files will be overwritten on the next generation. 
We look forward to hearing your feedback. Feel free to open a PR or an issue with a proof of concept and we'll do our best to include it in a future release. 

### SDK Created by [Speakeasy](https://www.speakeasy.com/?utm_source=paygentic-sdk&utm_campaign=python)
