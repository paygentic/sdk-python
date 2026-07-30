# PlanVersionStatus

Lifecycle status of the version.

## Example Usage

```python
from paygentic_sdk.models import PlanVersionStatus

# Open enum: unrecognized values are captured as UnrecognizedStr
value: PlanVersionStatus = "draft"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"draft"`
- `"published"`
- `"archived"`
