# LineCalculationNotApplied

A rule in force for the line that did not change it.


## Fields

| Field                                                                       | Type                                                                        | Required                                                                    | Description                                                                 |
| --------------------------------------------------------------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| `source`                                                                    | *str*                                                                       | :heavy_check_mark:                                                          | The key of the rule's source in `sources`.                                  |
| `reason`                                                                    | *str*                                                                       | :heavy_check_mark:                                                          | Why the rule did not change the line, for example `within` or `notBinding`. |