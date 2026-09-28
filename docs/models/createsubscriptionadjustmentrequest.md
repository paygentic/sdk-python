# CreateSubscriptionAdjustmentRequest

One adjustment to attach to the subscription. The type decides which number the body carries: a rate for percentageDiscount, a unit count and one target price for usageDiscount, and a contracted quantity and one target price for minimumQuantity and maximumQuantity.


## Supported Types

### `models.CreatePercentageDiscountAdjustment`

```python
value: models.CreatePercentageDiscountAdjustment = /* values here */
```

### `models.CreateUsageDiscountAdjustment`

```python
value: models.CreateUsageDiscountAdjustment = /* values here */
```

### `models.CreateMinimumQuantityAdjustment`

```python
value: models.CreateMinimumQuantityAdjustment = /* values here */
```

### `models.CreateMaximumQuantityAdjustment`

```python
value: models.CreateMaximumQuantityAdjustment = /* values here */
```

