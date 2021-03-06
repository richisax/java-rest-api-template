```  
████████╗██████╗  █████╗ ██╗   ██╗███████╗██╗     ███████╗████████╗ █████╗ ██████╗ ████████╗
╚══██╔══╝██╔══██╗██╔══██╗██║   ██║██╔════╝██║     ██╔════╝╚══██╔══╝██╔══██╗██╔══██╗╚══██╔══╝
   ██║   ██████╔╝███████║██║   ██║█████╗  ██║     ███████╗   ██║   ███████║██████╔╝   ██║   
   ██║   ██╔══██╗██╔══██║╚██╗ ██╔╝██╔══╝  ██║     ╚════██║   ██║   ██╔══██║██╔══██╗   ██║   
   ██║   ██║  ██║██║  ██║ ╚████╔╝ ███████╗███████╗███████║   ██║   ██║  ██║██║  ██║   ██║   
   ╚═╝   ╚═╝  ╚═╝╚═╝  ╚═╝  ╚═══╝  ╚══════╝╚══════╝╚══════╝   ╚═╝   ╚═╝  ╚═╝╚═╝  ╚═╝   ╚═╝   
                                                                                            
██████╗ ███████╗███████╗████████╗     █████╗ ██████╗ ██╗                                    
██╔══██╗██╔════╝██╔════╝╚══██╔══╝    ██╔══██╗██╔══██╗██║                                    
██████╔╝█████╗  ███████╗   ██║       ███████║██████╔╝██║                                    
██╔══██╗██╔══╝  ╚════██║   ██║       ██╔══██║██╔═══╝ ██║                                    
██║  ██║███████╗███████║   ██║       ██║  ██║██║     ██║                                    
╚═╝  ╚═╝╚══════╝╚══════╝   ╚═╝       ╚═╝  ╚═╝╚═╝     ╚═╝
```       
                                                                 
REST API Template (Java+Netty+Camel+Swagger)
=====================================

A nice, simple REST API template written in Java using [Camel](http://camel.apache.org/) with [Netty](https://github.com/netty/netty) which includs an ErrorHandler and a few sample requests. [Swagger](//swagger.io) support included as well.

*This is a work in progress - contributions are welcome*

## How do you build / run / develop it ?

You will need [gradle](https://gradle.org/) to build (and "deploy" [optional] ). 

Mode | How | How (in debug)
--- | --- | ---
Development option 1| `gradle run` | `gradle run --debug-jvm`
Development option 2| run [com.travelstart.api.Boot](src/main/java/com/travelstart/api/Boot.java) from IDE | run [com.travelstart.api.Boot](src/main/java/com/travelstart/api/Boot.java) in debug mode in IDE
Externally | `gradle installDist`, run script: `build/install/java-rest-api-template/bin/java-rest-api-template` | N/A

## Things to know
- REST Routes are defined in [com.travelstart.api.RestRoutes](src/main/java/com/travelstart/api/RestRoutes.java)
- Errors are handled in [com.travelstart.api.handler.ErrorHandler](src/main/java/com/travelstart/api/handler/ErrorHandler.java)
- Request/Response content handler for logging is in [com.travelstart.api.handler.LoggingHandler](src/main/java/com/travelstart/api/handler/LoggingHandler.java)
- Runs on port 8890 by default - to customise, see [com.travelstart.api.Boot.PORT](src/main/java/com/travelstart/api/Boot.java)
- Uses _CPU Cores x 2_ workers - see [com.travelstart.api.Boot.WORKER_COUNT](src/main/java/com/travelstart/api/Boot.java) to customise

## IDE Support
- Eclipse: `gradle eclipse`
- IntelliJ IDEA: `gradle idea`
- NetBeans: use the gradle plugin

## Example endpoints:
- `/api/ping` - POST/GET that returns a fixed string response
- `/api/booking` - PUT to create a booking - returns the ID in the response
- `/api/booking/{id}` - POST to update a booking given the ID
- `/api/booking/{id}` - GET to retrieve a booking given the ID

## Swagger support:
### Create (once-off):
- `docker create --rm --name swagger-rest-template -p 8081:8080 -e API_URL=http://localhost:8890/api-doc/swagger.json swaggerapi/swagger-ui:v2.2.9`
### Start it:
- `docker start swagger-rest-template`
### Use it:
- goto: http://localhost:8081/ and enter http://localhost:8890/api-doc/swagger.json in the box

## Unit Testing
`gradle test jacocoTestReport`

test result reports at: 
- code coverage: java-rest-api-template/build/reports/jacoco/test/html/index.html
- test summary: java-rest-api-template/build/reports/tests/test/index.html


## Customising the Server

The following system properties can be set to customise the server:

System Property | What
--- | ---
`server.host`| The binding address - default is `localhost` 
`server.port`| The port the server listens on - default is `8890`
`server.workers`| The number of works (threads) available for requests - default is CPU Cores x 2
`server.max-content-length`| The maximum upload size - default is 1MB
