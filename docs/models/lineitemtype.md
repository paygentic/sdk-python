# LineItemType

The type of line item. 'discount' and 'adjustment' line items have negative subtotal/total amounts: 'discount' is a grant discount, 'adjustment' is a discount agreed on the subscription.

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
- `"adjustment"`
