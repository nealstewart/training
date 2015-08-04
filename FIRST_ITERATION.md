## First Iteration

Create a dockerized Jetty web service using Jersey that responds to the
following request from `curl`:

```sh
curl -X POST http://localhost:8080/messages -d '{"user":"foo", "message": "bar"}'
```

and produces a response with header Content-Type: application/json and JSON payload:

```json
{
	"user": "foo",
	"message": "bar",
	"postedAt": "2012-04-23T18:25:43.511Z"
}
```

Furthermore, the service must meet the following requirements:

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
* Date format in JSON must be in [ISO 8601](https://en.wikipedia.org/?title=ISO_8601)
