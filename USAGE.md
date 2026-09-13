<!-- Start SDK Example Usage [usage] -->
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