## Second iteration

The second iteration consists adding a new REST resource to the project, such that the following curl:

```
curl -X GET http://localhost:8080/messages?limit=10
```

produces the JSON output:

```json
{
 "count": 2,
 "messages": [
	 {
			"user": "bob",
			"message": "bar",
			"postedAt": "2012-04-23T18:25:00.511Z"
	 },
   {
		 "user": "bob",
		 "message": "bar",
		 "postedAt": "2012-04-23T18:20:00.511Z"
   }
 ]
}
```

### Requirements:

- Endpoint matches specification above
	- `count` is the number of messages that have been submitted to the server
	- The messages array is the most recent messages.
	- The limit query parameter should be respected
- Messages are stored in a postgres database
	- should be created in a docker image, based on the [official docker image](https://registry.hub.docker.com/_/postgres/)
	- schema is initialized during the bootup of the project. The database and user can be created manually.
- A `MessagesDAO` class abstracts Java's interaction with the database.
	- Resource -> Service -> DAO -> Database
	- DAO should return DTOs to service layer.
	- Spring JDBC should be used for database calls
	- [More information on DAO pattern](https://en.wikipedia.org/wiki/Data_access_object)
- Unit Tests are written for all classes
	- All dependencies are mocked	
	- Mockito is used for mock objects
	- Jacoco is used for code coverage reporting
  - Code coverage is over 60%
