## Authentication

Here's an example login request:

```
> POST /api/command
  Content-Type: application/json
  {
    "type": "login",
    "username": "***YOUR_USERNAME_GOES_HERE***",
    "password": "***YOUR_PASSWORD_GOES_HERE***"
  }
 
< HTTP/1.1 200 OK
  {
    "token": "***GENERATED_TOKEN***",
    "organisationId": "***ORGANISATION_ID***",
    "user": {
      "id": "user3",
      "email": "tom@sodadata.io"
    },
    "organisations": [
      {
        "id": "org1",
        "name": "Soda Data"
      }
    ]
  }
```

Next in requests, authentication is provided in the JSON 
body of HTTP requests
```
{
  ...
  "authentication": {
    "token": "C--YeHIQvyS16Q4169xM37mz6qs",
    "organisationId": "org1"
  }
  ...
}
``` 

Where `xxxxx` is the authentication token and the `organisationId` 
are obtained from the login.