# PeriodBasis

How relative periods are defined. 'calendar' (default): period N = N calendar grains after the anchor. 'order_sequence': period N = billing-order number (1-based; N=1 = initial purchase, N=2 = first renewal, etc.).


## Supported Types

### `Operations\PeriodBasisCalendar`

```php
/**
* @var \Juo\AdminAPI\Models\Operations\PeriodBasisCalendar
*/
Operations\PeriodBasisCalendar $value = /* values here */
```

### `Operations\PeriodBasisOrderSequence`

```php
/**
* @var \Juo\AdminAPI\Models\Operations\PeriodBasisOrderSequence
*/
Operations\PeriodBasisOrderSequence $value = /* values here */
```

