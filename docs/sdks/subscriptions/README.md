# Subscriptions

## Overview

Recurring billing agreements with customers. Manage lifecycle (pause, resume, cancel, reactivate), items, and discounts.

### Available Operations

* [list](#list) - List subscriptions
* [create](#create) - Create a subscription
* [update](#update) - Update a subscription
* [pause](#pause) - Pause an active subscription
* [resume](#resume) - Resume a paused subscription
* [cancel](#cancel) - Cancel a subscription
* [reactivate](#reactivate) - Reactivate a canceled subscription

## list

Returns a paginated list of all subscriptions for the tenant. Use the `query` parameter to search by id, serial, status, dates, or customer. Supports cursor-based pagination via `after`/`before`. Optionally expand the `customer` relationship to include customer details inline.

### Example Usage

<!-- UsageSnippet language="php" operationID="get_/subscriptions" method="get" path="/subscriptions" -->
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

## create

Creates a new subscription for an existing customer. Requires a billing policy, next billing date, delivery address, at least one subscription item, and a payment method (by id or by provider details). If the customer does not yet exist locally, they are looked up in the e-commerce platform and registered automatically.

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/subscriptions" method="post" path="/subscriptions" -->
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Juo\AdminAPI;
use Juo\AdminAPI\Models\Components;
use Juo\AdminAPI\Models\Operations;
use Juo\AdminAPI\Utils;

$sdk = AdminAPI\Juo::builder()
    ->setTenant('<value>')
    ->setSecurity(
        new Components\Security(
            adminApiKey: '<YOUR_API_KEY_HERE>',
        )
    )
    ->build();

$requestBody = new Operations\PostSubscriptionsRequestBody(
    customerId: '<id>',
    nextBillingDate: Utils\Utils::parseDateTime('2024-04-04T12:01:04.403Z'),
    billingPolicy: new Operations\PostSubscriptionsBillingPolicy(
        interval: Operations\PostSubscriptionsIntervalBillingPolicyYear::Year,
        intervalCount: 257469,
    ),
    paymentMethod: new Operations\PaymentMethod2(
        provider: Operations\PostSubscriptionsProviderMollie::Mollie,
        instrument: new Operations\PostSubscriptionsInstrumentBacs(
            type: Operations\PaymentMethodTypeBacs::Bacs,
            lastDigits: '<value>',
        ),
    ),
    status: Operations\PostSubscriptionsStatus::Active,
    currencyCode: Operations\CurrencyCode::Usd,
    deliveryAddress: new Operations\PostSubscriptionsDeliveryAddress(),
    items: [
        new Operations\PostSubscriptionsItem(
            variantId: '<id>',
            quantity: 1,
        ),
    ],
);

$response = $sdk->subscriptions->create(
    requestBody: $requestBody
);

if ($response->subscription !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                          | Type                                                                                               | Required                                                                                           | Description                                                                                        |
| -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| `requestBody`                                                                                      | [Operations\PostSubscriptionsRequestBody](../../Models/Operations/PostSubscriptionsRequestBody.md) | :heavy_check_mark:                                                                                 | N/A                                                                                                |
| `tenant`                                                                                           | *?string*                                                                                          | :heavy_minus_sign:                                                                                 | Unique identifier of the tenant in the system (usually a store identifier)                         |

### Response

**[?Operations\PostSubscriptionsResponse](../../Models/Operations/PostSubscriptionsResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## update

Updates mutable fields on an existing subscription using merge-patch semantics — only provided fields are changed. Supports changing the payment method, delivery address, delivery method, delivery price, and next billing date. These changes are permanent and affect all future billing cycles.

### Example Usage

<!-- UsageSnippet language="php" operationID="patch_/subscriptions/{subscriptionId}" method="patch" path="/subscriptions/{subscriptionId}" -->
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

Pauses an active subscription, suspending future billing cycles until explicitly resumed. The subscription must currently be in `active` status. After pausing, the subscription status changes to `paused`.

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/subscriptions/{subscriptionId}/pause" method="post" path="/subscriptions/{subscriptionId}/pause" -->
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

Resumes a paused subscription, restoring normal billing from the next scheduled billing date. The subscription must currently be in `paused` status.

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/subscriptions/{subscriptionId}/resume" method="post" path="/subscriptions/{subscriptionId}/resume" -->
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

Permanently cancels an active or paused subscription, stopping all future billing. Accepts an optional cancellation reason and a flag to notify the customer by email. Use `reactivate` to reverse a cancellation.

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/subscriptions/{subscriptionId}/cancel" method="post" path="/subscriptions/{subscriptionId}/cancel" -->
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

Reactivates a previously canceled subscription, returning it to `active` status and resuming billing from the next scheduled date. The subscription must currently be in `canceled` status.

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/subscriptions/{subscriptionId}/reactivate" method="post" path="/subscriptions/{subscriptionId}/reactivate" -->
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