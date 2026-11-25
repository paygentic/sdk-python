# GetCreditPoolLedgerResponse

Pool ledger for the requested window. The shape depends on whether `granularity` was set: unset returns itemized `entries`, set returns rolled-up `buckets`.


## Supported Types

### `models.CreditPoolLedgerItemizedResponse`

```python
value: models.CreditPoolLedgerItemizedResponse = /* values here */
```

### `models.CreditPoolLedgerBucketedResponse`

```python
value: models.CreditPoolLedgerBucketedResponse = /* values here */
```

