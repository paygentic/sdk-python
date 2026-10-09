# CostData

Whether metering recorded usage against a cost for every customer the row covers (`recorded`), some of them (`partial`, only on the 'Other' and 'deleted' rows) or none (`none`). Usage that prices at zero is recorded, so `recorded` with a zero `totalCost` is a measured zero. `none` means no cost data, not a zero cost.

## Example Usage

```python
from paygentic_sdk.models import CostData

# Open enum: unrecognized values are captured as UnrecognizedStr
value: CostData = "recorded"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"recorded"`
- `"partial"`
- `"none"`
