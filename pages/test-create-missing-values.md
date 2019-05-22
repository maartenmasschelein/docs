### Create a missing values test
```
> POST /api/command
  Cookie: token=npRXwDmzs31-fa_pY6z4PwXdjmI
  Content-Type: application/json
  {
    "type": "createTest",
    "authentication": {
      "token": "testtoken",
      "organisationId": "org1"
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
    "id": "test12",
    "title": "All Funds except for the Z-funds should have an annual management fee.",
    "expression": {
      "type": "lessThan",
      "left": {
        "type": "metric",
        "metric": {
          "type": "missingValuesPercentage",
          "id": "metric13",
```
          "testId": "test12",
          "datasetId": "dataset123",
