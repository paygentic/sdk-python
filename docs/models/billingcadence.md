# BillingCadence

ISO 8601 duration for the billing period.

## Example Usage

```python
from paygentic_sdk.models import BillingCadence

# Open enum: unrecognized values are captured as UnrecognizedStr
value: BillingCadence = "P1M"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"P1M"`
- `"P3M"`
- `"P1Y"`
