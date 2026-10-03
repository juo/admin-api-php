# Subscriptions.Items

## Overview

### Available Operations

* [create](#create) - Add an item to a subscription
* [update](#update) - Update a subscription item
* [delete](#delete) - Remove a subscription item

## create

Adds a new subscription item (product variant) to a subscription. Optionally set a custom base price (applied before subscription discounts), quantity, and a recurring cycle limit (how many billing cycles the item appears). The variant must be part of a subscription plan.

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/subscriptions/{subscriptionId}/items" method="post" path="/subscriptions/{subscriptionId}/items" -->
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Juo\AdminAPI;
use Juo\AdminAPI\Models\Components;
use Juo\AdminAPI\Models\Operations;

$sdk = AdminAPI\Juo::builder()
    ->setTenant('<value>')
    ->setSecurity(
        new Components\Security(
            adminApiKey: '<YOUR_API_KEY_HERE>',
        )
    )
    ->build();

$requestBody = new Operations\PostSubscriptionsSubscriptionIdItemsRequestBody(
    variant: '<value>',
    quantity: 502841,
    recurringCycleLimit: 3,
);

$response = $sdk->subscriptions->items->create(
    subscriptionId: 'ca8e5a5e-6c71-41c5-bf47-344a1c6193b5',
    requestBody: $requestBody

);

if ($response->subscriptionItem !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                                | Type                                                                                                                                     | Required                                                                                                                                 | Description                                                                                                                              |
| ---------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| `subscriptionId`                                                                                                                         | *string*                                                                                                                                 | :heavy_check_mark:                                                                                                                       | The subscription identifier                                                                                                              |
| `requestBody`                                                                                                                            | [Operations\PostSubscriptionsSubscriptionIdItemsRequestBody](../../Models/Operations/PostSubscriptionsSubscriptionIdItemsRequestBody.md) | :heavy_check_mark:                                                                                                                       | N/A                                                                                                                                      |
| `tenant`                                                                                                                                 | *?string*                                                                                                                                | :heavy_minus_sign:                                                                                                                       | Unique identifier of the tenant in the system (usually a store identifier)                                                               |

### Response

**[?Operations\PostSubscriptionsSubscriptionIdItemsResponse](../../Models/Operations/PostSubscriptionsSubscriptionIdItemsResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## update

Updates a specific subscription item using merge-patch semantics. Can change the quantity, billing policy, or delivery policy for that item independently of subscription-level policies.

### Example Usage

<!-- UsageSnippet language="php" operationID="patch_/subscriptions/{subscriptionId}/items/{itemId}" method="patch" path="/subscriptions/{subscriptionId}/items/{itemId}" -->
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Juo\AdminAPI;
use Juo\AdminAPI\Models\Components;
use Juo\AdminAPI\Models\Operations;

$sdk = AdminAPI\Juo::builder()
    ->setTenant('<value>')
    ->setSecurity(
        new Components\Security(
            adminApiKey: '<YOUR_API_KEY_HERE>',
        )
    )
    ->build();

$requestBody = new Operations\PatchSubscriptionsSubscriptionIdItemsItemIdRequestBody(
    quantity: 1,
);

$response = $sdk->subscriptions->items->update(
    subscriptionId: 'd2b28517-0fd5-4981-943b-556135fbb598',
    itemId: 'e3ab8a07-6e97-42fc-b919-54c29a4fcde2',
    requestBody: $requestBody

);

if ($response->subscriptionItem !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                                               | Type                                                                                                                                                    | Required                                                                                                                                                | Description                                                                                                                                             |
| ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `subscriptionId`                                                                                                                                        | *string*                                                                                                                                                | :heavy_check_mark:                                                                                                                                      | The subscription identifier                                                                                                                             |
| `itemId`                                                                                                                                                | *string*                                                                                                                                                | :heavy_check_mark:                                                                                                                                      | The subscription item identifier                                                                                                                        |
| `tenant`                                                                                                                                                | *?string*                                                                                                                                               | :heavy_minus_sign:                                                                                                                                      | Unique identifier of the tenant in the system (usually a store identifier)                                                                              |
| `requestBody`                                                                                                                                           | [?Operations\PatchSubscriptionsSubscriptionIdItemsItemIdRequestBody](../../Models/Operations/PatchSubscriptionsSubscriptionIdItemsItemIdRequestBody.md) | :heavy_minus_sign:                                                                                                                                      | N/A                                                                                                                                                     |

### Response

**[?Operations\PatchSubscriptionsSubscriptionIdItemsItemIdResponse](../../Models/Operations/PatchSubscriptionsSubscriptionIdItemsItemIdResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## delete

Removes an item from a subscription. The subscription must retain at least one item after removal. This is a permanent change affecting all future billing cycles.

### Example Usage

<!-- UsageSnippet language="php" operationID="delete_/subscriptions/{subscriptionId}/items/{itemId}" method="delete" path="/subscriptions/{subscriptionId}/items/{itemId}" -->
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Juo\AdminAPI;
use Juo\AdminAPI\Models\Components;

$sdk = AdminAPI\Juo::builder()
    ->setTenant('<value>')
    ->setSecurity(
        new Components\Security(
            adminApiKey: '<YOUR_API_KEY_HERE>',
        )
    )
    ->build();



$response = $sdk->subscriptions->items->delete(
    subscriptionId: '81c9d54c-c277-4d1d-812d-94a6a95ba086',
    itemId: 'e38ac163-dc12-446c-8862-ae6640967cac'

);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `subscriptionId`                                                           | *string*                                                                   | :heavy_check_mark:                                                         | The subscription identifier                                                |
| `itemId`                                                                   | *string*                                                                   | :heavy_check_mark:                                                         | The subscription item identifier                                           |
| `tenant`                                                                   | *?string*                                                                  | :heavy_minus_sign:                                                         | Unique identifier of the tenant in the system (usually a store identifier) |

### Response

**[?Operations\DeleteSubscriptionsSubscriptionIdItemsItemIdResponse](../../Models/Operations/DeleteSubscriptionsSubscriptionIdItemsItemIdResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |