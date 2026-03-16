# PaymentSession


## Fields

| Field                                                                | Type                                                                 | Required                                                             | Description                                                          |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `url`                                                                | *str*                                                                | :heavy_check_mark:                                                   | The Stripe checkout URL for the customer to complete payment.        |
| `expires_at`                                                         | [date](https://docs.python.org/3/library/datetime.html#date-objects) | :heavy_minus_sign:                                                   | When the payment session expires.                                    |
| `amount`                                                             | *Optional[float]*                                                    | :heavy_minus_sign:                                                   | The payment amount in the currency's minor unit (e.g., cents).       |