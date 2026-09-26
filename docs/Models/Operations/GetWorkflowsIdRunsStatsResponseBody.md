# GetWorkflowsIdRunsStatsResponseBody

Default Response


## Fields

| Field                                                                           | Type                                                                            | Required                                                                        | Description                                                                     |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| `totalRuns`                                                                     | *float*                                                                         | :heavy_check_mark:                                                              | N/A                                                                             |
| `successRuns`                                                                   | *float*                                                                         | :heavy_check_mark:                                                              | N/A                                                                             |
| `failedRuns`                                                                    | *float*                                                                         | :heavy_check_mark:                                                              | N/A                                                                             |
| `nodes`                                                                         | array<string, [Operations\Nodes](../../Models/Operations/Nodes.md)>             | :heavy_check_mark:                                                              | N/A                                                                             |
| `experiments`                                                                   | array<string, [Operations\Experiments](../../Models/Operations/Experiments.md)> | :heavy_check_mark:                                                              | N/A                                                                             |