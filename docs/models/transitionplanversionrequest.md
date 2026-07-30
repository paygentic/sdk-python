# TransitionPlanVersionRequest

Sets this version as the plan's default.


## Fields

| Field                                                                                               | Type                                                                                                | Required                                                                                            | Description                                                                                         |
| --------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| `default`                                                                                           | *Optional[bool]*                                                                                    | :heavy_minus_sign:                                                                                  | Set to true to point the plan's default at this version. Idempotent on the already-default version. |