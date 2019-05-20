## Commands and queries

The web API is split into commands and queries.  Commands 
are requests that change the system, while queries are 
read only requests.

Both for commands and queries you have to use the HTTP POST 
method.  That is because in HTTP GET requests are not allowed 
to have a body. 

`POST /api/command`

`POST /api/query`