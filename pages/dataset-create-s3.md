### Create an S3 connection
```
> POST /api/command
  Cookie: token=npRXwDmzs31-fa_pY6z4PwXdjmI
  Content-Type: application/json
  {
    "type": "createDatasource",
    "authentication": {
      "token": "testtoken",
      "organisationId": "org1"
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
    "id": "datasource15",
    "organisationId": "org1",
    "name": "Datalake",
    "region": "eu-west-1",
    "bucketName": "data-lake-bucket-name",
    "accessKey": "***AWS_ACCESS_KEY***",
    "secretKey": "***AWS_SECRET_KEY***"
  }
```
### Create a snapshot file dataset
```
> POST /api/command
  Cookie: token=npRXwDmzs31-fa_pY6z4PwXdjmI
  Content-Type: application/json
  {
    "type": "createDataset",
    "authentication": {
      "token": "testtoken",
      "organisationId": "org1"
    },
    "dataset": {
      "type": "snapshotFile",
      "name": "Customers",
      "datasourceId": "datasource15",
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
    "id": "dataset16",
    "organisationId": "org1",
    "name": "Customers",
    "datasourceId": "datasource15",
    "filePattern": [
      "master/",
      "yyyy/MM/dd",
```
      "/customers.parquet"
