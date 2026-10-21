# Product


## Fields

| Field                                                                 | Type                                                                  | Required                                                              | Description                                                           |
| --------------------------------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------- |
| `id`                                                                  | *string*                                                              | :heavy_check_mark:                                                    | N/A                                                                   |
| `title`                                                               | *string*                                                              | :heavy_check_mark:                                                    | N/A                                                                   |
| `image`                                                               | [Components\ProductImage](../../Models/Components/ProductImage.md)    | :heavy_check_mark:                                                    | N/A                                                                   |
| `collections`                                                         | array<[Components\Collection](../../Models/Components/Collection.md)> | :heavy_check_mark:                                                    | N/A                                                                   |
| `planGroups`                                                          | array<*string*>                                                       | :heavy_check_mark:                                                    | Subscription plan group IDs associated with this product              |