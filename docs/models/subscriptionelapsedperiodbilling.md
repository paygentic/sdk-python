# SubscriptionElapsedPeriodBilling

Whether this subscription's backdated start bills its elapsed periods, as chosen at creation. `null` for a subscription created before the choice existed. `null` is listed in the enum as well as via `nullable` because the response validator checks the enum independently.

## Example Usage

```python
from paygentic_sdk.models import SubscriptionElapsedPeriodBilling

# Open enum: unrecognized values are captured as UnrecognizedStr
value: SubscriptionElapsedPeriodBilling = "none"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"none"`
- `"per_period"`
