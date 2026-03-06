# EntitlementTemplateMetered


## Fields

| Field                                                        | Type                                                         | Required                                                     | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `type`                                                       | *Literal["metered"]*                                         | :heavy_check_mark:                                           | N/A                                                          |
| `usage_period`                                               | [models.UsagePeriod](../models/usageperiod.md)               | :heavy_check_mark:                                           | N/A                                                          |
| `is_soft_limit`                                              | *Optional[bool]*                                             | :heavy_minus_sign:                                           | When true, access is granted even when balance is exhausted. |
| `issue_after_reset`                                          | *Optional[float]*                                            | :heavy_minus_sign:                                           | Amount of grants to issue after each period reset.           |
| `issue_after_reset_priority`                                 | *Optional[int]*                                              | :heavy_minus_sign:                                           | Priority for grants issued after reset.                      |
| `preserve_overage_at_reset`                                  | *Optional[bool]*                                             | :heavy_minus_sign:                                           | When true, overage from the previous period carries over.    |
| `reset_max_rollover`                                         | *Optional[float]*                                            | :heavy_minus_sign:                                           | Maximum amount of unused balance that rolls over on reset.   |
| `reset_min_rollover`                                         | *Optional[float]*                                            | :heavy_minus_sign:                                           | Minimum amount of balance guaranteed to roll over on reset.  |