# InvoiceStatus

The current status of the invoice

## Example Usage

```python
from paygentic_sdk.models import InvoiceStatus

# Open enum: unrecognized values are captured as UnrecognizedStr
value: InvoiceStatus = "ACTIVE"
```


## Values

| Name             | Value            |
| ---------------- | ---------------- |
| `ACTIVE`         | ACTIVE           |
| `CLOSING`        | CLOSING          |
| `CLOSED`         | CLOSED           |
| `CALCULATING`    | CALCULATING      |
| `DRAFT`          | DRAFT            |
| `ISSUED`         | ISSUED           |
| `PAYMENT_FAILED` | PAYMENT_FAILED   |
| `PAID`           | PAID             |
| `CANCELLED`      | CANCELLED        |
| `WRITTEN_OFF`    | WRITTEN_OFF      |
| `FAILED`         | FAILED           |