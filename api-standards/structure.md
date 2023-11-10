An extension of the [API Standards](../API_STANDARDS.md), with implementation details specific to development of RESTful APIs for ONS.

## RESTful API Structure and Syntax

### Syntax & types

  * Field names snake case, e.g. `total_count`
  * Use appropriate types for fields, e.g. numbers should be numeric types for the language in use and not strings unless necessary
    * A field which always returns whole  numbers is an int or similar
    * A field which always returns numbers and may contain decimal places (15.7) is a float or similar
    * A field which may contain "10500", "10.51" or "X" (such as statistical observations) may be a string
  * Timestamps should be UTC (optionally, with a timezone)
  * Root endpoint IDs should be referred to as `identifier`, rather than name-spaced. All IDs under this level will need descriptive placeholder names. e.g. /datasets/<identifier>/editions/<edition> where /datasets is the root endpoint

### Methods & Behaviours
 * Use the `GET` method for search endpoints
 * `POST` endpoints should typically generate IDs, and these should use GUIDs not auto-incrementing counts

 ### _links
* All endpoints must return a `_links.self` subdoc in their response,
* Resources should avoid a nested list by having a links to list endpoints or using `_embedded`
* Responses must contain fully qualified URLs, though this may be managed by the API router
* `Links` object contains descriptively named objects which each contain
  an `id` (optional) and `url` field e.g.
  ```
  {  
      "id":"1234",
      "data":"i have stuff",
      "_links": {  
          "latest_resource": {  
              "id":"5678",
              "url":"/thisapi/1234/subresources/5678"
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
* Resources may link to their direct parent, a child list, or any critical related resources. 
Resources which are many layers deep in an API do not need to contain links to all higher 
elements but may if that is deemed useful for navigation
* URLs which do not facilitate navigation (such as a link to the `license` document) should not be
in the `_links` subdoc but should instead be top level fields with appropraitely descriptive names

### _embedded
The HAL specification allows for an `_embedded` subdocument to be introduced which contains relevant fields of related resources to minimise on additional requests. 

For our implementation, the intention is this should include as few fields as possible to allow a user to disambiguate between resources of a certain type and navigate to them. e.g. for an embedded list of versions may look like:
```
{
    _embedded: {
        "versions": [
            {
                "@id": api.ons.gov.uk/versions/3
                "published_date": 02/01/2023
                "version_note": "a correction to the Jan 1st publication"
            },
            {
                "@id": api.ons.gov.uk/versions/2
                "published_date": 01/01/2023
                "version_note": "2023 data publication"
            },
            {
                "@id": api.ons.gov.uk/versions/1
                "published_date": 01/01/2022
                "version_note": "2022 data publication"
            }
        ]
    }
}
```
Embedded documents are likely to be lists of resources, and each item in that list must always contain an `@id` field where such field would be present on the complete resource. Although the HAL spec allows for it, we prefer not to include any `_links` field within an `_embedded` resource.

The `_embedded` field should not be included in list responses. E.g. if the model for /datasets/<identifier> includes an `_embedded` field, then it should be omitted from responses at /datasets.


### Returning errors
  * **Errors** should return a status code and a JSON payload with the error message
      * `errors` array containing error messages

## List responses

List endpoints must always use a plural name e.g. `/datasets` rather than `/dataset`

It is not necessary for a list response to contain all possible fields for a resource. The `items` contained in `/datasets` do not need to exactly match the number of fields returned on requesting specific resources at `/datasets/<identifier>` but any field present should be named and typed consistently across both responses.

Items in a list response should not contain `_embedded` fields and need only contain the `_links` that are deemed appropriate for navigation and disambiguation within the list.

### List controls, pagination and search results
Search/list endpoints should contain the following fields: `count`, `limit`, `offset`, `total_count`, `items`

Within the `_links` subdoc for a list response, there should only be `self`, `next`, and `prev` based on the specified page size from the `limit` query param.

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