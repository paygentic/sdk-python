# CostAggregation

## Example Usage

```python
from paygentic_sdk.models import CostAggregation

# Open enum: unrecognized values are captured as UnrecognizedStr
value: CostAggregation = "SUM"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"SUM"`
- `"COUNT"`
- `"AVG"`
- `"MIN"`
- `"MAX"`
- `"UNIQUE_COUNT"`
- `"LATEST"`
