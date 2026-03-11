# RuleConditionType

The type of field to evaluate

## Example Usage

```python
from paygentic_sdk.models import RuleConditionType

# Open enum: unrecognized values are captured as UnrecognizedStr
value: RuleConditionType = "date"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"date"`
- `"customerName"`
- `"customerEmail"`
- `"amount"`
