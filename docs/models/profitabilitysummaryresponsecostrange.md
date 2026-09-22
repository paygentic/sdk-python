# ProfitabilitySummaryResponseCostRange

Where the caller's cost data actually lies in time. Present only when the selected range returned no cost. An object carries the bounds of the real cost events; null means the caller has no cost event at any time; an absent field means the extent was not resolved, because the result was not empty, because the lookup failed, or because the metering service does not serve the bounds method. An absent field must never be read as an absence.


## Fields

| Field                                                                | Type                                                                 | Required                                                             | Description                                                          |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `from_`                                                              | [date](https://docs.python.org/3/library/datetime.html#date-objects) | :heavy_check_mark:                                                   | Earliest cost event instant.                                         |
| `to`                                                                 | [date](https://docs.python.org/3/library/datetime.html#date-objects) | :heavy_check_mark:                                                   | Latest cost event instant.                                           |