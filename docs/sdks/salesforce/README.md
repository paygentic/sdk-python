# Salesforce

## Overview

### Available Operations

* [list_salesforce_accounts](#list_salesforce_accounts) - List Salesforce accounts

## list_salesforce_accounts

Returns Accounts from the merchant's connected Salesforce org via live proxy SOQL.

### Example Usage

<!-- UsageSnippet language="python" operationID="listSalesforceAccounts" method="get" path="/v0/integrations/salesforce/accounts" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.salesforce.list_salesforce_accounts(merchant_id="<id>", limit=50, offset=0)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `merchant_id`                                                       | *str*                                                               | :heavy_check_mark:                                                  | Merchant whose Salesforce connection to use.                        |
| `q`                                                                 | *Optional[str]*                                                     | :heavy_minus_sign:                                                  | Optional name filter (LIKE match).                                  |
| `limit`                                                             | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | N/A                                                                 |
| `offset`                                                            | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.ListSalesforceAccountsResponse](../../models/listsalesforceaccountsresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 401, 403                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |