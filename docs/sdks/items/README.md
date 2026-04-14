# Items
(*subscriptions->items*)

## Overview

### Available Operations

* [create](#create) - Creates a subscription item
* [delete](#delete) - Deletes a subscription item
* [update](#update) - Updates a subscription item

## create

Creates a subscription item

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/subscriptions/{subscriptionId}/items" method="post" path="/subscriptions/{subscriptionId}/items" -->
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Juo\AdminAPI;
use Juo\AdminAPI\Models\Operations;

$sdk = AdminAPI\Juo::builder()
    ->setTenant('<value>')
    ->setSecurity(
        '<YOUR_API_KEY_HERE>'
    )
    ->build();

$requestBody = new Operations\PostSubscriptionsSubscriptionIdItemsRequestBody(
    variant: '<value>',
    quantity: 502841,
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

## delete

Deletes a subscription item

### Example Usage

<!-- UsageSnippet language="php" operationID="delete_/subscriptions/{subscriptionId}/items/{itemId}" method="delete" path="/subscriptions/{subscriptionId}/items/{itemId}" -->
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Juo\AdminAPI;

$sdk = AdminAPI\Juo::builder()
    ->setTenant('<value>')
    ->setSecurity(
        '<YOUR_API_KEY_HERE>'
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

## update

Updates a subscription item

### Example Usage

<!-- UsageSnippet language="php" operationID="patch_/subscriptions/{subscriptionId}/items/{itemId}" method="patch" path="/subscriptions/{subscriptionId}/items/{itemId}" -->
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Juo\AdminAPI;

$sdk = AdminAPI\Juo::builder()
    ->setTenant('<value>')
    ->setSecurity(
        '<YOUR_API_KEY_HERE>'
    )
    ->build();



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