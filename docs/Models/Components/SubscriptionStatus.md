# SubscriptionStatus

Subscription lifecycle status. `active`: billing runs on schedule; `paused`: billing suspended until resumed; `canceled`: permanently stopped (can be reactivated); `failed`: latest billing attempt failed; `expired`: reached configured end date; `merged`: consolidated into another subscription.


## Values

| Name       | Value      |
| ---------- | ---------- |
| `Active`   | active     |
| `Paused`   | paused     |
| `Canceled` | canceled   |
| `Failed`   | failed     |
| `Expired`  | expired    |
| `Merged`   | merged     |