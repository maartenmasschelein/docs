### Create a missing values test
```
> POST /api/command
  Cookie: token=8WUolP6Kr-y4KeCZw20LsolpJnQ
  Content-Type: application/json
  {
    "type": "createTest",
    "authentication": {
      "token": "testtoken",
      "organisationId": "org22"
    },
    "test": {
      "title": "All Funds except for the Z-funds should have an annual management fee.",
      "expression": {
        "type": "lessThan",
        "left": {
          "type": "metric",
          "metric": {
            "type": "missingValuesPercentage",
            "datasetId": "dataset123",
            "columnName": "annualManagementFee"
          }
        },
        "right": {
          "type": "number",
          "value": 0.2
        }
      }
    }
  }
< HTTP/1.1 200 OK
  {
    "id": "test23",
    "title": "All Funds except for the Z-funds should have an annual management fee.",
    "expression": {
      "type": "lessThan",
      "left": {
        "type": "metric",
        "metric": {
          "type": "missingValuesPercentage",
          "id": "metric24",
          "testId": "test23",
          "datasetId": "dataset123",
          "columnName": "annualManagementFee"
        }
```
      },
      "right": {
