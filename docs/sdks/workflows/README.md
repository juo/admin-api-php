# Workflows

## Overview

Interactive customer-facing flows for retention, dunning, and onboarding. Define steps, publish, and track execution runs and experiments.

### Available Operations

* [list](#list) - List workflows
* [create](#create) - Create a workflow
* [get](#get) - Get a workflow
* [update](#update) - Update a workflow
* [delete](#delete) - Delete a workflow
* [archive](#archive) - Archive a workflow
* [duplicate](#duplicate) - Duplicate a workflow
* [publish](#publish) - Publish a workflow
* [listRuns](#listruns) - List workflow runs
* [unpublish](#unpublish) - Unpublish a workflow
* [getRun](#getrun) - Get a workflow run
* [exportRuns](#exportruns) - Export workflow runs as CSV
* [getWorkflowsIdRunsExport](#getworkflowsidrunsexport) - Download workflow runs CSV
* [getRunStats](#getrunstats) - Get workflow run statistics
* [concludeExperiment](#concludeexperiment) - Conclude a workflow experiment

## list

Returns a paginated list of workflow definitions. By default excludes archived workflows. Use `includeArchived` to include them. Use `filterNonInteractive` to return only workflows that have at least one customer-facing input step (i.e. previewable in the editor).

### Example Usage

<!-- UsageSnippet language="php" operationID="get_/workflows" method="get" path="/workflows" -->
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

$request = new Operations\GetWorkflowsRequest();

$response = $sdk->workflows->list(
    request: $request
);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                        | Type                                                                             | Required                                                                         | Description                                                                      |
| -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| `$request`                                                                       | [Operations\GetWorkflowsRequest](../../Models/Operations/GetWorkflowsRequest.md) | :heavy_check_mark:                                                               | The request object to use for the request.                                       |

### Response

**[?Operations\GetWorkflowsResponse](../../Models/Operations/GetWorkflowsResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## create

Creates a new workflow definition in draft status. A workflow defines a trigger type, a set of steps (each optionally with an action), and transitions between steps. Draft workflows must be published before they can be triggered by subscription lifecycle events.

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/workflows" method="post" path="/workflows" -->
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

$requestBody = new Operations\PostWorkflowsRequestBody(
    name: '<value>',
    triggerType: '<value>',
    trigger: new Operations\PostWorkflowsTrigger(
        id: '<id>',
        type: '<value>',
        category: Operations\PostWorkflowsCategoryTimeBased::TimeBased,
    ),
    steps: [],
);

$response = $sdk->workflows->create(
    requestBody: $requestBody
);

if ($response->workflow !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                  | Type                                                                                       | Required                                                                                   | Description                                                                                |
| ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| `requestBody`                                                                              | [Operations\PostWorkflowsRequestBody](../../Models/Operations/PostWorkflowsRequestBody.md) | :heavy_check_mark:                                                                         | N/A                                                                                        |
| `tenant`                                                                                   | *?string*                                                                                  | :heavy_minus_sign:                                                                         | Unique identifier of the tenant in the system (usually a store identifier)                 |

### Response

**[?Operations\PostWorkflowsResponse](../../Models/Operations/PostWorkflowsResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## get

Retrieves the full definition of a workflow including its trigger type, step definitions, transitions, canvas layout metadata, and current publication status.

### Example Usage

<!-- UsageSnippet language="php" operationID="get_/workflows/{id}" method="get" path="/workflows/{id}" -->
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



$response = $sdk->workflows->get(
    id: '23c90300-32f5-47ad-8e87-28f66e19821b'
);

if ($response->workflow !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `id`                                                                       | *string*                                                                   | :heavy_check_mark:                                                         | The workflow identifier                                                    |
| `tenant`                                                                   | *?string*                                                                  | :heavy_minus_sign:                                                         | Unique identifier of the tenant in the system (usually a store identifier) |

### Response

**[?Operations\GetWorkflowsIdResponse](../../Models/Operations/GetWorkflowsIdResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## update

Replaces the full definition of a workflow. Updates the name, description, trigger, steps, transitions, and canvas metadata. This is a full replacement — provide all fields you want to keep. Typically only draft or unpublished workflows should be updated.

### Example Usage

<!-- UsageSnippet language="php" operationID="put_/workflows/{id}" method="put" path="/workflows/{id}" -->
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



$response = $sdk->workflows->update(
    id: 'fe3804c6-fba0-4562-8b20-ff8dd0453b61',
    requestBody: $requestBody

);

if ($response->workflow !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                     | Type                                                                                          | Required                                                                                      | Description                                                                                   |
| --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| `id`                                                                                          | *string*                                                                                      | :heavy_check_mark:                                                                            | The workflow identifier                                                                       |
| `tenant`                                                                                      | *?string*                                                                                     | :heavy_minus_sign:                                                                            | Unique identifier of the tenant in the system (usually a store identifier)                    |
| `requestBody`                                                                                 | [?Operations\PutWorkflowsIdRequestBody](../../Models/Operations/PutWorkflowsIdRequestBody.md) | :heavy_minus_sign:                                                                            | N/A                                                                                           |

### Response

**[?Operations\PutWorkflowsIdResponse](../../Models/Operations/PutWorkflowsIdResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## delete

Soft-deletes a workflow. The workflow is marked as deleted and removed from active use. Historical run data is preserved for reporting.

### Example Usage

<!-- UsageSnippet language="php" operationID="delete_/workflows/{id}" method="delete" path="/workflows/{id}" -->
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



$response = $sdk->workflows->delete(
    id: 'b6e837f2-f623-4a89-960f-c6ba4c588b7d'
);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `id`                                                                       | *string*                                                                   | :heavy_check_mark:                                                         | The workflow identifier                                                    |
| `tenant`                                                                   | *?string*                                                                  | :heavy_minus_sign:                                                         | Unique identifier of the tenant in the system (usually a store identifier) |

### Response

**[?Operations\DeleteWorkflowsIdResponse](../../Models/Operations/DeleteWorkflowsIdResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## archive

Archives a workflow, removing it from active triggering without deleting it. Archived workflows no longer match incoming subscription lifecycle events. Use to retire outdated workflows while preserving run history for reporting.

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/workflows/{id}/archive" method="post" path="/workflows/{id}/archive" -->
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



$response = $sdk->workflows->archive(
    id: 'd8a00e2f-35b4-48fa-8340-a2a3c39997c1'
);

if ($response->workflow !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `id`                                                                       | *string*                                                                   | :heavy_check_mark:                                                         | The workflow identifier                                                    |
| `tenant`                                                                   | *?string*                                                                  | :heavy_minus_sign:                                                         | Unique identifier of the tenant in the system (usually a store identifier) |

### Response

**[?Operations\PostWorkflowsIdArchiveResponse](../../Models/Operations/PostWorkflowsIdArchiveResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## duplicate

Creates an exact copy of an existing workflow as a new draft. Useful for creating variations of a working workflow without modifying the live version. The copy includes all steps, transitions, and canvas metadata.

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/workflows/{id}/duplicate" method="post" path="/workflows/{id}/duplicate" -->
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



$response = $sdk->workflows->duplicate(
    id: '0b5b28ee-6963-47f5-82af-718c73fc8e26'
);

if ($response->workflow !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `id`                                                                       | *string*                                                                   | :heavy_check_mark:                                                         | The workflow identifier                                                    |
| `tenant`                                                                   | *?string*                                                                  | :heavy_minus_sign:                                                         | Unique identifier of the tenant in the system (usually a store identifier) |

### Response

**[?Operations\PostWorkflowsIdDuplicateResponse](../../Models/Operations/PostWorkflowsIdDuplicateResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## publish

Publishes a draft workflow, making it active and eligible to be triggered by matching subscription lifecycle events. Only one workflow per trigger type can be published at a time; publishing a new one replaces the previous published version for that trigger type.

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/workflows/{id}/publish" method="post" path="/workflows/{id}/publish" -->
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



$response = $sdk->workflows->publish(
    id: 'ce745abb-875e-4fb6-87fe-6c969a41f3eb'
);

if ($response->workflow !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `id`                                                                       | *string*                                                                   | :heavy_check_mark:                                                         | The workflow identifier                                                    |
| `tenant`                                                                   | *?string*                                                                  | :heavy_minus_sign:                                                         | Unique identifier of the tenant in the system (usually a store identifier) |

### Response

**[?Operations\PostWorkflowsIdPublishResponse](../../Models/Operations/PostWorkflowsIdPublishResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## listRuns

Returns a paginated list of execution runs for a specific workflow. Each run represents one customer's execution instance, including their current step, context, and status (in-progress, completed, failed, canceled). Results are cursor-paginated.

### Example Usage

<!-- UsageSnippet language="php" operationID="get_/workflows/{id}/runs" method="get" path="/workflows/{id}/runs" -->
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

$request = new Operations\GetWorkflowsIdRunsRequest(
    id: 'a7e3f782-57d2-4f55-9226-c33b566128a2',
);

$response = $sdk->workflows->listRuns(
    request: $request
);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                                    | Type                                                                                         | Required                                                                                     | Description                                                                                  |
| -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| `$request`                                                                                   | [Operations\GetWorkflowsIdRunsRequest](../../Models/Operations/GetWorkflowsIdRunsRequest.md) | :heavy_check_mark:                                                                           | The request object to use for the request.                                                   |

### Response

**[?Operations\GetWorkflowsIdRunsResponse](../../Models/Operations/GetWorkflowsIdRunsResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## unpublish

Unpublishes an active workflow, moving it back to draft status. No new runs are started after unpublishing. In-flight runs continue to completion on their existing workflow snapshot. Use to pause a live workflow for editing without deleting run history.

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/workflows/{id}/unpublish" method="post" path="/workflows/{id}/unpublish" -->
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



$response = $sdk->workflows->unpublish(
    id: '9954cec4-dec4-40a6-84b2-3509cd384370'
);

if ($response->workflow !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `id`                                                                       | *string*                                                                   | :heavy_check_mark:                                                         | The workflow identifier                                                    |
| `tenant`                                                                   | *?string*                                                                  | :heavy_minus_sign:                                                         | Unique identifier of the tenant in the system (usually a store identifier) |

### Response

**[?Operations\PostWorkflowsIdUnpublishResponse](../../Models/Operations/PostWorkflowsIdUnpublishResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## getRun

Retrieves the current execution state of a specific workflow run, including the active step, accumulated context variables, customer responses to input steps, and overall run status.

### Example Usage

<!-- UsageSnippet language="php" operationID="get_/workflows/{id}/runs/{runId}" method="get" path="/workflows/{id}/runs/{runId}" -->
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



$response = $sdk->workflows->getRun(
    id: '4e28cdd8-63a6-448c-92df-06346701c556',
    runId: '93b4b60b-63d5-4750-9cfb-ff44d0ed7148'

);

if ($response->workflowRunState !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `id`                                                                       | *string*                                                                   | :heavy_check_mark:                                                         | The workflow identifier                                                    |
| `runId`                                                                    | *string*                                                                   | :heavy_check_mark:                                                         | The workflow run identifier                                                |
| `tenant`                                                                   | *?string*                                                                  | :heavy_minus_sign:                                                         | Unique identifier of the tenant in the system (usually a store identifier) |

### Response

**[?Operations\GetWorkflowsIdRunsRunIdResponse](../../Models/Operations/GetWorkflowsIdRunsRunIdResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## exportRuns

Creates a short-lived signed URL (valid 60 seconds) for downloading all workflow runs for the specified workflow as a CSV file. The CSV includes per-step entry/exit counts, customer response data, experiment variant assignments, and completion outcomes. Fetch the returned URL to download the file.

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/workflows/{id}/runs/export" method="post" path="/workflows/{id}/runs/export" -->
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



$response = $sdk->workflows->exportRuns(
    id: '76b02637-c007-48e8-917f-d6b559878860'
);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `id`                                                                       | *string*                                                                   | :heavy_check_mark:                                                         | The workflow identifier                                                    |
| `tenant`                                                                   | *?string*                                                                  | :heavy_minus_sign:                                                         | Unique identifier of the tenant in the system (usually a store identifier) |

### Response

**[?Operations\PostWorkflowsIdRunsExportResponse](../../Models/Operations/PostWorkflowsIdRunsExportResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## getWorkflowsIdRunsExport

Streams the CSV file for all workflow runs. Accessed via the signed URL returned by the exportRuns operation — not callable directly with an API key.

### Example Usage

<!-- UsageSnippet language="php" operationID="get_/workflows/{id}/runs/export" method="get" path="/workflows/{id}/runs/export" -->
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



$response = $sdk->workflows->getWorkflowsIdRunsExport(
    token: '<value>',
    shop: '<value>',
    id: '59fc814d-89ba-4a9b-9f9f-cc7704d1b62f'

);

if ($response->statusCode === 200) {
    // handle response
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `token`                                                                    | *string*                                                                   | :heavy_check_mark:                                                         | N/A                                                                        |
| `shop`                                                                     | *string*                                                                   | :heavy_check_mark:                                                         | N/A                                                                        |
| `id`                                                                       | *string*                                                                   | :heavy_check_mark:                                                         | N/A                                                                        |
| `tenant`                                                                   | *?string*                                                                  | :heavy_minus_sign:                                                         | Unique identifier of the tenant in the system (usually a store identifier) |

### Response

**[?Operations\GetWorkflowsIdRunsExportResponse](../../Models/Operations/GetWorkflowsIdRunsExportResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## getRunStats

Returns aggregate execution statistics for a workflow: total, successful, and failed run counts; per-node (step) entry execution counts; and per-experiment-step variant enrollment counts with per-metric conversion rates. Use to power analytics dashboards and experiment result views.

### Example Usage

<!-- UsageSnippet language="php" operationID="get_/workflows/{id}/runs/stats" method="get" path="/workflows/{id}/runs/stats" -->
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



$response = $sdk->workflows->getRunStats(
    id: 'd0239613-0523-40f7-b38c-b9c7e656f4bc'
);

if ($response->object !== null) {
    // handle response
}
```

### Parameters

| Parameter                                                                  | Type                                                                       | Required                                                                   | Description                                                                |
| -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `id`                                                                       | *string*                                                                   | :heavy_check_mark:                                                         | The workflow identifier                                                    |
| `tenant`                                                                   | *?string*                                                                  | :heavy_minus_sign:                                                         | Unique identifier of the tenant in the system (usually a store identifier) |

### Response

**[?Operations\GetWorkflowsIdRunsStatsResponse](../../Models/Operations/GetWorkflowsIdRunsStatsResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |

## concludeExperiment

Concludes an A/B experiment on a specific workflow step. Use `select_winner` with a `winnerVariantId` to promote one variant as the permanent path for all future runs, or `stop` to end the experiment without selecting a winner and revert to the control path. In-flight runs continue on their already-assigned variant.

### Example Usage

<!-- UsageSnippet language="php" operationID="post_/workflows/{id}/experiment/{stepId}/conclude" method="post" path="/workflows/{id}/experiment/{stepId}/conclude" -->
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

$requestBody = new Operations\PostWorkflowsIdExperimentStepIdConcludeRequestBody(
    action: Operations\ActionStop::Stop,
);

$response = $sdk->workflows->concludeExperiment(
    id: 'c268c34b-7e78-442b-bc2f-64f1ed0a6566',
    stepId: '<id>',
    requestBody: $requestBody

);

if ($response->statusCode === 200) {
    // handle response
}
```

### Parameters

| Parameter                                                                                                                                      | Type                                                                                                                                           | Required                                                                                                                                       | Description                                                                                                                                    |
| ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`                                                                                                                                           | *string*                                                                                                                                       | :heavy_check_mark:                                                                                                                             | The workflow identifier                                                                                                                        |
| `stepId`                                                                                                                                       | *string*                                                                                                                                       | :heavy_check_mark:                                                                                                                             | The experiment step identifier                                                                                                                 |
| `requestBody`                                                                                                                                  | [Operations\PostWorkflowsIdExperimentStepIdConcludeRequestBody](../../Models/Operations/PostWorkflowsIdExperimentStepIdConcludeRequestBody.md) | :heavy_check_mark:                                                                                                                             | N/A                                                                                                                                            |
| `tenant`                                                                                                                                       | *?string*                                                                                                                                      | :heavy_minus_sign:                                                                                                                             | Unique identifier of the tenant in the system (usually a store identifier)                                                                     |

### Response

**[?Operations\PostWorkflowsIdExperimentStepIdConcludeResponse](../../Models/Operations/PostWorkflowsIdExperimentStepIdConcludeResponse.md)**

### Errors

| Error Type          | Status Code         | Content Type        |
| ------------------- | ------------------- | ------------------- |
| Errors\APIException | 4XX, 5XX            | \*/\*               |