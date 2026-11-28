# Customers

## Overview

Customers who own subscriptions. Create and update customer records.

### Available Operations

* [list](#list) - List customers
* [create](#create) - Create a customer
* [update](#update) - Update a customer
* [delete](#delete) - Delete a customer
* [createPaymentMethod](#createpaymentmethod) - Creates a customer payment method

## list

Returns a paginated list of customers with active or past subscriptions. Supports search by id, display name, email, or phone. Results are cursor-paginated.

### Example Usage

<!-- UsageSnippet language="php" operationID="get_/customers" method="get" path="/customers" -->
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

### Parameters

| Parameter                                                                        | Type                                                                             | Required                                                                         | Description                                                                      |
| -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `$request`                                                                       | [Operations\GetCustomersRequest](../../Models/Operations/GetCustomersRequest.md) | :heavy_check_mark:                                                               | The request object to use for the request.                                       |

### Response

**[?Operations\GetCustomersResponse](../../Models/Operations/GetCustomersResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## create

Creates a new customer in the e-commerce platform. Provide contact details (first name, last name, email, phone, tags, note). Returns the created customer once registered.

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/customers" method="post" path="/customers" -->
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



$response = $sdk->customers->create(
    requestBody: $requestBody
);

if ($response->customer !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                   | Type                                                                                        | Required                                                                                    | Description                                                                                 |
| ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| `tenant`                                                                                    | *?string*                                                                                   | :heavy_minus_sign:                                                                          | Unique identifier of the tenant in the system (usually a store identifier)                  |
| `requestBody`                                                                               | [?Operations\PostCustomersRequestBody](../../Models/Operations/PostCustomersRequestBody.md) | :heavy_minus_sign:                                                                          | N/A                                                                                         |

### Response

**[?Operations\PostCustomersResponse](../../Models/Operations/PostCustomersResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## update

Updates an existing customer's profile in the e-commerce platform. Supports partial updates — only provided fields are changed.

### Example Usage

<!-- UsageSnippet language="php" operationID="patch_/customers/{customerId}" method="patch" path="/customers/{customerId}" -->
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



$response = $sdk->customers->update(
    customerId: '<id>',
    requestBody: $requestBody

);

if ($response->customer !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                         | Type                                                                                                              | Required                                                                                                          | Description                                                                                                       |
| ----------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| `customerId`                                                                                                      | *string*                                                                                                          | :heavy_check_mark:                                                                                                | The customer identifier                                                                                           |
| `tenant`                                                                                                          | *?string*                                                                                                         | :heavy_minus_sign:                                                                                                | Unique identifier of the tenant in the system (usually a store identifier)                                        |
| `requestBody`                                                                                                     | [?Operations\PatchCustomersCustomerIdRequestBody](../../Models/Operations/PatchCustomersCustomerIdRequestBody.md) | :heavy_minus_sign:                                                                                                | N/A                                                                                                               |

### Response

**[?Operations\PatchCustomersCustomerIdResponse](../../Models/Operations/PatchCustomersCustomerIdResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## delete

Permanently deletes a customer from the e-commerce platform. This operation is irreversible.

### Example Usage

<!-- UsageSnippet language="php" operationID="delete_/customers/{customerId}" method="delete" path="/customers/{customerId}" -->
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



$response = $sdk->customers->delete(
    customerId: '<id>'
);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `customerId`                                                               | *string*                                                                   | :heavy_check_mark:                                                         | The customer identifier                                                    |
| `tenant`                                                                   | *?string*                                                                  | :heavy_minus_sign:                                                         | Unique identifier of the tenant in the system (usually a store identifier) |

### Response

**[?Operations\DeleteCustomersCustomerIdResponse](../../Models/Operations/DeleteCustomersCustomerIdResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## createPaymentMethod

Creates a customer payment method

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/customers/{customerId}/payment-methods" method="post" path="/customers/{customerId}/payment-methods" -->
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



$response = $sdk->customers->createPaymentMethod(
    customerId: '<id>'
);

if ($response->customerPaymentMethod !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                                                             | Type                                                                                                                                                                  | Required                                                                                                                                                              | Description                                                                                                                                                           |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `customerId`                                                                                                                                                          | *string*                                                                                                                                                              | :heavy_check_mark:                                                                                                                                                    | The customer identifier                                                                                                                                               |
| `tenant`                                                                                                                                                              | *?string*                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                    | Unique identifier of the tenant in the system (usually a store identifier)                                                                                            |
| `requestBody`                                                                                                                                                         | [Operations\Bogus\|Operations\PostCustomersCustomerIdPaymentMethodsRequestBody\|null](../../Models/Operations/PostCustomersCustomerIdPaymentMethodsRequestBodyUnion.md) | :heavy_minus_sign:                                                                                                                                                    | N/A                                                                                                                                                                   |

### Response

**[?Operations\PostCustomersCustomerIdPaymentMethodsResponse](../../Models/Operations/PostCustomersCustomerIdPaymentMethodsResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |