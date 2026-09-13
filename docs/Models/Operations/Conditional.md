# Conditional


## Fields

| Field                                                                                | Type                                                                                 | Required                                                                             | Description                                                                          |
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ |
| `fields`                                                                             | array<*string*>                                                                      | :heavy_check_mark:                                                                   | The dimension keys this rule covers.                                                 |
| `requires`                                                                           | *string*                                                                             | :heavy_check_mark:                                                                   | The request shape under which these fields are applied. Outside it they are ignored. |