# Webhooks

## Overview

Endpoints for setting up webhook integrations and administering webhook settings

### Available Operations

* [get](#get) - Get
* [enable](#enable) - Enable
* [update](#update) - Update
* [disable](#disable) - Disable
* [get_portal](#get_portal) - Get Portal Access

## get

Returns the webhook configuration for your account. Returns 404 if webhooks have never been enabled.

### Example Usage

<!-- UsageSnippet language="python" operationID="getWebhooks" method="get" path="/v0/webhooks" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.webhooks.get()

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `request`                                                           | [models.GetWebhooksRequest](../../models/getwebhooksrequest.md)     | :heavy_check_mark:                                                  | The request object to use for the request.                          |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.Webhooks](../../models/webhooks.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## enable

Turns on webhook delivery for your account. Call it once: when a configuration already exists, enabled or disabled, the response is 400 with code `DUPLICATE_RESOURCE`. Use the update operation to turn delivery on or off after that. Endpoint URLs, event subscriptions and the signing secret are managed in the webhook portal.

### Example Usage

<!-- UsageSnippet language="python" operationID="createWebhooks" method="post" path="/v0/webhooks" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.webhooks.enable()

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                             | Type                                                                  | Required                                                              | Description                                                           |
| --------------------------------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------- |
| `request`                                                             | [models.CreateWebhooksRequest](../../models/createwebhooksrequest.md) | :heavy_check_mark:                                                    | The request object to use for the request.                            |
| `retries`                                                             | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)      | :heavy_minus_sign:                                                    | Configuration to override the default retry behavior of the client.   |

### Response

**[models.Webhooks](../../models/webhooks.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## update

Turns webhook delivery on or off. Set `enabled` to `false` to pause delivery and to `true` to resume it. Endpoints and their event subscriptions are kept. Returns 404 if webhooks have never been enabled.

### Example Usage

<!-- UsageSnippet language="python" operationID="updateWebhooks" method="patch" path="/v0/webhooks" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.webhooks.update(enabled=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                     | Type                                                                                                          | Required                                                                                                      | Description                                                                                                   |
| ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| `enabled`                                                                                                     | *bool*                                                                                                        | :heavy_check_mark:                                                                                            | Whether webhooks are enabled                                                                                  |
| `merchant_id`                                                                                                 | *Optional[str]*                                                                                               | :heavy_minus_sign:                                                                                            | The merchant organization ID. If omitted, defaults to the merchant associated with the authenticated API key. |
| `retries`                                                                                                     | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                              | :heavy_minus_sign:                                                                                            | Configuration to override the default retry behavior of the client.                                           |

### Response

**[models.Webhooks](../../models/webhooks.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## disable

Pauses webhook delivery. This has the same effect as the update operation with `enabled: false`: it does not delete the configuration, the endpoints or their event subscriptions. Use the update operation with `enabled: true` to resume delivery. Returns 404 if webhooks have never been enabled.

### Example Usage

<!-- UsageSnippet language="python" operationID="deleteWebhooks" method="delete" path="/v0/webhooks" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    paygentic.webhooks.disable()

    # Use the SDK ...

```

### Parameters

| Parameter                                                             | Type                                                                  | Required                                                              | Description                                                           |
| --------------------------------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------- |
| `request`                                                             | [models.DeleteWebhooksRequest](../../models/deletewebhooksrequest.md) | :heavy_check_mark:                                                    | The request object to use for the request.                            |
| `retries`                                                             | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)      | :heavy_minus_sign:                                                    | Configuration to override the default retry behavior of the client.   |

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get_portal

Returns a link to the webhook portal, where you add endpoints, choose event types, read the signing secret and inspect deliveries. The link opens without a login and expires one hour after it is issued, at `expiresAt`. Treat it as a secret. The link is read-only unless the caller holds `webhooks:write`: a read-only portal shows endpoints and deliveries but does not let you add or change endpoints, read the signing secret or replay messages. Returns 404 unless webhooks are enabled.

### Example Usage

<!-- UsageSnippet language="python" operationID="getWebhookPortal" method="get" path="/v0/webhooks/portal" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.webhooks.get_portal()

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                 | Type                                                                      | Required                                                                  | Description                                                               |
| ------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| `request`                                                                 | [models.GetWebhookPortalRequest](../../models/getwebhookportalrequest.md) | :heavy_check_mark:                                                        | The request object to use for the request.                                |
| `retries`                                                                 | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)          | :heavy_minus_sign:                                                        | Configuration to override the default retry behavior of the client.       |

### Response

**[models.WebhookPortal](../../models/webhookportal.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403, 404                | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |