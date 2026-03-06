# Sources.Rules

## Overview

### Available Operations

* [list](#list) - List Rules
* [create](#create) - Create Rule
* [get](#get) - Get Rule
* [update](#update) - Update Rule
* [delete](#delete) - Delete Rule

## list

List all auto-acceptance rules for a source. These rules automatically approve pending source events when all conditions are met.

### Example Usage

<!-- UsageSnippet language="python" operationID="listSourceRules" method="get" path="/v0/sourceRules" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.sources.rules.list(source_id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `source_id`                                                         | *str*                                                               | :heavy_check_mark:                                                  | Filter rules by source ID                                           |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.ListSourceRulesResponse](../../models/listsourcerulesresponse.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## create

Create a rule for automatically approving source events. When a pending source event matches ALL conditions in a rule, it will be automatically approved and converted to a usage event. Rules are evaluated in order (lowest order number first), and the first matching rule triggers auto-approval. Maximum 10 rules per source.

### Example Usage

<!-- UsageSnippet language="python" operationID="createSourceRule" method="post" path="/v0/sourceRules" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.sources.rules.create(conditions=[], name="<value>", source_id="<id>", enabled=True, order=0)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                                             | Type                                                                                                                                                                                                                                                                                  | Required                                                                                                                                                                                                                                                                              | Description                                                                                                                                                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `conditions`                                                                                                                                                                                                                                                                          | List[[models.RuleCondition](../../models/rulecondition.md)]                                                                                                                                                                                                                           | :heavy_check_mark:                                                                                                                                                                                                                                                                    | Conditions that must ALL be met (AND logic) for auto-acceptance. Sample values: customerEmail domain='@trusted.com' AND amount lessThan=1000, customerId equals='org_abc123' AND billableMetricId equals='bm_tokens', subscriptionId equals='sub_xyz789' AND quantity greaterThan=100 |
| `name`                                                                                                                                                                                                                                                                                | *str*                                                                                                                                                                                                                                                                                 | :heavy_check_mark:                                                                                                                                                                                                                                                                    | Human-readable name for the source rule                                                                                                                                                                                                                                               |
| `source_id`                                                                                                                                                                                                                                                                           | *str*                                                                                                                                                                                                                                                                                 | :heavy_check_mark:                                                                                                                                                                                                                                                                    | Unique identifier for a source                                                                                                                                                                                                                                                        |
| `description`                                                                                                                                                                                                                                                                         | *Optional[str]*                                                                                                                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                                                                                    | Detailed description of what this source rule does                                                                                                                                                                                                                                    |
| `enabled`                                                                                                                                                                                                                                                                             | *Optional[bool]*                                                                                                                                                                                                                                                                      | :heavy_minus_sign:                                                                                                                                                                                                                                                                    | Whether this rule should be active immediately                                                                                                                                                                                                                                        |
| `order`                                                                                                                                                                                                                                                                               | *Optional[int]*                                                                                                                                                                                                                                                                       | :heavy_minus_sign:                                                                                                                                                                                                                                                                    | Evaluation priority (0-999). Lower numbers are evaluated first. First matching rule triggers auto-acceptance.                                                                                                                                                                         |
| `retries`                                                                                                                                                                                                                                                                             | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                                      | :heavy_minus_sign:                                                                                                                                                                                                                                                                    | Configuration to override the default retry behavior of the client.                                                                                                                                                                                                                   |

### Response

**[models.SourceRule](../../models/sourcerule.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## get

Get Rule

### Example Usage

<!-- UsageSnippet language="python" operationID="getSourceRule" method="get" path="/v0/sourceRules/{ruleId}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.sources.rules.get(rule_id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `rule_id`                                                           | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.SourceRule](../../models/sourcerule.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## update

Update Rule

### Example Usage

<!-- UsageSnippet language="python" operationID="updateSourceRule" method="patch" path="/v0/sourceRules/{ruleId}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.sources.rules.update(rule_id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                              | Type                                                                   | Required                                                               | Description                                                            |
| ---------------------------------------------------------------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| `rule_id`                                                              | *str*                                                                  | :heavy_check_mark:                                                     | N/A                                                                    |
| `conditions`                                                           | List[[models.RuleCondition](../../models/rulecondition.md)]            | :heavy_minus_sign:                                                     | List of conditions that must ALL be met (AND logic)                    |
| `description`                                                          | *Optional[str]*                                                        | :heavy_minus_sign:                                                     | Detailed description of what this source rule does                     |
| `enabled`                                                              | *Optional[bool]*                                                       | :heavy_minus_sign:                                                     | Whether this rule should be active                                     |
| `name`                                                                 | *Optional[str]*                                                        | :heavy_minus_sign:                                                     | Human-readable name for the source rule                                |
| `order`                                                                | *Optional[int]*                                                        | :heavy_minus_sign:                                                     | Priority order for rule evaluation (lower numbers are evaluated first) |
| `retries`                                                              | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)       | :heavy_minus_sign:                                                     | Configuration to override the default retry behavior of the client.    |

### Response

**[models.SourceRule](../../models/sourcerule.md)**

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |

## delete

Delete Rule

### Example Usage

<!-- UsageSnippet language="python" operationID="deleteSourceRule" method="delete" path="/v0/sourceRules/{ruleId}" -->
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    paygentic.sources.rules.delete(rule_id="<id>")

    # Use the SDK ...

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `rule_id`                                                           | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Errors

| Error Type                   | Status Code                  | Content Type                 |
| ---------------------------- | ---------------------------- | ---------------------------- |
| errors.Error                 | 400                          | application/json             |
| errors.ValidationError       | 400                          | application/json             |
| errors.Error                 | 403, 404                     | application/json             |
| errors.Error                 | 500                          | application/json             |
| errors.PaygenticDefaultError | 4XX, 5XX                     | \*/\*                        |