# MerchantIntegrations

## Overview

A `MerchantIntegration` records a merchant's connection to an external provider. One connection per `(merchant, provider)` — re-connecting upserts in place.

### Available Operations

* [list_merchant_integrations](#list_merchant_integrations) - List
* [upsert_merchant_integration](#upsert_merchant_integration) - Upsert
* [get_merchant_integration](#get_merchant_integration) - Get
* [disconnect_merchant_integration](#disconnect_merchant_integration) - Disconnect

## list_merchant_integrations

List

### Example Usage

<!-- UsageSnippet language="python" operationID="listMerchantIntegrations" method="get" path="/v0/merchantIntegrations" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.merchant_integrations.list_merchant_integrations(request={})

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                 | Type                                                                                      | Required                                                                                  | Description                                                                               |
| ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| `request`                                                                                 | [models.ListMerchantIntegrationsRequest](../../models/listmerchantintegrationsrequest.md) | :heavy_check_mark:                                                                        | The request object to use for the request.                                                |
| `retries`                                                                                 | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                          | :heavy_minus_sign:                                                                        | Configuration to override the default retry behavior of the client.                       |

### Response

**[models.ListMerchantIntegrationsResponse](../../models/listmerchantintegrationsresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## upsert_merchant_integration

Create or re-activate a merchant's connection to a provider. Idempotent on `(merchantId, provider)` — connecting an already-connected provider re-activates the existing row, never creating a duplicate.

### Example Usage

<!-- UsageSnippet language="python" operationID="upsertMerchantIntegration" method="put" path="/v0/merchantIntegrations" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.merchant_integrations.upsert_merchant_integration(merchant_id="<id>", provider="salesforce")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                               | Type                                                                                    | Required                                                                                | Description                                                                             |
| --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `merchant_id`                                                                           | *str*                                                                                   | :heavy_check_mark:                                                                      | Unique identifier for an organization                                                   |
| `provider`                                                                              | [models.MerchantIntegrationProvider](../../models/merchantintegrationprovider.md)       | :heavy_check_mark:                                                                      | External provider a merchant can connect at the tenant level                            |
| `external_id`                                                                           | *Optional[str]*                                                                         | :heavy_minus_sign:                                                                      | Ampersand installation id.                                                              |
| `status`                                                                                | [Optional[models.MerchantIntegrationStatus]](../../models/merchantintegrationstatus.md) | :heavy_minus_sign:                                                                      | Connection lifecycle state. Live Ampersand health is separate and not stored here.      |
| `config`                                                                                | Dict[str, *Any*]                                                                        | :heavy_minus_sign:                                                                      | N/A                                                                                     |
| `metadata`                                                                              | Dict[str, *Any*]                                                                        | :heavy_minus_sign:                                                                      | N/A                                                                                     |
| `retries`                                                                               | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                        | :heavy_minus_sign:                                                                      | Configuration to override the default retry behavior of the client.                     |

### Response

**[models.MerchantIntegration](../../models/merchantintegration.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get_merchant_integration

Get

### Example Usage

<!-- UsageSnippet language="python" operationID="getMerchantIntegration" method="get" path="/v0/merchantIntegrations/{id}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.merchant_integrations.get_merchant_integration(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the merchant integration                   |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.MerchantIntegration](../../models/merchantintegration.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## disconnect_merchant_integration

Soft-disconnect a connection (status `disconnected`, stamp `disconnectedAt`). Never hard-deletes — preserves the install id and `connectedAt` for audit.

### Example Usage

<!-- UsageSnippet language="python" operationID="disconnectMerchantIntegration" method="patch" path="/v0/merchantIntegrations/{id}/disconnect" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.merchant_integrations.disconnect_merchant_integration(id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `id`                                                                | *str*                                                               | :heavy_check_mark:                                                  | The unique identifier of the merchant integration                   |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.MerchantIntegration](../../models/merchantintegration.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |