# Analytics

## Overview

Time-series metrics over subscriptions, customers and orders. Read the metric catalog first: it states what each metric means, the approximations it carries, and which filters and group-by dimensions the metric will honour — an unsupported filter is a 400, not an empty result.

### Available Operations

* [query](#query) - Query analytics metrics
* [listMetrics](#listmetrics) - Describe the analytics metric catalog

## query

Executes a time-series analytics query for the given metric. Results are grouped into time buckets of the requested granularity and, optionally, by additional dimensions. Supports filtering via the segment IR, currency conversion for monetary metrics, and cohort analysis.

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/analytics/query" method="post" path="/analytics/query" -->
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

### Parameters

| Parameter                                                                                            | Type                                                                                                 | Required                                                                                             | Description                                                                                          |
| ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| `requestBody`                                                                                        | [Operations\PostAnalyticsQueryRequestBody](../../Models/Operations/PostAnalyticsQueryRequestBody.md) | :heavy_check_mark:                                                                                   | N/A                                                                                                  |
| `tenant`                                                                                             | *?string*                                                                                            | :heavy_minus_sign:                                                                                   | Unique identifier of the tenant in the system (usually a store identifier)                           |

### Response

**[?Operations\PostAnalyticsQueryResponse](../../Models/Operations/PostAnalyticsQueryResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## listMetrics

Returns every metric the analytics query endpoint accepts, with what the number means, the approximations it carries, and which filters and group-by dimensions it will honour. Intended to be read before building a query: a filter listed under `unsupported` is a 400, and one listed under `ignored` is silently not applied.

### Example Usage

<!-- UsageSnippet language="php" operationID="get_/analytics/metrics" method="get" path="/analytics/metrics" -->
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



$response = $sdk->analytics->listMetrics(

);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `tenant`                                                                   | *?string*                                                                  | :heavy_minus_sign:                                                         | Unique identifier of the tenant in the system (usually a store identifier) |

### Response

**[?Operations\GetAnalyticsMetricsResponse](../../Models/Operations/GetAnalyticsMetricsResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |