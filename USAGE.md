<!-- Start SDK Example Usage [usage] -->
```python
# Synchronous Example
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billable_metrics.create(aggregation="SUM", description="orange daily out slow nor smoothly", merchant_id="<id>", name="<value>", product_id="<id>", unit="meter")

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

        res = await paygentic.billable_metrics.create_async(aggregation="SUM", description="orange daily out slow nor smoothly", merchant_id="<id>", name="<value>", product_id="<id>", unit="meter")

        # Handle response
        print(res)

asyncio.run(main())
```
<!-- End SDK Example Usage [usage] -->