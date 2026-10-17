# Products

## Overview

Products and variants linked to subscription plans. Manage catalog and plan assignments.

### Available Operations

* [list](#list) - List products
* [create](#create) - Create a product
* [update](#update) - Update a product
* [delete](#delete) - Delete a product
* [assignProductToPlan](#assignproducttoplan) - Assign a product to a subscription plan
* [removeProductFromPlan](#removeproductfromplan) - Remove a product from a subscription plan
* [addVariant](#addvariant) - Add a variant to a product
* [removeVariant](#removevariant) - Remove a variant from a product
* [assignVariantToPlan](#assignvarianttoplan) - Assign a variant to a subscription plan
* [removeVariantFromPlan](#removevariantfromplan) - Remove a variant from a subscription plan

## list

Returns a paginated list of products available for subscription. Supports search by id, title, status, or variant SKU/title. Use `planGroup` to filter by subscription plan group. Results are cursor-paginated.

### Example Usage

<!-- UsageSnippet language="php" operationID="get_/products" method="get" path="/products" -->
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

$request = new Operations\GetProductsRequest();

$responses = $sdk->products->list(
    request: $request
);


foreach ($responses as $response) {
    if ($response->statusCode === 200) {
        // handle response
    }
}
```

### Parameters

| Parameter                                                                      | Type                                                                           | Required                                                                       | Description                                                                    |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ |
| `$request`                                                                     | [Operations\GetProductsRequest](../../Models/Operations/GetProductsRequest.md) | :heavy_check_mark:                                                             | The request object to use for the request.                                     |

### Response

**[?Operations\GetProductsResponse](../../Models/Operations/GetProductsResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## create

Creates a new product in the e-commerce platform. Specify title, description, vendor, product type, tags, status (active/draft), taxonomy category ID, collection IDs, and an optional image URL. Returns the created product.

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/products" method="post" path="/products" -->
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

$requestBody = new Operations\PostProductsRequestBody(
    title: '<value>',
);

$response = $sdk->products->create(
    requestBody: $requestBody
);

if ($response->product !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                | Type                                                                                     | Required                                                                                 | Description                                                                              |
| ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `requestBody`                                                                            | [Operations\PostProductsRequestBody](../../Models/Operations/PostProductsRequestBody.md) | :heavy_check_mark:                                                                       | N/A                                                                                      |
| `tenant`                                                                                 | *?string*                                                                                | :heavy_minus_sign:                                                                       | Unique identifier of the tenant in the system (usually a store identifier)               |

### Response

**[?Operations\PostProductsResponse](../../Models/Operations/PostProductsResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## update

Updates a product in the e-commerce platform. Supports partial updates — only provided fields are changed. Status can be set to active, draft, or archived.

### Example Usage

<!-- UsageSnippet language="php" operationID="patch_/products/{productId}" method="patch" path="/products/{productId}" -->
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



$response = $sdk->products->update(
    productId: '<id>',
    requestBody: $requestBody

);

if ($response->product !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                     | Type                                                                                                          | Required                                                                                                      | Description                                                                                                   |
| ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| `productId`                                                                                                   | *string*                                                                                                      | :heavy_check_mark:                                                                                            | The product identifier                                                                                        |
| `tenant`                                                                                                      | *?string*                                                                                                     | :heavy_minus_sign:                                                                                            | Unique identifier of the tenant in the system (usually a store identifier)                                    |
| `requestBody`                                                                                                 | [?Operations\PatchProductsProductIdRequestBody](../../Models/Operations/PatchProductsProductIdRequestBody.md) | :heavy_minus_sign:                                                                                            | N/A                                                                                                           |

### Response

**[?Operations\PatchProductsProductIdResponse](../../Models/Operations/PatchProductsProductIdResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## delete

Permanently deletes a product from the e-commerce platform.

### Example Usage

<!-- UsageSnippet language="php" operationID="delete_/products/{productId}" method="delete" path="/products/{productId}" -->
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



$response = $sdk->products->delete(
    productId: '<id>'
);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `productId`                                                                | *string*                                                                   | :heavy_check_mark:                                                         | The product identifier                                                     |
| `tenant`                                                                   | *?string*                                                                  | :heavy_minus_sign:                                                         | Unique identifier of the tenant in the system (usually a store identifier) |

### Response

**[?Operations\DeleteProductsProductIdResponse](../../Models/Operations/DeleteProductsProductIdResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## assignProductToPlan

Associates a product with a subscription plan group, making all its variants available for subscription purchase under that plan.

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/products/{productId}/plans" method="post" path="/products/{productId}/plans" -->
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

$requestBody = new Operations\PostProductsProductIdPlansRequestBody(
    planId: '<id>',
);

$response = $sdk->products->assignProductToPlan(
    productId: '<id>',
    requestBody: $requestBody

);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                            | Type                                                                                                                 | Required                                                                                                             | Description                                                                                                          |
| -------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| `productId`                                                                                                          | *string*                                                                                                             | :heavy_check_mark:                                                                                                   | The product identifier                                                                                               |
| `requestBody`                                                                                                        | [Operations\PostProductsProductIdPlansRequestBody](../../Models/Operations/PostProductsProductIdPlansRequestBody.md) | :heavy_check_mark:                                                                                                   | N/A                                                                                                                  |
| `tenant`                                                                                                             | *?string*                                                                                                            | :heavy_minus_sign:                                                                                                   | Unique identifier of the tenant in the system (usually a store identifier)                                           |

### Response

**[?Operations\PostProductsProductIdPlansResponse](../../Models/Operations/PostProductsProductIdPlansResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## removeProductFromPlan

Disassociates a product from a subscription plan group, removing all its variants from eligibility under that plan.

### Example Usage

<!-- UsageSnippet language="php" operationID="delete_/products/{productId}/plans" method="delete" path="/products/{productId}/plans" -->
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

$requestBody = new Operations\DeleteProductsProductIdPlansRequestBody(
    planId: '<id>',
);

$response = $sdk->products->removeProductFromPlan(
    productId: '<id>',
    requestBody: $requestBody

);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                | Type                                                                                                                     | Required                                                                                                                 | Description                                                                                                              |
| ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------ |
| `productId`                                                                                                              | *string*                                                                                                                 | :heavy_check_mark:                                                                                                       | The product identifier                                                                                                   |
| `requestBody`                                                                                                            | [Operations\DeleteProductsProductIdPlansRequestBody](../../Models/Operations/DeleteProductsProductIdPlansRequestBody.md) | :heavy_check_mark:                                                                                                       | N/A                                                                                                                      |
| `tenant`                                                                                                                 | *?string*                                                                                                                | :heavy_minus_sign:                                                                                                       | Unique identifier of the tenant in the system (usually a store identifier)                                               |

### Response

**[?Operations\DeleteProductsProductIdPlansResponse](../../Models/Operations/DeleteProductsProductIdPlansResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## addVariant

Creates and adds a new variant (e.g., size or color) to an existing product in the e-commerce platform.

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/products/{productId}/variants" method="post" path="/products/{productId}/variants" -->
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

$requestBody = new Operations\PostProductsProductIdVariantsRequestBody(
    price: 7461.18,
);

$response = $sdk->products->addVariant(
    productId: '<id>',
    requestBody: $requestBody

);

if ($response->productVariant !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                  | Type                                                                                                                       | Required                                                                                                                   | Description                                                                                                                |
| -------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| `productId`                                                                                                                | *string*                                                                                                                   | :heavy_check_mark:                                                                                                         | The product identifier                                                                                                     |
| `requestBody`                                                                                                              | [Operations\PostProductsProductIdVariantsRequestBody](../../Models/Operations/PostProductsProductIdVariantsRequestBody.md) | :heavy_check_mark:                                                                                                         | N/A                                                                                                                        |
| `tenant`                                                                                                                   | *?string*                                                                                                                  | :heavy_minus_sign:                                                                                                         | Unique identifier of the tenant in the system (usually a store identifier)                                                 |

### Response

**[?Operations\PostProductsProductIdVariantsResponse](../../Models/Operations/PostProductsProductIdVariantsResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## removeVariant

Permanently removes a specific variant from a product in the e-commerce platform.

### Example Usage

<!-- UsageSnippet language="php" operationID="delete_/products/{productId}/variants/{variantId}" method="delete" path="/products/{productId}/variants/{variantId}" -->
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



$response = $sdk->products->removeVariant(
    productId: '<id>',
    variantId: '<id>'

);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `productId`                                                                | *string*                                                                   | :heavy_check_mark:                                                         | The product identifier                                                     |
| `variantId`                                                                | *string*                                                                   | :heavy_check_mark:                                                         | The variant identifier                                                     |
| `tenant`                                                                   | *?string*                                                                  | :heavy_minus_sign:                                                         | Unique identifier of the tenant in the system (usually a store identifier) |

### Response

**[?Operations\DeleteProductsProductIdVariantsVariantIdResponse](../../Models/Operations/DeleteProductsProductIdVariantsVariantIdResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## assignVariantToPlan

Associates a specific product variant with a subscription plan group, making only that variant available for subscription purchase under that plan.

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/products/{productId}/variants/{variantId}/plans" method="post" path="/products/{productId}/variants/{variantId}/plans" -->
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

$requestBody = new Operations\PostProductsProductIdVariantsVariantIdPlansRequestBody(
    planId: '<id>',
);

$response = $sdk->products->assignVariantToPlan(
    productId: '<id>',
    variantId: '<id>',
    requestBody: $requestBody

);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                                              | Type                                                                                                                                                   | Required                                                                                                                                               | Description                                                                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `productId`                                                                                                                                            | *string*                                                                                                                                               | :heavy_check_mark:                                                                                                                                     | The product identifier                                                                                                                                 |
| `variantId`                                                                                                                                            | *string*                                                                                                                                               | :heavy_check_mark:                                                                                                                                     | The variant identifier                                                                                                                                 |
| `requestBody`                                                                                                                                          | [Operations\PostProductsProductIdVariantsVariantIdPlansRequestBody](../../Models/Operations/PostProductsProductIdVariantsVariantIdPlansRequestBody.md) | :heavy_check_mark:                                                                                                                                     | N/A                                                                                                                                                    |
| `tenant`                                                                                                                                               | *?string*                                                                                                                                              | :heavy_minus_sign:                                                                                                                                     | Unique identifier of the tenant in the system (usually a store identifier)                                                                             |

### Response

**[?Operations\PostProductsProductIdVariantsVariantIdPlansResponse](../../Models/Operations/PostProductsProductIdVariantsVariantIdPlansResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## removeVariantFromPlan

Disassociates a specific product variant from a subscription plan group, removing it from eligibility under that plan.

### Example Usage

<!-- UsageSnippet language="php" operationID="delete_/products/{productId}/variants/{variantId}/plans" method="delete" path="/products/{productId}/variants/{variantId}/plans" -->
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

$requestBody = new Operations\DeleteProductsProductIdVariantsVariantIdPlansRequestBody(
    planId: '<id>',
);

$response = $sdk->products->removeVariantFromPlan(
    productId: '<id>',
    variantId: '<id>',
    requestBody: $requestBody

);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                                                  | Type                                                                                                                                                       | Required                                                                                                                                                   | Description                                                                                                                                                |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `productId`                                                                                                                                                | *string*                                                                                                                                                   | :heavy_check_mark:                                                                                                                                         | The product identifier                                                                                                                                     |
| `variantId`                                                                                                                                                | *string*                                                                                                                                                   | :heavy_check_mark:                                                                                                                                         | The variant identifier                                                                                                                                     |
| `requestBody`                                                                                                                                              | [Operations\DeleteProductsProductIdVariantsVariantIdPlansRequestBody](../../Models/Operations/DeleteProductsProductIdVariantsVariantIdPlansRequestBody.md) | :heavy_check_mark:                                                                                                                                         | N/A                                                                                                                                                        |
| `tenant`                                                                                                                                                   | *?string*                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                         | Unique identifier of the tenant in the system (usually a store identifier)                                                                                 |

### Response

**[?Operations\DeleteProductsProductIdVariantsVariantIdPlansResponse](../../Models/Operations/DeleteProductsProductIdVariantsVariantIdPlansResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |