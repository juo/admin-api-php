# PostSubscriptionsStatus

The subscription's initial lifecycle status. Defaults to `active` if not provided. Any status except `merged` may be set, e.g. when migrating subscriptions from another platform. Creating a subscription in `canceled`, `failed`, or `expired` sets its cancellation date and skips customer notifications.


## Values

| Name       | Value      |
| ---------- | ---------- |
| `Active`   | active     |
| `Paused`   | paused     |
| `Canceled` | canceled   |
| `Failed`   | failed     |
| `Expired`  | expired    |