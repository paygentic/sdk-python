# Users

## Overview

A `User` is an entity granted access to an Organization's resources. All operations are performed by users.

### Available Operations

* [get](#get) - Get
* [update](#update) - Update

## get

Get

### Example Usage

<!-- UsageSnippet language="python" operationID="getUser" method="get" path="/v0/users/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.users.get(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.User](../../models/user.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## update

Update

### Example Usage

<!-- UsageSnippet language="python" operationID="updateUser" method="patch" path="/v0/users/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.users.update(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                    | Type                                                                         | Required                                                                     | Description                                                                  |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `id`                                                                         | *str*                                                                        | :heavy_check_mark:                                                           | N/A                                                                          |
| `address`                                                                    | [Optional[models.Address]](../../models/address.md)                          | :heavy_minus_sign:                                                           | N/A                                                                          |
| `date_of_birth`                                                              | [datetime](https://docs.python.org/3/library/datetime.html#datetime-objects) | :heavy_minus_sign:                                                           | The date of birth of the user.                                               |
| `first_name`                                                                 | *Optional[str]*                                                              | :heavy_minus_sign:                                                           | The first name of the user.                                                  |
| `last_name`                                                                  | *Optional[str]*                                                              | :heavy_minus_sign:                                                           | The last name of the user.                                                   |
| `phone`                                                                      | *Optional[str]*                                                              | :heavy_minus_sign:                                                           | The phone number of the user.                                                |
| `type`                                                                       | [Optional[models.UpdateUserType]](../../models/updateusertype.md)            | :heavy_minus_sign:                                                           | Type of entity the user represents.                                          |
| `retries`                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)             | :heavy_minus_sign:                                                           | Configuration to override the default retry behavior of the client.          |

### Response

**[models.User](../../models/user.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |