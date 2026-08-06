# Items

## Overview

An `Item` is the canonical "thing you sell" that external-system mappings point at. It is fully decoupled from the billing `Product` and holds no pricing/plan/metering, and it is CRM/ERP agnostic — which providers map to it lives entirely in its `ExternalReference` rows.

### Available Operations

* [create_item](#create_item) - Create
* [list_items](#list_items) - List
* [get_item](#get_item) - Get
* [update_item](#update_item) - Update
* [delete_item](#delete_item) - Delete

## create_item

Create

### Example Usage

<!-- UsageSnippet language="python" operationID="createItem" method="post" path="/v0/items" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.items.create_item(merchant_id="<id>", name="<value>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `merchant_id`                                                       | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `name`                                                              | *str*                                                               | :heavy_check_mark:                                                  | Canonical sellable name for the Item                                |
| `catalog_id`                                                        | *Optional[str]*                                                     | :heavy_minus_sign:                                                  | Unique identifier for a product                                     |
| `metadata`                                                          | Dict[str, *Any*]                                                    | :heavy_minus_sign:                                                  | Optional key-value metadata                                         |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.Item](../../models/item.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## list_items

List

### Example Usage

<!-- UsageSnippet language="python" operationID="listItems" method="get" path="/v0/items" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.items.list_items(request={})

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `request`                                                           | [models.ListItemsRequest](../../models/listitemsrequest.md)         | :heavy_check_mark:                                                  | The request object to use for the request.                          |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.ListItemsResponse](../../models/listitemsresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get_item

Get

### Example Usage

<!-- UsageSnippet language="python" operationID="getItem" method="get" path="/v0/items/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.items.get_item(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the item                                   |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.Item](../../models/item.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## update_item

Update

### Example Usage

<!-- UsageSnippet language="python" operationID="updateItem" method="patch" path="/v0/items/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.items.update_item(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                 | Type                                                                                                                                                      | Required                                                                                                                                                  | Description                                                                                                                                               |
| --------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                                      | *str*                                                                                                                                                     | :heavy_check_mark:                                                                                                                                        | The unique identifier of the item                                                                                                                         |
| `name`                                                                                                                                                    | *Optional[str]*                                                                                                                                           | :heavy_minus_sign:                                                                                                                                        | N/A                                                                                                                                                       |
| `catalog_id`                                                                                                                                              | *OptionalNullable[str]*                                                                                                                                   | :heavy_minus_sign:                                                                                                                                        | The product this item belongs to.                                                                                                                         |
| `archived`                                                                                                                                                | *Optional[bool]*                                                                                                                                          | :heavy_minus_sign:                                                                                                                                        | Set to true to retire this item from your catalog, or false to restore it. Archived items remain readable and continue to resolve on historical invoices. |
| `metadata`                                                                                                                                                | Dict[str, *Any*]                                                                                                                                          | :heavy_minus_sign:                                                                                                                                        | N/A                                                                                                                                                       |
| `retries`                                                                                                                                                 | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                          | :heavy_minus_sign:                                                                                                                                        | Configuration to override the default retry behavior of the client.                                                                                       |

### Response

**[models.Item](../../models/item.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## delete_item

Delete

### Example Usage

<!-- UsageSnippet language="python" operationID="deleteItem" method="delete" path="/v0/items/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    paygentic.items.delete_item(id="<id>")

    # Use the SDK ...

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the item                                   |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |