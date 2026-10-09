# InvoicePaymentProvider

The payment provider that a hosted payment link routes to.

## Example Usage

```python
from paygentic_sdk.models import InvoicePaymentProvider

# Open enum: unrecognized values are captured as UnrecognizedStr
value: InvoicePaymentProvider = "stripe"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"stripe"`
- `"airwallex"`
