# OrderTypeUnion

`recurring` is a scheduled renewal order, `checkout` the order that created the subscription, and `instant` a one-off purchase the customer made outside the schedule (an instant order) — it carries no billing cycle.


## Supported Types

### `Components\TypeCheckout`

```php
/**
* @var \Juo\AdminAPI\Models\Components\TypeCheckout
*/
Components\TypeCheckout $value = /* values here */
```

### `Components\TypeRecurring`

```php
/**
* @var \Juo\AdminAPI\Models\Components\TypeRecurring
*/
Components\TypeRecurring $value = /* values here */
```

### `Components\TypeInstant`

```php
/**
* @var \Juo\AdminAPI\Models\Components\TypeInstant
*/
Components\TypeInstant $value = /* values here */
```

