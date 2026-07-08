# PriceModel

Pricing model of a price as returned by the API. Includes legacy models ('dynamic', 'volume', 'percentage') retained for existing prices; only 'standard' can be created (see PriceModelInput).

## Example Usage

```python
from paygentic_sdk.models import PriceModel

# Open enum: unrecognized values are captured as UnrecognizedStr
value: PriceModel = "standard"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"standard"`
- `"dynamic"`
- `"volume"`
- `"percentage"`
