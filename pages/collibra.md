# Collibra UI flow
### Create and update of Collibra settings
```
> POST /api/command
  Content-Type: application/json
  {
    "type": "updateCollibraSettings",
    "authentication": {
      "token": "testtoken",
      "organisationId": "org1"
    },
    "settings": {
      "type": "collibra",
      "url": "https://shape.collibra.com",
      "username": "Admin",
      "password": "FujFezOl7quaroo",
      "communityName": "Soda community",
      "domainName": "Soda domain"
    }
  }
< HTTP/1.1 200 OK
  {
    "type": "collibra",
    "id": "settings2",
    "url": "https://shape.collibra.com/",
    "username": "Admin",
    "password": "FujFezOl7quaroo",
    "communityName": "Soda community",
    "communityId": "e4fe8f0d-ad0a-4af7-9633-9b98988274ab",
    "domainName": "Soda domain",
    "domainId": "1aef8687-515b-40d3-8dfb-e793c2ab0915"
  }
```

  
### Test Collibra settings
```
> POST /api/command
  Content-Type: application/json
  {
    "type": "testCollibraSettings",
    "authentication": {
      "token": "testtoken",
      "organisationId": "org1"
    }
  }
< HTTP/1.1 200 OK
  {}
```
