## Third Iteration

Consume the REST API built previously for a chat application.

- Use a NodeJS docker image
	- https://registry.hub.docker.com/_/node/
- Use Grunt or Gulp for build scripts
	- `grunt test` or `gulp test` should run Jasmine unit tests from the project root
- Use AngularJS for building the client-side application
	- A service should be used for consuming the REST API
	- A controller should be used to display data from the service
- Use Browserify and CommonJS to build client-side files.
- Use an ExpressJS server
	- Serves HTML/CSS files
	- Serves Browserify bundle
- Use Jasmine to write unit tests for the client and server.
