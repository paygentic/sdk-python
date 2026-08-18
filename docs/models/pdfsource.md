# PdfSource

Who produced the document at pdfUrl, or null when there is none. `paygentic` means pdfUrl is this API's download endpoint and the request must carry your API key; `tax_provider` means it is the provider's own link, which opens directly in a browser.

## Example Usage

```python
from paygentic_sdk.models import PdfSource

# Open enum: unrecognized values are captured as UnrecognizedStr
value: PdfSource = "paygentic"
```


## Values

This is an open enum. Unrecognized values will not fail type checks.

- `"paygentic"`
- `"tax_provider"`
