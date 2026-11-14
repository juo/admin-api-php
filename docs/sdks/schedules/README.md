# Schedules

## Overview

Read-only view of upcoming billing orders generated from subscription state, schedule adjustments, and workflows. Use schedule adjustments for targeted changes to upcoming orders (scoped by cycle number, date, or both) — they never alter the subscription itself. For permanent changes (billing frequency, items, payment method), update the subscription directly.

### Available Operations

* [list](#list) - List schedule orders
* [listAdjustments](#listadjustments) - List schedule adjustments
* [create](#create) - Create a schedule adjustment
* [delete](#delete) - Delete a schedule adjustment

## list

Returns a projection of upcoming billing orders for a customer, derived from their subscription state, active schedule adjustments, and triggered workflows. Shows what orders will be generated and when. Use `count` to control how many upcoming orders to return. This is a read-only view — it does not modify subscriptions.

### Example Usage

<!-- UsageSnippet language="php" operationID="get_/schedules/" method="get" path="/schedules/" -->
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

$request = new Operations\GetSchedulesRequest(
    customerId: '<id>',
    count: 168523,
);

$response = $sdk->schedules->list(
    request: $request
);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                        | Type                                                                             | Required                                                                         | Description                                                                      |
| -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `$request`                                                                       | [Operations\GetSchedulesRequest](../../Models/Operations/GetSchedulesRequest.md) | :heavy_check_mark:                                                               | The request object to use for the request.                                       |

### Response

**[?Operations\GetSchedulesResponse](../../Models/Operations/GetSchedulesResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## listAdjustments

Returns a paginated list of schedule adjustments. A schedule adjustment applies a targeted modification to upcoming orders matching the specified criteria (by cycle number, date, or both) — it never modifies the subscription itself. For permanent changes (billing frequency, items, payment method), update the subscription directly. Results are cursor-paginated.

### Example Usage

<!-- UsageSnippet language="php" operationID="get_/schedules/adjustments" method="get" path="/schedules/adjustments" -->
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

$request = new Operations\GetSchedulesAdjustmentsRequest(
    customerId: '<id>',
);

$responses = $sdk->schedules->listAdjustments(
    request: $request
);


foreach ($responses as $response) {
    if ($response->statusCode === 200) {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                              | Type                                                                                                   | Required                                                                                               | Description                                                                                            |
| ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ |
| `$request`                                                                                             | [Operations\GetSchedulesAdjustmentsRequest](../../Models/Operations/GetSchedulesAdjustmentsRequest.md) | :heavy_check_mark:                                                                                     | The request object to use for the request.                                                             |

### Response

**[?Operations\GetSchedulesAdjustmentsResponse](../../Models/Operations/GetSchedulesAdjustmentsResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## create

Creates a modification to upcoming orders matched by cycle number, date, or both. Adjustments can match a single order or a range of orders depending on the matcher criteria. This does NOT change the subscription — it only affects the matched upcoming order(s). Supported types: skip order, change date, update shipping address or method, change payment method, modify products (add/remove/change quantity), or apply a discount. For permanent changes, update the subscription directly.

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/schedules/adjustments" method="post" path="/schedules/adjustments" -->
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

$requestBody = new Operations\PostSchedulesAdjustmentsRequestBody(
    customerId: '<id>',
    matcher: new Operations\MatcherCycle(
        type: Operations\TypeCycle::Cycle,
        input: new Operations\MatcherInput1(
            cycle: 734289,
        ),
    ),
    action: new Operations\ActionUpdateProducts(
        type: Operations\TypeUpdateProducts::UpdateProducts,
        input: new Operations\ActionInput6(
            lines: [
                new Operations\Line(
                    lineId: '<id>',
                ),
            ],
        ),
    ),
);

$response = $sdk->schedules->create(
    requestBody: $requestBody
);

if ($response->scheduleAdjustment !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                        | Type                                                                                                             | Required                                                                                                         | Description                                                                                                      |
| ---------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| `requestBody`                                                                                                    | [Operations\PostSchedulesAdjustmentsRequestBody](../../Models/Operations/PostSchedulesAdjustmentsRequestBody.md) | :heavy_check_mark:                                                                                               | N/A                                                                                                              |
| `tenant`                                                                                                         | *?string*                                                                                                        | :heavy_minus_sign:                                                                                               | Unique identifier of the tenant in the system (usually a store identifier)                                       |

### Response

**[?Operations\PostSchedulesAdjustmentsResponse](../../Models/Operations/PostSchedulesAdjustmentsResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## delete

Permanently deletes a pending schedule adjustment, reverting the affected upcoming order to its original configuration.

### Example Usage

<!-- UsageSnippet language="php" operationID="delete_/schedules/adjustments/{adjustmentId}" method="delete" path="/schedules/adjustments/{adjustmentId}" -->
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



$response = $sdk->schedules->delete(
    adjustmentId: 'b26d15ed-5f39-4b3b-ae89-fcfbe0c20a66'
);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `adjustmentId`                                                             | *string*                                                                   | :heavy_check_mark:                                                         | The adjustment identifier                                                  |
| `tenant`                                                                   | *?string*                                                                  | :heavy_minus_sign:                                                         | Unique identifier of the tenant in the system (usually a store identifier) |

### Response

**[?Operations\DeleteSchedulesAdjustmentsAdjustmentIdResponse](../../Models/Operations/DeleteSchedulesAdjustmentsAdjustmentIdResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |