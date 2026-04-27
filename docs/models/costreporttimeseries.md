# CostReportTimeSeries


## Fields

| Field                                                                               | Type                                                                                | Required                                                                            | Description                                                                         |
| ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| `window_start`                                                                      | [date](https://docs.python.org/3/library/datetime.html#date-objects)                | :heavy_check_mark:                                                                  | N/A                                                                                 |
| `window_end`                                                                        | [date](https://docs.python.org/3/library/datetime.html#date-objects)                | :heavy_check_mark:                                                                  | N/A                                                                                 |
| `groups`                                                                            | Dict[str, *float*]                                                                  | :heavy_check_mark:                                                                  | Map of group key → cost value for this time window. Keys match CostReportGroup.key. |