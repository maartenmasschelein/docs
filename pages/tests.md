## Tests

Create a new test

```
> POST /api/command
  {
    "type": "createTest",
    "authentication": {
      "token": "testtoken",
      "organisationId": "to1"
    },
    "test": {
      "expression": {
        "type": "lessThan",
        "left": {
          "type": "metric",
          "metric": {
            "type": "missingValuesCount",
            "columnName": "customerId"
          }
        },
        "right": {
          "type": "number",
          "value": 2.0
        }
      }
    }
  }
```

### Column customerId should not have more than 2% missing values
```
{
  "expression": {
    "type": "lessThan",
    "left": {
      "type": "metric",
      "metric": {
        "type": "missingValuesCount",
        "columnName": "customerId"
      }
    },
    "right": {
      "type": "number",
      "value": 2.0
    }
  }
}
```
# Column customerId should not have more than 2% missing values with customized missing values
```
{
  "expression": {
    "type": "lessThan",
    "left": {
      "type": "metric",
      "metric": {
        "type": "missingValuesCount",
        "columnName": "customerId",
        "missingValues": [
          {
            "type": "null"
          },
          {
            "type": "emptyString"
          },
          {
            "type": "whitespace"
          },
          {
            "type": "text",
            "text": "no value"
          },
          {
            "type": "text",
            "text": "n/a"
          }
        ]
      }
    },
    "right": {
      "type": "number",
      "value": 2.0
    }
  }
}
```
# The average of today should not increase more than 10 nor decrease more than 10
```
{
  "expression": {
    "type": "between",
    "lowerBound": -10.0,
    "upperBound": 10.0,
    "numericValueExpression": {
      "type": "historicalDiff",
      "metricExpression": {
        "type": "metric",
        "metric": {
          "type": "average",
          "datasetId": "datasetId123",
          "columnName": "currentNav"
        }
      }
    }
  }
}
```
