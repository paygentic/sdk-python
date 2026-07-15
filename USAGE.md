<!-- Start SDK Example Usage [usage] -->
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

    res = paygentic.events.ingest(request={
        "type": "ai.inference",
        "source": "https://api.myapp.com",
        "subject": "cus_abc123",
        "data": {
            "tokens": 1500,
            "model": "gpt-4o",
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

        res = await paygentic.events.ingest_async(request={
            "type": "ai.inference",
            "source": "https://api.myapp.com",
            "subject": "cus_abc123",
            "data": {
                "tokens": 1500,
                "model": "gpt-4o",
            },
        })

        # Handle response
        print(res)

asyncio.run(main())
```
<!-- End SDK Example Usage [usage] -->