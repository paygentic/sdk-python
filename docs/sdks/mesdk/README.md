# Me

## Overview

The caller: who it is in its active organization and what it can do

### Available Operations

* [get_me](#get_me) - Get the caller

## get_me

Returns the caller's identity in its active organization, its roles, and the permissions that its credential holds there. The permissions are the effective set for the credential of the call: for a session or an API key, those of the principal; for an OAuth token, those of the principal narrowed to the scopes of the token.

### Example Usage

<!-- UsageSnippet language="python" operationID="getMe" method="get" path="/v0/me" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.me.get_me()

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.Me](../../models/me.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 401, 403                     | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |