### Create an S3 connection
```
> POST /api/command
  Cookie: token=8WUolP6Kr-y4KeCZw20LsolpJnQ
  Content-Type: application/json
  {
    "type": "createDatasource",
    "authentication": {
      "token": "testtoken",
      "organisationId": "org26"
    },
    "datasource": {
      "type": "awsS3",
      "name": "Datalake",
      "region": "eu-west-1",
      "bucketName": "data-lake-bucket-name",
      "accessKey": "***AWS_ACCESS_KEY***",
      "secretKey": "***AWS_SECRET_KEY***"
    },
    "skipValidation": true
  }
< HTTP/1.1 200 OK
  {
    "type": "awsS3",
    "id": "datasource27",
    "organisationId": "org26",
    "name": "Datalake",
    "region": "eu-west-1",
```
    "bucketName": "data-lake-bucket-name",
### Create a snapshot file dataset
```
    "accessKey": "***AWS_ACCESS_KEY***",
    "secretKey": "***AWS_SECRET_KEY***"
  }
> POST /api/command
  Cookie: token=8WUolP6Kr-y4KeCZw20LsolpJnQ
  Content-Type: application/json
  {
    "type": "createDataset",
    "authentication": {
      "token": "testtoken",
      "organisationId": "org26"
    },
    "dataset": {
      "type": "snapshotFile",
      "name": "Customers",
      "datasourceId": "datasource27",
      "filePattern": [
        "master/",
        "yyyy/MM/dd",
        "/customers.parquet"
      ],
      "fileType": "parquet"
    },
    "skipSample": true,
    "skipColumnNames": true
  }
< HTTP/1.1 200 OK
  {
    "type": "snapshotFile",
    "id": "dataset28",
    "organisationId": "org26",
    "name": "Customers",
    "datasourceId": "datasource27",
    "filePattern": [
      "master/",
      "yyyy/MM/dd",
      "/customers.parquet"
    ],
    "fileType": "parquet"
  }
```
