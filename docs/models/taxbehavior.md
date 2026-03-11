# TaxBehavior

Whether tax is added on top of the price (exclusive) or included in the price (inclusive)

## Example Usage

```python
from paygentic_sdk.models import TaxBehavior

# Open enum: unrecognized values are captured as UnrecognizedStr
value: TaxBehavior = "exclusive"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"exclusive"`
- `"inclusive"`
