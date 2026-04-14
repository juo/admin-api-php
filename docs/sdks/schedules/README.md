# Schedules
(*schedules*)

## Overview

### Available Operations

* [list](#list) - List schedule orders for a customer
* [listAdjustments](#listadjustments) - List schedule adjustments for a customer
* [postSchedulesAdjustments](#postschedulesadjustments) - Creates a schedule adjustment
* [delete](#delete) - Deletes a schedule adjustment

## list

List schedule orders for a customer

### Example Usage

<!-- UsageSnippet language="php" operationID="get_/schedules/" method="get" path="/schedules/" -->
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



$response = $sdk->schedules->list(
    customerId: '<id>',
    count: 168523

);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                                                                                                                                                               | Type                                                                                                                                                                                                                                                                    | Required                                                                                                                                                                                                                                                                | Description                                                                                                                                                                                                                                                             |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `customerId`                                                                                                                                                                                                                                                            | *string*                                                                                                                                                                                                                                                                | :heavy_check_mark:                                                                                                                                                                                                                                                      | The customer identifier                                                                                                                                                                                                                                                 |
| `count`                                                                                                                                                                                                                                                                 | *int*                                                                                                                                                                                                                                                                   | :heavy_check_mark:                                                                                                                                                                                                                                                      | N/A                                                                                                                                                                                                                                                                     |
| `query`                                                                                                                                                                                                                                                                 | *?string*                                                                                                                                                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                                                                                                      | The search query string. See [search query language](/docs/api-reference/admin/introduction#search-query-language) for information how to build the search query. Supported fields are listed [here](/docs/api-reference/admin/schedules/resource#search-query-fields). |
| `tenant`                                                                                                                                                                                                                                                                | *?string*                                                                                                                                                                                                                                                               | :heavy_minus_sign:                                                                                                                                                                                                                                                      | Unique identifier of the tenant in the system (usually a store identifier)                                                                                                                                                                                              |

### Response

**[?Operations\GetSchedulesResponse](../../Models/Operations/GetSchedulesResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## listAdjustments

List schedule adjustments for a customer

### Example Usage

<!-- UsageSnippet language="php" operationID="get_/schedules/adjustments" method="get" path="/schedules/adjustments" -->
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

## postSchedulesAdjustments

Creates a schedule adjustment

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/schedules/adjustments" method="post" path="/schedules/adjustments" -->
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
        input: new Operations\ActionInput5(
            lines: [
                new Operations\Line(
                    lineId: '<id>',
                ),
            ],
        ),
    ),
);

$response = $sdk->schedules->postSchedulesAdjustments(
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

Deletes a schedule adjustment

### Example Usage

<!-- UsageSnippet language="php" operationID="delete_/schedules/adjustments/{adjustmentId}" method="delete" path="/schedules/adjustments/{adjustmentId}" -->
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