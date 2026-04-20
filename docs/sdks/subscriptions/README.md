# Subscriptions

## Overview

### Available Operations

* [list](#list) - Lists subscriptions
* [update](#update) - Updates a subscription
* [pause](#pause) - Pauses an active subscription
* [resume](#resume) - Resumes a paused subscription
* [cancel](#cancel) - Cancels an active/paused subscription
* [reactivate](#reactivate) - Reactivates a cancelled subscription

## list

Lists subscriptions

### Example Usage

<!-- UsageSnippet language="php" operationID="get_/subscriptions" method="get" path="/subscriptions" -->
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

$request = new Operations\GetSubscriptionsRequest();

$responses = $sdk->subscriptions->list(
    request: $request
);


foreach ($responses as $response) {
    if ($response->statusCode === 200) {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                                | Type                                                                                     | Required                                                                                 | Description                                                                              |
| ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `$request`                                                                               | [Operations\GetSubscriptionsRequest](../../Models/Operations/GetSubscriptionsRequest.md) | :heavy_check_mark:                                                                       | The request object to use for the request.                                               |

### Response

**[?Operations\GetSubscriptionsResponse](../../Models/Operations/GetSubscriptionsResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## update

Updates a subscription

### Example Usage

<!-- UsageSnippet language="php" operationID="patch_/subscriptions/{subscriptionId}" method="patch" path="/subscriptions/{subscriptionId}" -->
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



$response = $sdk->subscriptions->update(
    subscriptionId: '8c7c7740-54e3-413d-9502-b3b025cda706',
    requestBody: $requestBody

);

if ($response->subscription !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                         | Type                                                                                                                              | Required                                                                                                                          | Description                                                                                                                       |
| --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `subscriptionId`                                                                                                                  | *string*                                                                                                                          | :heavy_check_mark:                                                                                                                | The subscription identifier                                                                                                       |
| `tenant`                                                                                                                          | *?string*                                                                                                                         | :heavy_minus_sign:                                                                                                                | Unique identifier of the tenant in the system (usually a store identifier)                                                        |
| `requestBody`                                                                                                                     | [?Operations\PatchSubscriptionsSubscriptionIdRequestBody](../../Models/Operations/PatchSubscriptionsSubscriptionIdRequestBody.md) | :heavy_minus_sign:                                                                                                                | N/A                                                                                                                               |

### Response

**[?Operations\PatchSubscriptionsSubscriptionIdResponse](../../Models/Operations/PatchSubscriptionsSubscriptionIdResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## pause

Pauses an active subscription

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/subscriptions/{subscriptionId}/pause" method="post" path="/subscriptions/{subscriptionId}/pause" -->
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



$response = $sdk->subscriptions->pause(
    subscriptionId: '5b923319-d7ad-4644-9be8-cee71a7bbd90'
);

if ($response->subscription !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `subscriptionId`                                                           | *string*                                                                   | :heavy_check_mark:                                                         | The subscription identifier                                                |
| `tenant`                                                                   | *?string*                                                                  | :heavy_minus_sign:                                                         | Unique identifier of the tenant in the system (usually a store identifier) |

### Response

**[?Operations\PostSubscriptionsSubscriptionIdPauseResponse](../../Models/Operations/PostSubscriptionsSubscriptionIdPauseResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## resume

Resumes a paused subscription

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/subscriptions/{subscriptionId}/resume" method="post" path="/subscriptions/{subscriptionId}/resume" -->
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



$response = $sdk->subscriptions->resume(
    subscriptionId: '80af0219-af04-4247-ae0a-79410d022410'
);

if ($response->subscription !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `subscriptionId`                                                           | *string*                                                                   | :heavy_check_mark:                                                         | The subscription identifier                                                |
| `tenant`                                                                   | *?string*                                                                  | :heavy_minus_sign:                                                         | Unique identifier of the tenant in the system (usually a store identifier) |

### Response

**[?Operations\PostSubscriptionsSubscriptionIdResumeResponse](../../Models/Operations/PostSubscriptionsSubscriptionIdResumeResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## cancel

Cancels an active/paused subscription

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/subscriptions/{subscriptionId}/cancel" method="post" path="/subscriptions/{subscriptionId}/cancel" -->
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

$requestBody = new Operations\PostSubscriptionsSubscriptionIdCancelRequestBody(
    notifyCustomer: true,
);

$response = $sdk->subscriptions->cancel(
    subscriptionId: '8e409b1b-2fdb-4b78-a87a-fc62fd6bb881',
    requestBody: $requestBody

);

if ($response->subscription !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                                  | Type                                                                                                                                       | Required                                                                                                                                   | Description                                                                                                                                |
| ------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `subscriptionId`                                                                                                                           | *string*                                                                                                                                   | :heavy_check_mark:                                                                                                                         | The subscription identifier                                                                                                                |
| `requestBody`                                                                                                                              | [Operations\PostSubscriptionsSubscriptionIdCancelRequestBody](../../Models/Operations/PostSubscriptionsSubscriptionIdCancelRequestBody.md) | :heavy_check_mark:                                                                                                                         | N/A                                                                                                                                        |
| `tenant`                                                                                                                                   | *?string*                                                                                                                                  | :heavy_minus_sign:                                                                                                                         | Unique identifier of the tenant in the system (usually a store identifier)                                                                 |

### Response

**[?Operations\PostSubscriptionsSubscriptionIdCancelResponse](../../Models/Operations/PostSubscriptionsSubscriptionIdCancelResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## reactivate

Reactivates a cancelled subscription

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/subscriptions/{subscriptionId}/reactivate" method="post" path="/subscriptions/{subscriptionId}/reactivate" -->
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



$response = $sdk->subscriptions->reactivate(
    subscriptionId: 'f71f1920-f98e-47cf-ad83-b55b4737972c'
);

if ($response->subscription !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `subscriptionId`                                                           | *string*                                                                   | :heavy_check_mark:                                                         | The subscription identifier                                                |
| `tenant`                                                                   | *?string*                                                                  | :heavy_minus_sign:                                                         | Unique identifier of the tenant in the system (usually a store identifier) |

### Response

**[?Operations\PostSubscriptionsSubscriptionIdReactivateResponse](../../Models/Operations/PostSubscriptionsSubscriptionIdReactivateResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |