# Discounts
(*subscriptions->discounts*)

## Overview

### Available Operations

* [create](#create) - Creates a subscription discount
* [delete](#delete) - Deletes a subscription discount
* [update](#update) - Updates a subscription discount

## create

Creates a subscription discount

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/subscriptions/{subscriptionId}/discounts" method="post" path="/subscriptions/{subscriptionId}/discounts" -->
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



$response = $sdk->subscriptions->discounts->create(
    subscriptionId: '85a88783-c359-4b1f-9022-f6129ffd6b86'
);

if ($response->subscriptionDiscount !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                              | Type                                                                                                                                   | Required                                                                                                                               | Description                                                                                                                            |
| -------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `subscriptionId`                                                                                                                       | *string*                                                                                                                               | :heavy_check_mark:                                                                                                                     | The subscription identifier                                                                                                            |
| `tenant`                                                                                                                               | *?string*                                                                                                                              | :heavy_minus_sign:                                                                                                                     | Unique identifier of the tenant in the system (usually a store identifier)                                                             |
| `requestBody`                                                                                                                          | [Operations\RequestBody1\|Operations\RequestBody2\|null](../../Models/Operations/PostSubscriptionsSubscriptionIdDiscountsRequestBody.md) | :heavy_minus_sign:                                                                                                                     | N/A                                                                                                                                    |

### Response

**[?Operations\PostSubscriptionsSubscriptionIdDiscountsResponse](../../Models/Operations/PostSubscriptionsSubscriptionIdDiscountsResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## delete

Deletes a subscription discount

### Example Usage

<!-- UsageSnippet language="php" operationID="delete_/subscriptions/{subscriptionId}/discounts/{discountId}" method="delete" path="/subscriptions/{subscriptionId}/discounts/{discountId}" -->
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



$response = $sdk->subscriptions->discounts->delete(
    subscriptionId: 'ac6dd669-8cde-409f-a4e1-085aeeaf246a',
    discountId: '47ba2170-98b0-4a13-9e2e-7f9e2228a739'

);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `subscriptionId`                                                           | *string*                                                                   | :heavy_check_mark:                                                         | The subscription identifier                                                |
| `discountId`                                                               | *string*                                                                   | :heavy_check_mark:                                                         | The subscription discount identifier                                       |
| `tenant`                                                                   | *?string*                                                                  | :heavy_minus_sign:                                                         | Unique identifier of the tenant in the system (usually a store identifier) |

### Response

**[?Operations\DeleteSubscriptionsSubscriptionIdDiscountsDiscountIdResponse](../../Models/Operations/DeleteSubscriptionsSubscriptionIdDiscountsDiscountIdResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## update

Updates a subscription discount

### Example Usage

<!-- UsageSnippet language="php" operationID="patch_/subscriptions/{subscriptionId}/discounts/{discountId}" method="patch" path="/subscriptions/{subscriptionId}/discounts/{discountId}" -->
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



$response = $sdk->subscriptions->discounts->update(
    subscriptionId: '5b7f7c26-a817-4867-babd-ad1e81d4c949',
    discountId: 'b24f6aa0-fd16-4eb8-b9c7-64abe8da97d5',
    requestBody: $requestBody

);

if ($response->subscriptionDiscount !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                                                               | Type                                                                                                                                                                    | Required                                                                                                                                                                | Description                                                                                                                                                             |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `subscriptionId`                                                                                                                                                        | *string*                                                                                                                                                                | :heavy_check_mark:                                                                                                                                                      | The subscription identifier                                                                                                                                             |
| `discountId`                                                                                                                                                            | *string*                                                                                                                                                                | :heavy_check_mark:                                                                                                                                                      | The subscription discount identifier                                                                                                                                    |
| `tenant`                                                                                                                                                                | *?string*                                                                                                                                                               | :heavy_minus_sign:                                                                                                                                                      | Unique identifier of the tenant in the system (usually a store identifier)                                                                                              |
| `requestBody`                                                                                                                                                           | [?Operations\PatchSubscriptionsSubscriptionIdDiscountsDiscountIdRequestBody](../../Models/Operations/PatchSubscriptionsSubscriptionIdDiscountsDiscountIdRequestBody.md) | :heavy_minus_sign:                                                                                                                                                      | N/A                                                                                                                                                                     |

### Response

**[?Operations\PatchSubscriptionsSubscriptionIdDiscountsDiscountIdResponse](../../Models/Operations/PatchSubscriptionsSubscriptionIdDiscountsDiscountIdResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |