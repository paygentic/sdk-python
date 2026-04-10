# LineItemType

The type of line item. 'discount' line items represent grant discounts with negative subtotal/total amounts.

## Example Usage

```python
from paygentic_sdk.models import LineItemType

# Open enum: unrecognized values are captured as UnrecognizedStr
value: LineItemType = "fee"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"fee"`
- `"metered"`
- `"manual"`
- `"discount"`
