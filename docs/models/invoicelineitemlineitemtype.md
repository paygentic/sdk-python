# InvoiceLineItemLineItemType

Type of line item: 'charge' for regular billing, 'refund' for refunded items (amounts are negated)

## Example Usage

```python
from paygentic_sdk.models import InvoiceLineItemLineItemType

# Open enum: unrecognized values are captured as UnrecognizedStr
value: InvoiceLineItemLineItemType = "charge"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"charge"`
- `"refund"`
