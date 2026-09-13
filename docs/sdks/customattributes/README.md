# Subscriptions.CustomAttributes

## Overview

### Available Operations

* [create](#create) - Add custom attributes to a subscription

## create

Appends one or more custom attributes to a subscription. This is additive: existing attributes are never modified or removed. A key that already exists returns 409 — edit existing attributes elsewhere. Reserved and internal (`_`-prefixed) keys cannot be written (400).

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/subscriptions/{subscriptionId}/custom-attributes" method="post" path="/subscriptions/{subscriptionId}/custom-attributes" -->
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

$requestBody = new Operations\PostSubscriptionsSubscriptionIdCustomAttributesRequestBody(
    customAttributes: [
        new Operations\PostSubscriptionsSubscriptionIdCustomAttributesCustomAttribute(
            key: '<key>',
            value: '<value>',
        ),
    ],
);

$response = $sdk->subscriptions->customAttributes->create(
    subscriptionId: '2add5273-52dd-42b3-a6ef-48a6d8fc7bac',
    requestBody: $requestBody

);

if ($response->subscription !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                                                      | Type                                                                                                                                                           | Required                                                                                                                                                       | Description                                                                                                                                                    |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `subscriptionId`                                                                                                                                               | *string*                                                                                                                                                       | :heavy_check_mark:                                                                                                                                             | The subscription identifier                                                                                                                                    |
| `requestBody`                                                                                                                                                  | [Operations\PostSubscriptionsSubscriptionIdCustomAttributesRequestBody](../../Models/Operations/PostSubscriptionsSubscriptionIdCustomAttributesRequestBody.md) | :heavy_check_mark:                                                                                                                                             | N/A                                                                                                                                                            |
| `tenant`                                                                                                                                                       | *?string*                                                                                                                                                      | :heavy_minus_sign:                                                                                                                                             | Unique identifier of the tenant in the system (usually a store identifier)                                                                                     |

### Response

**[?Operations\PostSubscriptionsSubscriptionIdCustomAttributesResponse](../../Models/Operations/PostSubscriptionsSubscriptionIdCustomAttributesResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |