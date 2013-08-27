# Spec

Specification for backends for how to interact with the Web Write GUIs


## REST

All responses are returned in JSON and in the format of:

- `success`: Boolean - did the request complete successfully?
	- e.g. `true`
- `message`: String - the success or error message of what we did
	- e.g. `"The action completed successfully"`
- `data`: Object/Array 
	- e.g. `[{id:1,...}, {id:2:,...}]`

Available routes are:

- `/<collectioName>/[relativePath]`
	- Methods:
		- `GET` fetch the files at that relative path or collection
		- `PUT` create a new file at that relative path or collection
		- `POST` update the file at that relative path or collection
		- `DELETE` delete the files at that relative path or collection
	
	- Query String Fields:
		- `extension`: String - searches within the extension
			- e.g. `"md"`
		- `mime`: String - searches within the MIME content type
			- e.g. `"image"`
		- `limit`: Number - amount of items to return within the page
			- e.g. `10`
			- default `10`
		- `offset`: Number - the offset of items to start the paging from
			- e.g. `15`
		- `page`: Number - the page of data to return
			- e.g. `2`
			- default `1`
		- `filter`: JSON - a NoSQL filter to apply
			- e.g. `{"relativePath": $startsWith: "a"}`
		- `additionFields`: Array - extra fields to return
			- e.g. `["relativeOutDirPath', "contentRendered"]`

	- Result Data:

		``` javascript
		[
			{
				"id": 1,
				"title": "Hello World"
			}
		]
		```

- `/_collections/`
	- Methods:
		- `GET` fetch the collections that we have and their details
	
	- Result Data:

		``` javascript
		[
			{
				"id": "database"
			}
		]
		```

- `/_authenticate/`
	- Methods:
		- `GET` the authentication page
	
	- Query String Fields:
		- `goto`: String - the url to redirect to after the authentication has completed
