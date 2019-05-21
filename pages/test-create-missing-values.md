### Create a missing values test
```
> POST /api/command
  Content-Type: application/json
  {
    "type": "createTest",
    "authentication": {
      "token": "testtoken",
      "organisationId": "to1"
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
    "id": "test3",
    "title": "All Funds except for the Z-funds should have an annual management fee.",
    "expression": {
      "type": "lessThan",
      "left": {
        "type": "metric",
        "metric": {
          "type": "missingValuesPercentage",
          "id": "metric4",
          "testId": "test3",
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
```
