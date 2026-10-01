# ListIntervalChangesRequest


## Fields

| Field                                                                | Type                                                                 | Required                                                             | Description                                                          |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `limit`                                                              | *Optional[str]*                                                      | :heavy_minus_sign:                                                   | Number of interval changes to return                                 |
| `offset`                                                             | *Optional[str]*                                                      | :heavy_minus_sign:                                                   | Number of interval changes to skip                                   |
| `from_`                                                              | [date](https://docs.python.org/3/library/datetime.html#date-objects) | :heavy_minus_sign:                                                   | Only return changes recorded at or after this time                   |
| `to`                                                                 | [date](https://docs.python.org/3/library/datetime.html#date-objects) | :heavy_minus_sign:                                                   | Only return changes recorded before this time                        |
| `change_reason`                                                      | [Optional[models.ChangeReason]](../models/changereason.md)           | :heavy_minus_sign:                                                   | Only return changes with this reason.                                |