# InvoicePaymentLinkErrorCode

Why Paygentic cannot create a payment link for the invoice.

## Example Usage

```python
from paygentic_sdk.models import InvoicePaymentLinkErrorCode

# Open enum: unrecognized values are captured as UnrecognizedStr
value: InvoicePaymentLinkErrorCode = "INVOICE_NOT_LINKABLE_STATUS"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"INVOICE_NOT_LINKABLE_STATUS"`
- `"INVOICE_NO_BALANCE"`
- `"MERCHANT_NO_PAYMENT_ACCOUNT"`
