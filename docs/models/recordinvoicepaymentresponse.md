# RecordInvoicePaymentResponse

The invoice is settled, or a new payment link exists. The `method` field identifies the shape: `out_of_band` returns the `PAID` invoice; `hosted_link` returns the provider and the new payment link.


## Supported Types

### `models.OutOfBandPaymentResult`

```python
value: models.OutOfBandPaymentResult = /* values here */
```

### `models.HostedLinkPaymentResult`

```python
value: models.HostedLinkPaymentResult = /* values here */
```

