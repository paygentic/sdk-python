# TaxBehavior

Whether tax is added on top of the price (exclusive) or included in the price (inclusive)

## Example Usage

```python
from paygentic_sdk.models import TaxBehavior

# Open enum: unrecognized values are captured as UnrecognizedStr
value: TaxBehavior = "exclusive"
```


## Values

| Name        | Value       |
| ----------- | ----------- |
| `EXCLUSIVE` | exclusive   |
| `INCLUSIVE` | inclusive   |