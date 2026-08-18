# MerchantIntegrationProvider

External provider a merchant can connect at the tenant level. `netsuite` and `accountsiq` are returned on reads wherever a connection exists, but connecting them is accepted only in local and development environments; elsewhere the connect request is refused with 404.

## Example Usage

```python
from paygentic_sdk.models import MerchantIntegrationProvider

# Open enum: unrecognized values are captured as UnrecognizedStr
value: MerchantIntegrationProvider = "salesforce"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"salesforce"`
- `"netsuite"`
- `"accountsiq"`
