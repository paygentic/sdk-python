# ExternalReferences

## Overview

An `ExternalReference` links a Paygentic entity (e.g. an `Item`) to a record in an external system such as Salesforce or NetSuite. Multiple external records may map to the same Paygentic entity, but each external id is the *primary* reference of at most one entity per merchant.

### Available Operations

* [create_external_reference](#create_external_reference) - Create
* [list_external_references](#list_external_references) - List
* [get_external_reference](#get_external_reference) - Get
* [update_external_reference](#update_external_reference) - Update
* [delete_external_reference](#delete_external_reference) - Delete

## create_external_reference

Create

### Example Usage

<!-- UsageSnippet language="python" operationID="createExternalReference" method="post" path="/v0/externalReferences" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.external_references.create_external_reference(merchant_id="<id>", entity_type="item", entity_id="<id>", provider="<value>", external_id="<id>", is_primary=True, is_default=False)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                     | Type                                                                                                                                          | Required                                                                                                                                      | Description                                                                                                                                   |
| --------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| `merchant_id`                                                                                                                                 | *str*                                                                                                                                         | :heavy_check_mark:                                                                                                                            | N/A                                                                                                                                           |
| `entity_type`                                                                                                                                 | [models.EntityType](../../models/entitytype.md)                                                                                               | :heavy_check_mark:                                                                                                                            | The type of Paygentic entity this external reference points at                                                                                |
| `entity_id`                                                                                                                                   | *str*                                                                                                                                         | :heavy_check_mark:                                                                                                                            | Paygentic id of the entity, e.g. `itm_xxx`                                                                                                    |
| `provider`                                                                                                                                    | *str*                                                                                                                                         | :heavy_check_mark:                                                                                                                            | Lowercase snake_case provider identifier (e.g. `salesforce`, `netsuite`)                                                                      |
| `external_id`                                                                                                                                 | *str*                                                                                                                                         | :heavy_check_mark:                                                                                                                            | Identifier of the record in the external system                                                                                               |
| `external_label`                                                                                                                              | *Optional[str]*                                                                                                                               | :heavy_minus_sign:                                                                                                                            | Human-friendly name shown in UIs (e.g. a NetSuite financial-treatment name)                                                                   |
| `metadata`                                                                                                                                    | Dict[str, *Any*]                                                                                                                              | :heavy_minus_sign:                                                                                                                            | Provider-specific fields (e.g. `{ "sfObject": "Product2" }`)                                                                                  |
| `is_primary`                                                                                                                                  | *Optional[bool]*                                                                                                                              | :heavy_minus_sign:                                                                                                                            | Whether this is the canonical reference for `(provider, externalId)`. The primary is unique per merchant; non-primary references are aliases. |
| `is_default`                                                                                                                                  | *Optional[bool]*                                                                                                                              | :heavy_minus_sign:                                                                                                                            | Whether this is the default target for the entity + provider. At most one default per `(entityType, entityId, provider)`.                     |
| `retries`                                                                                                                                     | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                              | :heavy_minus_sign:                                                                                                                            | Configuration to override the default retry behavior of the client.                                                                           |

### Response

**[models.ExternalReference](../../models/externalreference.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404, 409           | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## list_external_references

List

### Example Usage

<!-- UsageSnippet language="python" operationID="listExternalReferences" method="get" path="/v0/externalReferences" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.external_references.list_external_references(request={})

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                             | Type                                                                                  | Required                                                                              | Description                                                                           |
| ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| `request`                                                                             | [models.ListExternalReferencesRequest](../../models/listexternalreferencesrequest.md) | :heavy_check_mark:                                                                    | The request object to use for the request.                                            |
| `retries`                                                                             | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                      | :heavy_minus_sign:                                                                    | Configuration to override the default retry behavior of the client.                   |

### Response

**[models.ListExternalReferencesResponse](../../models/listexternalreferencesresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get_external_reference

Get

### Example Usage

<!-- UsageSnippet language="python" operationID="getExternalReference" method="get" path="/v0/externalReferences/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.external_references.get_external_reference(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the external reference                     |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.ExternalReference](../../models/externalreference.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## update_external_reference

Update

### Example Usage

<!-- UsageSnippet language="python" operationID="updateExternalReference" method="patch" path="/v0/externalReferences/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.external_references.update_external_reference(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the external reference                     |
| `external_label`                                                    | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | N/A                                                                 |
| `metadata`                                                          | Dict[str, *Any*]                                                    | :heavy_minus_sign:                                                  | N/A                                                                 |
| `is_primary`                                                        | *Optional[bool]*                                                    | :heavy_minus_sign:                                                  | N/A                                                                 |
| `is_default`                                                        | *Optional[bool]*                                                    | :heavy_minus_sign:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.ExternalReference](../../models/externalreference.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404, 409           | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## delete_external_reference

Delete

### Example Usage

<!-- UsageSnippet language="python" operationID="deleteExternalReference" method="delete" path="/v0/externalReferences/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    paygentic.external_references.delete_external_reference(id="<id>")

    # Use the SDK ...

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the external reference                     |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |