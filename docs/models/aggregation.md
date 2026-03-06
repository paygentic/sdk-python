# Aggregation

## Example Usage

```python
from paygentic_sdk.models import Aggregation

# Open enum: unrecognized values are captured as UnrecognizedStr
value: Aggregation = "SUM"
```


## Values

| Name           | Value          |
| -------------- | -------------- |
| `SUM`          | SUM            |
| `COUNT`        | COUNT          |
| `AVG`          | AVG            |
| `MIN`          | MIN            |
| `MAX`          | MAX            |
| `UNIQUE_COUNT` | UNIQUE_COUNT   |
| `LATEST`       | LATEST         |