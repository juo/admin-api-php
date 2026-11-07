# juo/admin-api

Developer-friendly & type-safe Php SDK specifically catered to leverage *juo/admin-api* API.

<!-- Start Summary [summary] -->
## Summary

Juo Admin API: Programmatic access to subscription management for merchants.

## Core Resources

- **Subscriptions** — the central entity. Belongs to a Customer, contains Items (product variants) and Discounts. Lifecycle: `active` → `paused` or `cancelled`; `paused` → `active` or `cancelled`; `cancelled` → `active` (via reactivate).
- **Items** — subscription items (product variants) (quantity, price, billing/delivery policies).
- **Discounts** — applied to subscriptions by discount code or manually (percentage or fixed amount, targeting subscription items or shipping).
- **Customers** — customers who own subscriptions and payment methods.
- **Products / Variants** — catalog products and variants that can be assigned to subscription plans.
- **Schedules** — a read-only projection of upcoming billing orders, derived from subscription state, active schedule adjustments, and triggered workflows. **Schedule adjustments never modify the subscription** — they apply changes to upcoming orders matching the specified criteria (by cycle, date, or both), which may cover one or more orders. For permanent changes (billing frequency, items, payment method, delivery address), update the subscription directly.
- **Workflows** — interactive customer-facing flows (retention, dunning, onboarding). Contain Steps connected by Transitions and produce Runs on each execution. Supports A/B experiment steps.

## Authentication

Every request requires:
- `X-Juo-Admin-Api-Key` header — the merchant's Admin API key.
- `X-Tenant-ID` header — the store identifier (myshopify domain, e.g. `my-store.myshopify.com`).
<!-- End Summary [summary] -->

<!-- Start Table of Contents [toc] -->
## Table of Contents
<!-- $toc-max-depth=2 -->
* [juo/admin-api](#juoadmin-api)
  * [Core Resources](#core-resources)
  * [Authentication](#authentication)
  * [SDK Installation](#sdk-installation)
  * [SDK Example Usage](#sdk-example-usage)
  * [Authentication](#authentication-1)
  * [Available Resources and Operations](#available-resources-and-operations)
  * [Pagination](#pagination)
  * [Error Handling](#error-handling)
  * [Server Selection](#server-selection)
* [Development](#development)
  * [Maturity](#maturity)
  * [Contributions](#contributions)

<!-- End Table of Contents [toc] -->

<!-- Start SDK Installation [installation] -->
## SDK Installation

The SDK relies on [Composer](https://getcomposer.org/) to manage its dependencies.

To install the SDK and add it as a dependency to an existing `composer.json` file:
```bash
composer require "juo/admin-api"
```
<!-- End SDK Installation [installation] -->

<!-- Start SDK Example Usage [usage] -->
## SDK Example Usage

### Example

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

$requestBody = new Operations\PostAnalyticsQueryRequestBody(
    metric: Operations\MetricSubscriptionItemsCount::SubscriptionItemsCount,
    grain: Operations\GrainYear::Year,
    range: new Operations\Range(
        from: '<value>',
        to: '<value>',
    ),
);

$response = $sdk->analytics->query(
    requestBody: $requestBody
);

if ($response->object !== null) {
    // handle response
}
```
<!-- End SDK Example Usage [usage] -->

<!-- Start Authentication [security] -->
## Authentication

### Per-Client Security Schemes

This SDK supports the following security schemes globally:

| Name          | Type   | Scheme      |
| ------------- | ------ | ----------- |
| `adminApiKey` | apiKey | API key     |
| `bearerToken` | http   | HTTP Bearer |

You can set the security parameters through the `setSecurity` function on the `SDKBuilder` when initializing the SDK. The selected scheme will be used by default to authenticate with the API for all operations that support it. For example:
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Juo\AdminAPI;
use Juo\AdminAPI\Models\Components;
use Juo\AdminAPI\Models\Operations;

$sdk = AdminAPI\Juo::builder()
    ->setSecurity(
        new Components\Security(
            adminApiKey: '<YOUR_API_KEY_HERE>',
        )
    )
    ->setTenant('<value>')
    ->build();

$requestBody = new Operations\PostAnalyticsQueryRequestBody(
    metric: Operations\MetricSubscriptionItemsCount::SubscriptionItemsCount,
    grain: Operations\GrainYear::Year,
    range: new Operations\Range(
        from: '<value>',
        to: '<value>',
    ),
);

$response = $sdk->analytics->query(
    requestBody: $requestBody
);

if ($response->object !== null) {
    // handle response
}
```
<!-- End Authentication [security] -->

<!-- Start Available Resources and Operations [operations] -->
## Available Resources and Operations

<details open>
<summary>Available methods</summary>

### [Analytics](docs/sdks/analytics/README.md)

* [query](docs/sdks/analytics/README.md#query) - Query analytics metrics
* [listMetrics](docs/sdks/analytics/README.md#listmetrics) - Describe the analytics metric catalog

### [Customers](docs/sdks/customers/README.md)

* [list](docs/sdks/customers/README.md#list) - List customers
* [create](docs/sdks/customers/README.md#create) - Create a customer
* [update](docs/sdks/customers/README.md#update) - Update a customer
* [delete](docs/sdks/customers/README.md#delete) - Delete a customer
* [createPaymentMethod](docs/sdks/customers/README.md#createpaymentmethod) - Creates a customer payment method

### [Products](docs/sdks/products/README.md)

* [list](docs/sdks/products/README.md#list) - List products
* [create](docs/sdks/products/README.md#create) - Create a product
* [update](docs/sdks/products/README.md#update) - Update a product
* [delete](docs/sdks/products/README.md#delete) - Delete a product
* [assignProductToPlan](docs/sdks/products/README.md#assignproducttoplan) - Assign a product to a subscription plan
* [removeProductFromPlan](docs/sdks/products/README.md#removeproductfromplan) - Remove a product from a subscription plan
* [addVariant](docs/sdks/products/README.md#addvariant) - Add a variant to a product
* [removeVariant](docs/sdks/products/README.md#removevariant) - Remove a variant from a product
* [assignVariantToPlan](docs/sdks/products/README.md#assignvarianttoplan) - Assign a variant to a subscription plan
* [removeVariantFromPlan](docs/sdks/products/README.md#removevariantfromplan) - Remove a variant from a subscription plan

### [Schedules](docs/sdks/schedules/README.md)

* [list](docs/sdks/schedules/README.md#list) - List schedule orders
* [listAdjustments](docs/sdks/schedules/README.md#listadjustments) - List schedule adjustments
* [create](docs/sdks/schedules/README.md#create) - Create a schedule adjustment
* [delete](docs/sdks/schedules/README.md#delete) - Delete a schedule adjustment

### [Subscriptions](docs/sdks/subscriptions/README.md)

* [list](docs/sdks/subscriptions/README.md#list) - List subscriptions
* [create](docs/sdks/subscriptions/README.md#create) - Create a subscription
* [update](docs/sdks/subscriptions/README.md#update) - Update a subscription
* [pause](docs/sdks/subscriptions/README.md#pause) - Pause an active subscription
* [resume](docs/sdks/subscriptions/README.md#resume) - Resume a paused subscription
* [cancel](docs/sdks/subscriptions/README.md#cancel) - Cancel a subscription
* [reactivate](docs/sdks/subscriptions/README.md#reactivate) - Reactivate a canceled subscription

#### [Subscriptions.CustomAttributes](docs/sdks/customattributes/README.md)

* [create](docs/sdks/customattributes/README.md#create) - Add custom attributes to a subscription

#### [Subscriptions.Discounts](docs/sdks/discounts/README.md)

* [create](docs/sdks/discounts/README.md#create) - Add a discount to a subscription
* [update](docs/sdks/discounts/README.md#update) - Update a subscription discount
* [delete](docs/sdks/discounts/README.md#delete) - Remove a subscription discount

#### [Subscriptions.Items](docs/sdks/items/README.md)

* [create](docs/sdks/items/README.md#create) - Add an item to a subscription
* [update](docs/sdks/items/README.md#update) - Update a subscription item
* [delete](docs/sdks/items/README.md#delete) - Remove a subscription item

### [Workflows](docs/sdks/workflows/README.md)

* [list](docs/sdks/workflows/README.md#list) - List workflows
* [create](docs/sdks/workflows/README.md#create) - Create a workflow
* [get](docs/sdks/workflows/README.md#get) - Get a workflow
* [update](docs/sdks/workflows/README.md#update) - Update a workflow
* [delete](docs/sdks/workflows/README.md#delete) - Delete a workflow
* [archive](docs/sdks/workflows/README.md#archive) - Archive a workflow
* [duplicate](docs/sdks/workflows/README.md#duplicate) - Duplicate a workflow
* [publish](docs/sdks/workflows/README.md#publish) - Publish a workflow
* [listRuns](docs/sdks/workflows/README.md#listruns) - List workflow runs
* [unpublish](docs/sdks/workflows/README.md#unpublish) - Unpublish a workflow
* [getRun](docs/sdks/workflows/README.md#getrun) - Get a workflow run
* [exportRuns](docs/sdks/workflows/README.md#exportruns) - Export workflow runs as CSV
* [getWorkflowsIdRunsExport](docs/sdks/workflows/README.md#getworkflowsidrunsexport) - Download workflow runs CSV
* [getRunStats](docs/sdks/workflows/README.md#getrunstats) - Get workflow run statistics
* [concludeExperiment](docs/sdks/workflows/README.md#concludeexperiment) - Conclude a workflow experiment

</details>
<!-- End Available Resources and Operations [operations] -->

<!-- Start Pagination [pagination] -->
## Pagination

Some of the endpoints in this SDK support pagination. To use pagination, you make your SDK calls as usual, but the
returned object will be a `Generator` instead of an individual response.

Working with generators is as simple as iterating over the responses in a `foreach` loop, and you can see an example below:
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

$request = new Operations\GetCustomersRequest();

$responses = $sdk->customers->list(
    request: $request
);


foreach ($responses as $response) {
    if ($response->statusCode === 200) {
        // handle response
    }
}
```
<!-- End Pagination [pagination] -->

<!-- Start Error Handling [errors] -->
## Error Handling

Handling errors in this SDK should largely match your expectations. All operations return a response object or throw an exception.

By default an API error will raise a `Errors\APIException` exception, which has the following properties:

| Property       | Type                                    | Description           |
|----------------|-----------------------------------------|-----------------------|
| `$message`     | *string*                                | The error message     |
| `$statusCode`  | *int*                                   | The HTTP status code  |
| `$rawResponse` | *?\Psr\Http\Message\ResponseInterface*  | The raw HTTP response |
| `$body`        | *string*                                | The response content  |

When custom error responses are specified for an operation, the SDK may also throw their associated exception. You can refer to respective *Errors* tables in SDK docs for more details on possible exception types for each operation. For example, the `query` method throws the following exceptions:

| Error Type          | Status Code | Content Type |
| ------------------- | ----------- | ------------ |
| Errors\APIException | 4XX, 5XX    | \*/\*        |

### Example

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

try {
    $requestBody = new Operations\PostAnalyticsQueryRequestBody(
        metric: Operations\MetricSubscriptionItemsCount::SubscriptionItemsCount,
        grain: Operations\GrainYear::Year,
        range: new Operations\Range(
            from: '<value>',
            to: '<value>',
        ),
    );

    $response = $sdk->analytics->query(
        requestBody: $requestBody
    );

    if ($response->object !== null) {
        // handle response
    }
} catch (Errors\APIException $e) {
    // handle default exception
    throw $e;
}
```
<!-- End Error Handling [errors] -->

<!-- Start Server Selection [server] -->
## Server Selection

### Override Server URL Per-Client

The default server can be overridden globally using the `setServerUrl(string $serverUrl)` builder method when initializing the SDK client instance. For example:
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Juo\AdminAPI;
use Juo\AdminAPI\Models\Components;
use Juo\AdminAPI\Models\Operations;

$sdk = AdminAPI\Juo::builder()
    ->setServerURL('https://api.juo.io/admin/v1')
    ->setTenant('<value>')
    ->setSecurity(
        new Components\Security(
            adminApiKey: '<YOUR_API_KEY_HERE>',
        )
    )
    ->build();

$requestBody = new Operations\PostAnalyticsQueryRequestBody(
    metric: Operations\MetricSubscriptionItemsCount::SubscriptionItemsCount,
    grain: Operations\GrainYear::Year,
    range: new Operations\Range(
        from: '<value>',
        to: '<value>',
    ),
);

$response = $sdk->analytics->query(
    requestBody: $requestBody
);

if ($response->object !== null) {
    // handle response
}
```
<!-- End Server Selection [server] -->

<!-- Placeholder for Future Speakeasy SDK Sections -->

# Development

## Maturity

This SDK is in beta, and there may be breaking changes between versions without a major version update. Therefore, we recommend pinning usage
to a specific package version. This way, you can install the same version each time without breaking changes unless you are intentionally
looking for the latest version.

## Contributions

While we value open-source contributions to this SDK, this library is generated programmatically. Any manual changes added to internal files will be overwritten on the next generation. 
We look forward to hearing your feedback. Feel free to open a PR or an issue with a proof of concept and we'll do our best to include it in a future release. 
