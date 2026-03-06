# RuleConditionType

The type of field to evaluate

## Example Usage

```python
from paygentic_sdk.models import RuleConditionType

# Open enum: unrecognized values are captured as UnrecognizedStr
value: RuleConditionType = "date"
```


## Values

| Name             | Value            |
| ---------------- | ---------------- |
| `DATE`           | date             |
| `CUSTOMER_NAME`  | customerName     |
| `CUSTOMER_EMAIL` | customerEmail    |
| `AMOUNT`         | amount           |