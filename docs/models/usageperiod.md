# UsagePeriod


## Fields

| Field                                                                | Type                                                                 | Required                                                             | Description                                                          |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `interval`                                                           | *str*                                                                | :heavy_check_mark:                                                   | ISO 8601 duration for the usage period, e.g. P1D, P1W, P1M, P1Y.     |
| `anchor`                                                             | [date](https://docs.python.org/3/library/datetime.html#date-objects) | :heavy_minus_sign:                                                   | Optional anchor date-time for period alignment.                      |