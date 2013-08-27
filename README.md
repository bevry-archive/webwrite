spec
====

Specification for backends for how to interact with the Web Write GUIs


## REST

- `/#{collectioName}/#{relativePath}`
  - `GET` fetch the files at that relative path or collection
  - `PUT` create a new file at that relative path or collection
  - `POST` update the file at that relative path or collection
  - `DELETE` delete the files at that relative path or collection
  - Results are in the following format:

      ``` javascript
      {
        "success": true/false,
        "message": String,
        "data": Object/Array
      }
      ```

- `/_collections/`
  - `GET` fetch the collections that we have and their details

- `/_authenticate/`
  - `GET` the authentication page
  - Query String Paramaters:
    - `goto` the url to redirect to after the authentication has completed
      - performs a `POST` with the following JSON
