# Operator

The comparison operator to use

## Example Usage

```python
from paygentic_sdk.models import Operator

# Open enum: unrecognized values are captured as UnrecognizedStr
value: Operator = "equals"
```


## Values

| Name           | Value          |
| -------------- | -------------- |
| `EQUALS`       | equals         |
| `CONTAINS`     | contains       |
| `BETWEEN`      | between        |
| `GREATER_THAN` | greaterThan    |
| `LESS_THAN`    | lessThan       |
| `DOMAIN`       | domain         |