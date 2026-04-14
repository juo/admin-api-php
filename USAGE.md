<!-- Start SDK Example Usage [usage] -->
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