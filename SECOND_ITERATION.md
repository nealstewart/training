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

Requirements:
- Endpoint matches specification above
	- `messageCount` is the number of messages in the messages array
	- Date format in JSON must be in [ISO 8601](https://en.wikipedia.org/?title=ISO_8601)
	- The messages array is the list of the 10 (or less) most recent messages being produced by the POST resource `/messages/names/$name`
	- The `lastMessage` field contains the timestamp of the last message that was produced.
- Messages are stored in a postgres database
	- should be created in a docker image, based on the [official docker image](https://registry.hub.docker.com/_/postgres/)
	- schema is initialized during the bootup of the project. The database and user can be created manually.
	- 
- A `MessagesDAO` class abstracts Java's interaction with the database.
	- Resource -> Service -> DAO -> Database
	- DAO should return DTOs to service layer.
	- Spring JDBC should be used for database calls
	- [More information on DAO pattern](https://en.wikipedia.org/wiki/Data_access_object)
- Unit Tests are written for all classes
	- All dependencies are mocked	
	- Mockito is used for mock objects
	- Jacoco is used for code coverage reporting
  - Code covereage is over 60%
