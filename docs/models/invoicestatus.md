# InvoiceStatus

The current status of the invoice

## Example Usage

```python
from paygentic_sdk.models import InvoiceStatus

# Open enum: unrecognized values are captured as UnrecognizedStr
value: InvoiceStatus = "ACTIVE"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"ACTIVE"`
- `"CLOSING"`
- `"CLOSED"`
- `"CALCULATING"`
- `"DRAFT"`
- `"ISSUED"`
- `"PAYMENT_FAILED"`
- `"PAID"`
- `"CANCELLED"`
- `"WRITTEN_OFF"`
- `"FAILED"`
