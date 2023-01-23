An extension of the [API Standards](../API_STANDARDS.md), with implementation details specific to development of RESTful APIs for ONS.

## RESTful API Structure and Syntax

### Syntax & types

  * Field names snake case, e.g. `total_count`
  * Use appropriate types for fields, e.g. numbers should be ints not strings
  * Timestamps should be UTC (optionally, with a timezone)
  * Root endpoint IDs should always be referred to as `id`, rather than name-spaced. All IDs under this level will need descriptive placeholder names. e.g. /datasets/<id>/editions/<edition> where /datasets is the root endpoint

### Methods & Behaviours
 * Use the `GET` method for search endpoints
 * `POST` endpoints should typically generate IDs, and these should use GUIDs not auto-incrementing counts

 ### Links
* All endpoints must return a `links.self` subdoc in their response,
* Resources should avoid a nested list by having a links to list endpoints
* Responses must contain fully qualified URLs, though this may be managed by the API router
* `Links` object contains descriptively named objects which each contain
  an `id` (optional) and `url` field e.g.
  ```
  {  
      "id":"1234",
      "data":"i have stuff",
      "links": {  
          "latest_resource": {  
              "id":"5678",
              "url":"/thisapi/1234/subresources/5678"
          },
          "external": {  
              "id":"3456",
              "url":"/extresources/3456"
          },
          "subresources":{
              "url":"/thisapi/1234/subresources"
          },
          "self":{
              "id":"1234",
              "url":"/thisapi/1234"
          }
      }
  }
  ```
* Resources may link to their direct parent, a child list, or any relevant
  external resources. Resources which are many layers deep in an API do not need
  to contain links to all higher elements e.g. the resource at
  `/datasets/1234/editions/2345/versions/1` would contain a link to
  `/datasets/1234/editions/2345` but not to `/datasets/1234`


### Returning errors
  * **Errors** should return a status code and a JSON payload with the error message
      * `errors` array containing error messages


### Returning lists or search results
Search/list endpoints should contain the following fields: `count`, `limit`, `offset`, `total_count`, `items`

The fields work as:

* `limit` - max number of items we're returning in this response.
    * If value is not set, a configurable default limit should be used, unless otherwise stated this should be set to a value of `20`.
    * The limit value can be set to `0` to return `0` items, so an API user can obtain the metadata for the list endpoint.

* `count` - how many items are actually present in the response.

* `total_count` - how many total items there may be (so the full list size, maybe thousands).

* `offset` - the number of documents into the full list that this particular response is starting at, this should default to `0` if not set. 
    * For example, in a list that has a total_count of 511, we might set a limit of 100, an offset of 500, and get a response whose count is 11, because it's the last 11 documents in the list.*
	  
* `items` - array containing results. 
    * Should only return items which match the offset and limit criteria, e.g. using the example above, you would expect the items array to only contain 11 documents.
	  
When pagination is required, it is also required the data be in a sorted order before it can be paginated. We should always configure defaults to help protect the service from performance problems due to allowing large limit and offset query values being set: `DEFAULT_MAXIMUM_LIMIT`, `DEFAULT_MAXIMUM_OFFSET`

* `DEFAULT_MAXIMUM_LIMIT` - Environment variable to cap the number of items to be returned.
	  * Should be set in the region of 500 to 1000 items. It is good practice to return a few results at a time, so requests don’t tie up resources for too long by trying to get all the requested data at once.
	  * Should return 400 (bad request) status code and an error explaining the maximum limit on limit value and providing the maximum value.

* `DEFAULT_MAXIMUM_OFFSET` - **Optional** environment variable to cap how far one can access a list of items.
	  * This is optional and is dependent on the underlying database. *Example an API relying on Elasticsearch will need a maximum offset value see why in the [example below](#elasticsearch-example-of-performance-issues-using-large-offsets).*
	  * Should return 400 (bad request) status code and an error explaining the maximum limit on offset value and providing the maximum value.