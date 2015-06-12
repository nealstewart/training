# Code Challenge
The goal of the challenge is to create a dockerized web service such that the following HTTP request, for the variable `$name`
```sh
curl -X POST http://localhost:8080/messages/names/$name
```
produces a response with header Content-Type: application/json and JSON payload:
```json
{"message": { "content": "Hello $name"}}
```
Furthermore, the service must meet the following requirements:
* Code must be stored on github and be in a fork of this repository
* Code must be written in java
* Maven is used to build the project and produce a war file
* Jetty is used as the web server
* The REST interface is produced by Jersey
* It must have a class `MessageResource` containing the REST API definition and a `MessageService` class, that performs the logic.
* It must use Spring for injecting the singleton `MessageService` bean into the `MessageResource` bean
* JAX RS / Jackson is used for serializing a `Message` DTO class into the REST response.
* The project must be built as a docker image using a Dockerfile starting with `FROM ubuntu:trusty`, and run as a docker container.
* The docker image must be built using maven using mvn package
* Jetty, including the web-application, should start when docker start is issued for the created docker image.
* You have to write every line of code yourself, but you can ask anyone for help. No-one is required to help though.

## Second iteration
The second iteration consists adding a new REST resource to the project, such that the following curl:
```
curl -X GET http://localhost:8080/messages/recent
```
produces the JSON output:
```json
{"messageCount": 2,
 "lastMessage": "2012-04-23T18:25:43.511Z",
 "messages": [
   {"message": { "content": "hello $name1"}},
   {"message": { "content": "hello $name2"}}
 ]
}
```
The following requirements also have to be met:
* `messageCount` is the number of messages in the messages array
* The messages array is the list of the 10 (or less) most recent messages being produced by the POST resource `/messages/names/$name`
* The `lastMessage` field contains the timestamp of the last message that was produced.
* The messages are stored in a postgres database
* The database schema is initialized during the bootup of the project. The database and user can be created manually.
* The database is accessed using Spring JDBC
* There is a `MessagesDAO` class that handles the interaction with the database.
* The project build runs JUnit tests using Mockito for mock objects producing over 60% line coverage measured using Jacoco.
