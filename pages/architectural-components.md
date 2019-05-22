# Soda components

### Soda user interface

The Soda user interface is a web application that allows any user 
with access to get login and access Soda without installing any 
new software. 

### Soda application

The Soda application is the server of the Soda user interface as 
well as the Soda web API.

The Soda application is an executable Java jar file that only 
requires a Java runtime. Open JDK 8+ is required and Open JDK 11+ 
is recommended. 

The Soda application connects to the Soda database for the majority 
of the user interactions.  It also can launch Spark jobs and 
access the Soda file storage.

The Soda application is stateless.  Which implies that multiple 
Soda application instances can be deployed behind a load 
balancer.

### Soda database

The Soda database contains the following metadata about the data
in the data lake:

* Users
* Permissions
* Connections
  * Storage location details
  * Access credentials
* Metrics
  * Metadata about the data like the type, distributions, etc  
* Tests
  * Expectations about the data
* Scheduling
  * When should each test be executed to monitor the data
* Test results
* Alerts
  * Failed test results

### Soda Spark cluster 

The Soda Spark cluster is used for the following purposes:

* Execute tests on the data
* Create samples of the data
* Profile the data to build up metadata on the columns and structure of the data

Because we use Spark, it's easy to scale in terms of the amount of 
datasets as well as the size of the datasets.

Spark is also a common component in new architectures that is available 
and supported on all cloud platforms. 

### Soda file storage

TODO explain what the Soda file storage contains

#### Soda test suggester

TODO 

##### Soda Application Logs

TODO What do the logs contain, where are they sent. They do not contain the actual data.