# InvoicesV2

## Overview

Invoice V2 operations supporting billing cycles organized by time periods. Warning: v0 invoice endpoints are no longer supported.

### Available Operations

* [list](#list) - List
* [list_line_items](#list_line_items) - List Line Items
* [create_line_item](#create_line_item) - Create Manual Line Item
* [get](#get) - Get
* [get_line_items](#get_line_items) - Get Line Items
* [download_invoice_pdf](#download_invoice_pdf) - Download Invoice PDF
* [create_invoice_refund](#create_invoice_refund) - Refund Invoice
* [list_invoice_refunds](#list_invoice_refunds) - List Invoice Refunds
* [void_invoice_refund](#void_invoice_refund) - Void Invoice Refund

## list

List invoices with optional filters. Platform users can use nextActionAt=ready to get invoices ready for processing.

### Example Usage

<!-- UsageSnippet language="python" operationID="listInvoices" method="get" path="/v2/invoices" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.invoices_v2.list(request={})

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `request`                                                           | [models.ListInvoicesRequest](../../models/listinvoicesrequest.md)   | :heavy_check_mark:                                                  | The request object to use for the request.                          |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.ListInvoicesResponse](../../models/listinvoicesresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 403                          | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## list_line_items

List pending and invoiced line items for a subscription from the billing database. Returns exact fee amounts and estimated metered charges.

### Example Usage

<!-- UsageSnippet language="python" operationID="listLineItems" method="get" path="/v2/invoices/lineItems" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.invoices_v2.list_line_items(request={})

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `request`                                                           | [models.ListLineItemsRequest](../../models/listlineitemsrequest.md) | :heavy_check_mark:                                                  | The request object to use for the request.                          |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.LineItemsResponse](../../models/lineitemsresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## create_line_item

Create a manual line item for a billing v1 subscription. Manual line items are ad-hoc charges or credits that flow through the same collection pipeline as auto-generated items. Exactly one of subscriptionId or invoiceId must be provided.

### Example Usage

<!-- UsageSnippet language="python" operationID="createLineItem" method="post" path="/v2/invoices/lineItems" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.invoices_v2.create_line_item(display_name="Nathan54", currency="Rwanda Franc", quantity=6214.31, unit_price=7408.13)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                   | Type                                                                                                                                                                                                                                                        | Required                                                                                                                                                                                                                                                    | Description                                                                                                                                                                                                                                                 |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `display_name`                                                                                                                                                                                                                                              | *str*                                                                                                                                                                                                                                                       | :heavy_check_mark:                                                                                                                                                                                                                                          | Human-readable label shown on the invoice.                                                                                                                                                                                                                  |
| `currency`                                                                                                                                                                                                                                                  | *str*                                                                                                                                                                                                                                                       | :heavy_check_mark:                                                                                                                                                                                                                                          | ISO 4217 currency code (e.g., USD). Must match the subscription or invoice currency.                                                                                                                                                                        |
| `quantity`                                                                                                                                                                                                                                                  | *float*                                                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                                                          | Number of units.                                                                                                                                                                                                                                            |
| `unit_price`                                                                                                                                                                                                                                                | *float*                                                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                                                          | Price per unit as a decimal amount (e.g., 29.99 for $29.99). Can be negative for credits or adjustments.                                                                                                                                                    |
| `idempotency_key_param`                                                                                                                                                                                                                                     | *Optional[str]*                                                                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                                                          | Optional idempotency key. If provided, duplicate requests with the same key return the previously created item.                                                                                                                                             |
| `subscription_id`                                                                                                                                                                                                                                           | *Optional[str]*                                                                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                                                          | The subscription ID. Exactly one of subscriptionId or invoiceId must be provided.                                                                                                                                                                           |
| `invoice_id`                                                                                                                                                                                                                                                | *Optional[str]*                                                                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                                                          | The invoice ID to attach this item directly to. Exactly one of subscriptionId or invoiceId must be provided. The invoice must be in ACTIVE or CLOSING state.                                                                                                |
| `description`                                                                                                                                                                                                                                               | *OptionalNullable[str]*                                                                                                                                                                                                                                     | :heavy_minus_sign:                                                                                                                                                                                                                                          | Optional longer description shown on the invoice.                                                                                                                                                                                                           |
| `invoice_at`                                                                                                                                                                                                                                                | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                                                                                        | :heavy_minus_sign:                                                                                                                                                                                                                                          | When to collect this item into an invoice. Defaults to now. Ignored when invoiceId is provided.                                                                                                                                                             |
| `period_start`                                                                                                                                                                                                                                              | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                                                                                        | :heavy_minus_sign:                                                                                                                                                                                                                                          | Start of the billing period for display purposes. Defaults to now.                                                                                                                                                                                          |
| `period_end`                                                                                                                                                                                                                                                | [date](https://docs.python.org/3/library/datetime.html#date-objects)                                                                                                                                                                                        | :heavy_minus_sign:                                                                                                                                                                                                                                          | End of the billing period for display purposes. Defaults to now.                                                                                                                                                                                            |
| `idempotency_key`                                                                                                                                                                                                                                           | *OptionalNullable[str]*                                                                                                                                                                                                                                     | :heavy_minus_sign:                                                                                                                                                                                                                                          | Optional caller-provided idempotency key. Auto-generated if not provided.                                                                                                                                                                                   |
| `item_id`                                                                                                                                                                                                                                                   | *OptionalNullable[str]*                                                                                                                                                                                                                                     | :heavy_minus_sign:                                                                                                                                                                                                                                          | Optional item to tag this line with, for accounting/GL mapping. Must belong to the caller's merchant and must not be archived. A manual line has no price, so it is never reached by a later restamp — supplying it here is the only opportunity to tag it. |
| `retries`                                                                                                                                                                                                                                                   | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                                                                                          | Configuration to override the default retry behavior of the client.                                                                                                                                                                                         |

### Response

**[models.LineItem](../../models/lineitem.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404, 409, 422      | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get

Retrieve a single invoice with real-time aggregates (for ACTIVE/CLOSING/CLOSED) or cached aggregates (for finalized invoices). Optionally include line items with expand=lineItems.

### Example Usage

<!-- UsageSnippet language="python" operationID="getInvoice" method="get" path="/v2/invoices/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.invoices_v2.get(id="<id>", line_items_limit=100)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Type                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Required                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | *str*                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | The invoice ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `expand`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | *Optional[str]*                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Comma-separated list of fields to expand. Supports: lineItems, items. `items` resolves each returned line's item and its external accounting codes into an `items` collection inside the lineItems block; because those ids come from the lines, requesting `items` also expands `lineItems` on its default paging.                                                                                                                                                                                                                                                                   |
| `line_items_limit`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | *Optional[int]*                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Page size for line items when expand=lineItems                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `line_items_page_token`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | *Optional[str]*                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Opaque pagination token for line items when expand=lineItems, taken from a previous response's nextPageToken. Do not construct or parse this value.                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| `provider`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | *Optional[str]*                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Narrows which external references are returned per item when expand=items. Matched exactly against the provider stored on the reference (e.g. accountsiq); there is no allowlist of known providers, but the value must satisfy the same format every stored provider does, so a malformed one is rejected rather than answered with an empty result that reads as "nothing is mapped". It never removes lines or items: an item with no reference for this provider comes back with an empty list, so unmapped SKUs stay visible. Ignored when the items expansion is not requested. |
| `retries`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Configuration to override the default retry behavior of the client.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

### Response

**[models.Invoice](../../models/invoice.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get_line_items

Get paginated line items for an invoice

### Example Usage

<!-- UsageSnippet language="python" operationID="getInvoiceLineItems" method="get" path="/v2/invoices/{id}/lineItems" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.invoices_v2.get_line_items(id="<id>", limit=100)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Type                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Required                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | *str*                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | The invoice ID                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `limit`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | *Optional[int]*                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Maximum number of line items to return                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `page_token`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | *Optional[str]*                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Opaque pagination token to fetch the next page of results, taken from a previous response's nextPageToken. Do not construct or parse this value.                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `expand`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | *Optional[str]*                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Comma-separated list of fields to expand. Supports: items — resolves each returned line's item and that item's external accounting codes into an `items` collection, so a line can be translated to a GL/SKU code without a second call.                                                                                                                                                                                                                                                                                                                                              |
| `provider`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | *Optional[str]*                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Narrows which external references are returned per item when expand=items. Matched exactly against the provider stored on the reference (e.g. accountsiq); there is no allowlist of known providers, but the value must satisfy the same format every stored provider does, so a malformed one is rejected rather than answered with an empty result that reads as "nothing is mapped". It never removes lines or items: an item with no reference for this provider comes back with an empty list, so unmapped SKUs stay visible. Ignored when the items expansion is not requested. |
| `retries`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Configuration to override the default retry behavior of the client.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

### Response

**[models.InvoiceLineItemsResponse](../../models/invoicelineitemsresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## download_invoice_pdf

Downloads the Paygentic-rendered invoice document. The caller must be authenticated and entitled to the invoice; the stored document is streamed back, so no storage URL is ever handed out. Returns 404 when the invoice's document is the tax provider's rather than ours — in that case the invoice resource reports pdfSource `tax_provider` and its pdfUrl points at the provider's link instead.

### Example Usage

<!-- UsageSnippet language="python" operationID="downloadInvoicePdf" method="get" path="/v2/invoices/{id}/pdf" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.invoices_v2.download_invoice_pdf(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The invoice ID                                                      |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[httpx.Response](../../models/.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## create_invoice_refund

Issue a full refund against a paid invoice by creating a credit note. The invoice stays PAID; the refund is recorded as a child credit note. Accessible to the owning merchant or platform operators. Only works for invoices in PAID status that have not already been refunded. Full refund only — the entire invoice (subtotal + tax) is credited.

### Example Usage

<!-- UsageSnippet language="python" operationID="createInvoiceRefund" method="post" path="/v2/invoices/{id}/refunds" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.invoices_v2.create_invoice_refund(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The invoice ID                                                      |
| `reason`                                                            | *Optional[str]*                                                     | :heavy_minus_sign:                                                  | Optional reason for the refund (recorded on the credit note)        |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.InvoiceRefund](../../models/invoicerefund.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## list_invoice_refunds

List the credit notes (refunds) recorded against an invoice. Accessible to the owning merchant or platform operators.

### Example Usage

<!-- UsageSnippet language="python" operationID="listInvoiceRefunds" method="get" path="/v2/invoices/{id}/refunds" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.invoices_v2.list_invoice_refunds(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The invoice ID                                                      |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.InvoiceRefundList](../../models/invoicerefundlist.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## void_invoice_refund

Void a previously-issued refund (credit note). Reverses the credit note in the tax provider and excludes it from revenue. Accessible to the owning merchant or platform operators.

### Example Usage

<!-- UsageSnippet language="python" operationID="voidInvoiceRefund" method="post" path="/v2/invoices/{id}/refunds/{refundId}/void" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.invoices_v2.void_invoice_refund(id="<id>", refund_id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                            | Type                                                                 | Required                                                             | Description                                                          |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `id`                                                                 | *str*                                                                | :heavy_check_mark:                                                   | The invoice ID                                                       |
| `refund_id`                                                          | *str*                                                                | :heavy_check_mark:                                                   | The refund (credit note) ID                                          |
| `reason`                                                             | *Optional[str]*                                                      | :heavy_minus_sign:                                                   | Optional reason for voiding the refund (recorded on the credit note) |
| `retries`                                                            | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)     | :heavy_minus_sign:                                                   | Configuration to override the default retry behavior of the client.  |

### Response

**[models.InvoiceRefund](../../models/invoicerefund.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |