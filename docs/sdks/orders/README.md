# Orders

## Overview

Manage Orders, their line items, and billing schedules.

### Available Operations

* [create_order](#create_order) - Create an order
* [list_orders](#list_orders) - List orders
* [get_order](#get_order) - Get an order
* [update_order](#update_order) - Update an order
* [delete_order](#delete_order) - Delete an order
* [create_order_line_item](#create_order_line_item) - Add a line item
* [update_order_line_item](#update_order_line_item) - Update a line item
* [delete_order_line_item](#delete_order_line_item) - Delete a line item
* [create_order_approval](#create_order_approval) - Create an approval for the order

## create_order

Create an order

### Example Usage

<!-- UsageSnippet language="python" operationID="createOrder" method="post" path="/v0/orders" -->
```python
import os
from paygentic_sdk import Paygentic
from paygentic_sdk.utils import parse_datetime


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.orders.create_order(customer_id="<id>", currency="Bhutanese Ngultrum", term_start_date=parse_datetime("2024-07-21T22:30:59.168Z"), term_end_date=parse_datetime("2026-01-25T22:12:02.280Z"), total_amount="<value>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                 | Type                                                                                      | Required                                                                                  | Description                                                                               |
| ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| `customer_id`                                                                             | *str*                                                                                     | :heavy_check_mark:                                                                        | N/A                                                                                       |
| `currency`                                                                                | *str*                                                                                     | :heavy_check_mark:                                                                        | N/A                                                                                       |
| `term_start_date`                                                                         | [date](https://docs.python.org/3/library/datetime.html#date-objects)                      | :heavy_check_mark:                                                                        | N/A                                                                                       |
| `term_end_date`                                                                           | [date](https://docs.python.org/3/library/datetime.html#date-objects)                      | :heavy_check_mark:                                                                        | N/A                                                                                       |
| `total_amount`                                                                            | *str*                                                                                     | :heavy_check_mark:                                                                        | N/A                                                                                       |
| `type`                                                                                    | [OptionalNullable[models.CreateOrderRequestType]](../../models/createorderrequesttype.md) | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `close_date`                                                                              | [date](https://docs.python.org/3/library/datetime.html#date-objects)                      | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `default_payment_term_days`                                                               | *Optional[int]*                                                                           | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `metadata`                                                                                | Dict[str, *Any*]                                                                          | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `line_items`                                                                              | List[[models.CreateOrderLineItemRequest](../../models/createorderlineitemrequest.md)]     | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `reseller_id`                                                                             | *Optional[str]*                                                                           | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `tax_exempt`                                                                              | *Optional[bool]*                                                                          | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `selling_entity`                                                                          | *Optional[str]*                                                                           | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `retries`                                                                                 | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                          | :heavy_minus_sign:                                                                        | Configuration to override the default retry behavior of the client.                       |

### Response

**[models.Order](../../models/order.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## list_orders

List orders

### Example Usage

<!-- UsageSnippet language="python" operationID="listOrders" method="get" path="/v0/orders" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.orders.list_orders(request={})

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `request`                                                           | [models.ListOrdersRequest](../../models/listordersrequest.md)       | :heavy_check_mark:                                                  | The request object to use for the request.                          |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.OrderList](../../models/orderlist.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get_order

Get an order

### Example Usage

<!-- UsageSnippet language="python" operationID="getOrder" method="get" path="/v0/orders/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.orders.get_order(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.Order](../../models/order.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## update_order

Update an order

### Example Usage

<!-- UsageSnippet language="python" operationID="updateOrder" method="patch" path="/v0/orders/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.orders.update_order(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                 | Type                                                                                      | Required                                                                                  | Description                                                                               |
| ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| `id`                                                                                      | *str*                                                                                     | :heavy_check_mark:                                                                        | N/A                                                                                       |
| `type`                                                                                    | [OptionalNullable[models.UpdateOrderRequestType]](../../models/updateorderrequesttype.md) | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `term_start_date`                                                                         | [date](https://docs.python.org/3/library/datetime.html#date-objects)                      | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `term_end_date`                                                                           | [date](https://docs.python.org/3/library/datetime.html#date-objects)                      | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `close_date`                                                                              | [date](https://docs.python.org/3/library/datetime.html#date-objects)                      | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `total_amount`                                                                            | *Optional[str]*                                                                           | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `default_payment_term_days`                                                               | *Optional[int]*                                                                           | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `metadata`                                                                                | Dict[str, *Any*]                                                                          | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `cancelled_at`                                                                            | [date](https://docs.python.org/3/library/datetime.html#date-objects)                      | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `reseller_id`                                                                             | *OptionalNullable[str]*                                                                   | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `tax_exempt`                                                                              | *Optional[bool]*                                                                          | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `selling_entity`                                                                          | *OptionalNullable[str]*                                                                   | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `retries`                                                                                 | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                          | :heavy_minus_sign:                                                                        | Configuration to override the default retry behavior of the client.                       |

### Response

**[models.Order](../../models/order.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## delete_order

Delete an order

### Example Usage

<!-- UsageSnippet language="python" operationID="deleteOrder" method="delete" path="/v0/orders/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    paygentic.orders.delete_order(id="<id>")

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

## create_order_line_item

Add a line item

### Example Usage

<!-- UsageSnippet language="python" operationID="createOrderLineItem" method="post" path="/v0/orders/{orderId}/lineItems" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.orders.create_order_line_item(order_id="<id>", quantity="<value>", list_unit_price="<value>", unit_price="<value>", total_price="<value>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                            | Type                                                                 | Required                                                             | Description                                                          |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `order_id`                                                           | *str*                                                                | :heavy_check_mark:                                                   | N/A                                                                  |
| `quantity`                                                           | *str*                                                                | :heavy_check_mark:                                                   | N/A                                                                  |
| `list_unit_price`                                                    | *str*                                                                | :heavy_check_mark:                                                   | N/A                                                                  |
| `unit_price`                                                         | *str*                                                                | :heavy_check_mark:                                                   | N/A                                                                  |
| `total_price`                                                        | *str*                                                                | :heavy_check_mark:                                                   | N/A                                                                  |
| `item_id`                                                            | *OptionalNullable[str]*                                              | :heavy_minus_sign:                                                   | N/A                                                                  |
| `description`                                                        | *OptionalNullable[str]*                                              | :heavy_minus_sign:                                                   | N/A                                                                  |
| `discount_unit_amount`                                               | *Optional[str]*                                                      | :heavy_minus_sign:                                                   | N/A                                                                  |
| `metadata`                                                           | Dict[str, *Any*]                                                     | :heavy_minus_sign:                                                   | N/A                                                                  |
| `term_start_date`                                                    | [date](https://docs.python.org/3/library/datetime.html#date-objects) | :heavy_minus_sign:                                                   | N/A                                                                  |
| `term_end_date`                                                      | [date](https://docs.python.org/3/library/datetime.html#date-objects) | :heavy_minus_sign:                                                   | N/A                                                                  |
| `retries`                                                            | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)     | :heavy_minus_sign:                                                   | Configuration to override the default retry behavior of the client.  |

### Response

**[models.OrderLineItem](../../models/orderlineitem.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## update_order_line_item

Update a line item

### Example Usage

<!-- UsageSnippet language="python" operationID="updateOrderLineItem" method="patch" path="/v0/orders/{orderId}/lineItems/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.orders.update_order_line_item(order_id="<id>", id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                            | Type                                                                 | Required                                                             | Description                                                          |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `order_id`                                                           | *str*                                                                | :heavy_check_mark:                                                   | N/A                                                                  |
| `id`                                                                 | *str*                                                                | :heavy_check_mark:                                                   | N/A                                                                  |
| `item_id`                                                            | *OptionalNullable[str]*                                              | :heavy_minus_sign:                                                   | N/A                                                                  |
| `description`                                                        | *OptionalNullable[str]*                                              | :heavy_minus_sign:                                                   | N/A                                                                  |
| `quantity`                                                           | *Optional[str]*                                                      | :heavy_minus_sign:                                                   | N/A                                                                  |
| `list_unit_price`                                                    | *Optional[str]*                                                      | :heavy_minus_sign:                                                   | N/A                                                                  |
| `discount_unit_amount`                                               | *Optional[str]*                                                      | :heavy_minus_sign:                                                   | N/A                                                                  |
| `unit_price`                                                         | *Optional[str]*                                                      | :heavy_minus_sign:                                                   | N/A                                                                  |
| `total_price`                                                        | *Optional[str]*                                                      | :heavy_minus_sign:                                                   | N/A                                                                  |
| `metadata`                                                           | Dict[str, *Any*]                                                     | :heavy_minus_sign:                                                   | N/A                                                                  |
| `term_start_date`                                                    | [date](https://docs.python.org/3/library/datetime.html#date-objects) | :heavy_minus_sign:                                                   | N/A                                                                  |
| `term_end_date`                                                      | [date](https://docs.python.org/3/library/datetime.html#date-objects) | :heavy_minus_sign:                                                   | N/A                                                                  |
| `retries`                                                            | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)     | :heavy_minus_sign:                                                   | Configuration to override the default retry behavior of the client.  |

### Response

**[models.OrderLineItem](../../models/orderlineitem.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## delete_order_line_item

Delete a line item

### Example Usage

<!-- UsageSnippet language="python" operationID="deleteOrderLineItem" method="delete" path="/v0/orders/{orderId}/lineItems/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    paygentic.orders.delete_order_line_item(order_id="<id>", id="<id>")

    # Use the SDK ...

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `order_id`                                                          | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## create_order_approval

Submit the order for maker-checker approval. Returns 409 if a pending approval already exists.

### Example Usage

<!-- UsageSnippet language="python" operationID="createOrderApproval" method="post" path="/v0/orders/{orderId}/approvals" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.orders.create_order_approval(order_id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                      | Type                                                                                                                           | Required                                                                                                                       | Description                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------ |
| `order_id`                                                                                                                     | *str*                                                                                                                          | :heavy_check_mark:                                                                                                             | N/A                                                                                                                            |
| `requester`                                                                                                                    | *Optional[str]*                                                                                                                | :heavy_minus_sign:                                                                                                             | Optional. The maker submitting the order. Derived from the authenticated principal; only a platform key may set it explicitly. |
| `note`                                                                                                                         | *OptionalNullable[str]*                                                                                                        | :heavy_minus_sign:                                                                                                             | N/A                                                                                                                            |
| `retries`                                                                                                                      | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                               | :heavy_minus_sign:                                                                                                             | Configuration to override the default retry behavior of the client.                                                            |

### Response

**[models.Approval](../../models/approval.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |