# Operator

The comparison operator to use

## Example Usage

```python
from paygentic_sdk.models import Operator

# Open enum: unrecognized values are captured as UnrecognizedStr
value: Operator = "equals"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"equals"`
- `"contains"`
- `"between"`
- `"greaterThan"`
- `"lessThan"`
- `"domain"`
