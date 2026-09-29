# PlanPriceModel

## Example Usage

```python
from paygentic_sdk.models import PlanPriceModel

# Open enum: unrecognized values are captured as UnrecognizedStr
value: PlanPriceModel = "standard"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"standard"`
- `"dynamic"`
- `"volume"`
- `"percentage"`
