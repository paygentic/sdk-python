# Stale

Present only when the database can't be reached, or the list takes more than a second to compute. The response is then the last result for this same request in the past hour, computed at `computedAt`.


## Fields

| Field                                                                | Type                                                                 | Required                                                             | Description                                                          |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `computed_at`                                                        | [date](https://docs.python.org/3/library/datetime.html#date-objects) | :heavy_check_mark:                                                   | When this result was computed.                                       |