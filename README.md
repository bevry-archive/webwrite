# Spec

Specification for backends for how to interact with the Web Write GUIs


## REST

All responses are returned in JSON and in the format of:

``` javascript
var response = {	
	// Success: Boolean
	// Did the request complete successfully?
	success: true,

	// Message: String
	// The success or error message of what we did
	message: "Result returned successfully",

	// Data: Object/Array
	data: [
		{
			id: 1
			// ...
		},
		{
			id: 2
			// ...
		}
	]
};
```

### Route: `http://site.com/restapi/`

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

``` javascript
var request = {
	query: {
		// Extension: String
		// Searches within the extension
		extension: "md",

		// Mime: String
		// Searches within the MIME content type
		mime: "image",

		// Limit
	}
};
var responseData = {
	// Website Name
	name: "My Website",

	// Website URL
	url: "My Website URL"

	// Any custom file collections
	customFileCollections: [
		{
			id: "posts",
			relativePaths: ["post/2012-12-25 - Happy Christmas.html.md"]
		}
	],

	// Files
	// All files inside the website database
	files: [
		{
			meta: {
				title: "My Blog Post"
			},
			date: "2013-10-30T05:04:18.483Z",
			relativePath: "/post/2012-12-25 - Happy Christmas.html.md",
			filename: "2012-12-25 - Happy Christmas.html.md",
			url: "/post/2012-12-25 - Happy Christmas.html",
			contentType: "@todo",
			encoding: "utf8", // or binary
			source: "@todo",
			contentRendered: "@todo"
		}
	]
};
```

### Route: `http://site.com/restapi/collection/<collectionId>`

- Methods:
	- `GET` fetch the collections that we have and their details


### Route: `http://site.com/restapi/file/<fileRelativePath>`

- Methods:
	- `GET` fetch the files at that relative path or collection
	- `PUT` create a new file at that relative path or collection
	- `POST` update the file at that relative path or collection
	- `DELETE` delete the files at that relative path or collection
