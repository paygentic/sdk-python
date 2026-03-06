# UpdateRuleRequest


## Fields

| Field                                                                  | Type                                                                   | Required                                                               | Description                                                            |
| ---------------------------------------------------------------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| `conditions`                                                           | List[[models.RuleCondition](../models/rulecondition.md)]               | :heavy_minus_sign:                                                     | List of conditions that must ALL be met (AND logic)                    |
| `description`                                                          | *Optional[str]*                                                        | :heavy_minus_sign:                                                     | Detailed description of what this source rule does                     |
| `enabled`                                                              | *Optional[bool]*                                                       | :heavy_minus_sign:                                                     | Whether this rule should be active                                     |
| `name`                                                                 | *Optional[str]*                                                        | :heavy_minus_sign:                                                     | Human-readable name for the source rule                                |
| `order`                                                                | *Optional[int]*                                                        | :heavy_minus_sign:                                                     | Priority order for rule evaluation (lower numbers are evaluated first) |