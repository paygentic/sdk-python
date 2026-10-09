# Merchants

## Overview

### Available Operations

* [reset](#reset) - Reset a merchant's data

## reset

With `scope: merchant`, deletes the merchant's customers and everything attached to them: subscriptions, invoices, line items, payments, entitlements, grants, orders, test clocks, usage events, invoice documents and, when tax is enabled, the documents in the merchant's Quaderno sandbox account. `keepCatalog: true` keeps the catalog (products, plans, prices, fees, features, billable metrics), and `keepCatalog: false` deletes it too; the merchant's configuration is always kept. With `scope: customer`, deletes one customer and what is attached to it; test clocks and the Quaderno account's documents are kept, since they belong to no single customer.

A `204` means every delete is done or scheduled: usage events and Quaderno documents finish in the background, and usage events still being ingested while it runs can survive it. A `502` means a store outside Postgres failed; the customers are already out of the API, and calling again with the same body finishes the reset. Calling again is always safe. While a customer waits for that, its external id is free for a new customer to take; a retry then deletes usage events by customer id only.

Not available in production.

### Example Usage

<!-- UsageSnippet language="python" operationID="resetMerchant" method="post" path="/v0/merchants/{merchantId}/reset" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    paygentic.merchants.reset(merchant_id="<id>", merchant_reset={
        "scope": "merchant",
        "keep_catalog": False,
    })

    # Use the SDK ...

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `merchant_id`                                                       | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `merchant_reset`                                                    | [models.MerchantReset](../../models/merchantreset.md)               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403                     | application/json             |
| errors.Error                 | 500, 502                     | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |