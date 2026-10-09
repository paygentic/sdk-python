# RetryPaymentError

Why a payment retry did not collect the money.


## Fields

| Field                                                                  | Type                                                                   | Required                                                               | Description                                                            |
| ---------------------------------------------------------------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| `message`                                                              | *str*                                                                  | :heavy_check_mark:                                                     | Human-readable message. Do not parse it; use `code`.                   |
| `type`                                                                 | *Optional[str]*                                                        | :heavy_minus_sign:                                                     | Error category, for example `card_error` or `processing`.              |
| `code`                                                                 | *Optional[str]*                                                        | :heavy_minus_sign:                                                     | Machine-readable reason. See the operation description for the values. |
| `decline_code`                                                         | *Optional[str]*                                                        | :heavy_minus_sign:                                                     | The card decline code from the provider, when one is available.        |