# juo/admin-api

Developer-friendly & type-safe Php SDK specifically catered to leverage *juo/admin-api* API.

<div align="left" style="margin-bottom: 0;">
    <a href="https://www.speakeasy.com/?utm_source=juo/admin-api&utm_campaign=php" class="badge-link">
        <span class="badge-container">
            <span class="badge-icon-section">
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 30 30" fill="none" style="vertical-align: middle;"><title>Speakeasy Logo</title><path fill="currentColor" d="m20.639 27.548-19.17-2.724L0 26.1l20.639 2.931 8.456-7.336-1.468-.208-6.988 6.062Z"></path><path fill="currentColor" d="m20.639 23.1 8.456-7.336-1.468-.207-6.988 6.06-6.84-.972-9.394-1.333-2.936-.417L0 20.169l2.937.416L0 23.132l20.639 2.931 8.456-7.334-1.468-.208-6.986 6.062-9.78-1.39 1.468-1.273 8.31 1.18Z"></path><path fill="currentColor" d="m20.639 18.65-19.17-2.724L0 17.201l20.639 2.931 8.456-7.334-1.468-.208-6.988 6.06Z"></path><path fill="currentColor" d="M27.627 6.658 24.69 9.205 20.64 12.72l-7.923-1.126L1.469 9.996 0 11.271l11.246 1.596-1.467 1.275-8.311-1.181L0 14.235l20.639 2.932 8.456-7.334-2.937-.418 2.937-2.549-1.468-.208Z"></path><path fill="currentColor" d="M29.095 3.902 8.456.971 0 8.305l20.639 2.934 8.456-7.337Z"></path></svg>
            </span>
            <span class="badge-text badge-text-section">BUILT BY SPEAKEASY</span>
        </span>
    </a>
    <a href="https://opensource.org/licenses/MIT" class="badge-link">
        <span class="badge-container blue">
            <span class="badge-text badge-text-section">LICENSE // MIT</span>
        </span>
    </a>
</div>


<br /><br />
> [!IMPORTANT]
> This SDK is not yet ready for production use. To complete setup please follow the steps outlined in your [workspace](https://app.speakeasy.com/org/juo/admin-api-8af). Delete this section before > publishing to a package manager.

<!-- Start Summary [summary] -->
## Summary


<!-- End Summary [summary] -->

<!-- Start Table of Contents [toc] -->
## Table of Contents
<!-- $toc-max-depth=2 -->
* [juo/admin-api](#juoadmin-api)
  * [SDK Installation](#sdk-installation)
  * [SDK Example Usage](#sdk-example-usage)
  * [Authentication](#authentication)
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

> [!TIP]
> To finish publishing your SDK you must [run your first generation action](https://www.speakeasy.com/docs/github-setup#step-by-step-guide).


The SDK relies on [Composer](https://getcomposer.org/) to manage its dependencies.

To install the SDK first add the below to your `composer.json` file:

```json
{
    "repositories": [
        {
            "type": "github",
            "url": "<UNSET>.git"
        }
    ],
    "require": {
        "juo/admin-api": "*"
    }
}
```

Then run the following command:

```bash
composer update
```
<!-- End SDK Installation [installation] -->

<!-- Start SDK Example Usage [usage] -->
## SDK Example Usage

### Example

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
<!-- End SDK Example Usage [usage] -->

<!-- Start Authentication [security] -->
## Authentication

### Per-Client Security Schemes

This SDK supports the following security scheme globally:

| Name          | Type   | Scheme  |
| ------------- | ------ | ------- |
| `adminApiKey` | apiKey | API key |

To authenticate with the API the `adminApiKey` parameter must be set when initializing the SDK. For example:
```php
declare(strict_types=1);

require 'vendor/autoload.php';

use Juo\AdminAPI;
use Juo\AdminAPI\Models\Operations;

$sdk = AdminAPI\Juo::builder()
    ->setSecurity(
        '<YOUR_API_KEY_HERE>'
    )
    ->setTenant('<value>')
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
<!-- End Authentication [security] -->

<!-- Start Available Resources and Operations [operations] -->
## Available Resources and Operations

<details open>
<summary>Available methods</summary>

### [customers](docs/sdks/customers/README.md)

* [list](docs/sdks/customers/README.md#list) - Lists customers

### [schedules](docs/sdks/schedules/README.md)

* [list](docs/sdks/schedules/README.md#list) - List schedule orders for a customer
* [listAdjustments](docs/sdks/schedules/README.md#listadjustments) - List schedule adjustments for a customer
* [postSchedulesAdjustments](docs/sdks/schedules/README.md#postschedulesadjustments) - Creates a schedule adjustment
* [delete](docs/sdks/schedules/README.md#delete) - Deletes a schedule adjustment

### [subscriptions](docs/sdks/subscriptions/README.md)

* [list](docs/sdks/subscriptions/README.md#list) - Lists subscriptions
* [update](docs/sdks/subscriptions/README.md#update) - Updates a subscription
* [pause](docs/sdks/subscriptions/README.md#pause) - Pauses an active subscription
* [resume](docs/sdks/subscriptions/README.md#resume) - Resumes a paused subscription
* [cancel](docs/sdks/subscriptions/README.md#cancel) - Cancels an active/paused subscription
* [reactivate](docs/sdks/subscriptions/README.md#reactivate) - Reactivates a cancelled subscription

#### [subscriptions->discounts](docs/sdks/discounts/README.md)

* [create](docs/sdks/discounts/README.md#create) - Creates a subscription discount
* [delete](docs/sdks/discounts/README.md#delete) - Deletes a subscription discount
* [update](docs/sdks/discounts/README.md#update) - Updates a subscription discount

#### [subscriptions->items](docs/sdks/items/README.md)

* [create](docs/sdks/items/README.md#create) - Creates a subscription item
* [delete](docs/sdks/items/README.md#delete) - Deletes a subscription item
* [update](docs/sdks/items/README.md#update) - Updates a subscription item

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
use Juo\AdminAPI\Models\Operations;

$sdk = AdminAPI\Juo::builder()
    ->setTenant('<value>')
    ->setSecurity(
        '<YOUR_API_KEY_HERE>'
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

When custom error responses are specified for an operation, the SDK may also throw their associated exception. You can refer to respective *Errors* tables in SDK docs for more details on possible exception types for each operation. For example, the `list` method throws the following exceptions:

| Error Type          | Status Code | Content Type |
| ------------------- | ----------- | ------------ |
| Errors\APIException | 4XX, 5XX    | \*/\*        |

### Example

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

try {
    $request = new Operations\GetCustomersRequest();

    $responses = $sdk->customers->list(
        request: $request
    );

    foreach ($responses as $response) {
        if ($response->statusCode === 200) {
            // handle response
        }
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
use Juo\AdminAPI\Models\Operations;

$sdk = AdminAPI\Juo::builder()
    ->setServerURL('https://api.juo.io/admin/v1')
    ->setTenant('<value>')
    ->setSecurity(
        '<YOUR_API_KEY_HERE>'
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

### SDK Created by [Speakeasy](https://www.speakeasy.com/?utm_source=juo/admin-api&utm_campaign=php)

<style>
  :root {
    --badge-gray-bg: #f3f4f6;
    --badge-gray-border: #d1d5db;
    --badge-gray-text: #374151;
    --badge-blue-bg: #eff6ff;
    --badge-blue-border: #3b82f6;
    --badge-blue-text: #3b82f6;
  }

  @media (prefers-color-scheme: dark) {
    :root {
      --badge-gray-bg: #374151;
      --badge-gray-border: #4b5563;
      --badge-gray-text: #f3f4f6;
      --badge-blue-bg: #1e3a8a;
      --badge-blue-border: #3b82f6;
      --badge-blue-text: #93c5fd;
    }
  }
  
  h1 {
    border-bottom: none !important;
    margin-bottom: 4px;
    margin-top: 0;
    letter-spacing: 0.5px;
    font-weight: 600;
  }
  
  .badge-text {
    letter-spacing: 1px;
    font-weight: 300;
  }
  
  .badge-container {
    display: inline-flex;
    align-items: center;
    background: var(--badge-gray-bg);
    border: 1px solid var(--badge-gray-border);
    border-radius: 6px;
    overflow: hidden;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;
    font-size: 11px;
    text-decoration: none;
    vertical-align: middle;
  }

  .badge-container.blue {
    background: var(--badge-blue-bg);
    border-color: var(--badge-blue-border);
  }

  .badge-icon-section {
    padding: 4px 8px;
    border-right: 1px solid var(--badge-gray-border);
    display: flex;
    align-items: center;
  }

  .badge-text-section {
    padding: 4px 10px;
    color: var(--badge-gray-text);
    font-weight: 400;
  }

  .badge-container.blue .badge-text-section {
    color: var(--badge-blue-text);
  }
  
  .badge-link {
    text-decoration: none;
    margin-left: 8px;
    display: inline-flex;
    vertical-align: middle;
  }

  .badge-link:hover {
    text-decoration: none;
  }
  
  .badge-link:first-child {
    margin-left: 0;
  }
  
  .badge-icon-section svg {
    color: var(--badge-gray-text);
  }

  .badge-container.blue .badge-icon-section svg {
    color: var(--badge-blue-text);
  }
</style> 