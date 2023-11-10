API standards
=============

## Core Principles

### Formats
We use HTTP APIs to represent our data in machine-readable, predictable ways.

User research shows that our API users are still most comfortable with RESTful JSON APIs, so they are our recommended primary offering, but other API formats such as SPARQL and GraphQL are acceptable additional options or for internal only APIs where relevant. This approach is consistent with the [Gov.uk: API Technical and Data Standards](https://www.gov.uk/guidance/gds-api-technical-and-data-standards) recommendation.

### RESTful
Our primary public APIs follow [RESTful principles](https://restfulapi.net/) which are worth understanding more fully but highlights we're particularly focussed on are:
- Endpoints must return JSON responses and correct/meaningful HTTP status codes
- Endpoints must use appropriate requests methods (GET/PUT/PATCH/POST etc). Changes must not be made via GET requests.
- Concrete path elements must be pluralised e.g. datasets not dataset in /datasets/<id>
- Endpoints must be documented using the Swagger/OpenAPI standard
- Updates to data must be idempotent

As a further specification to our RESTful approach, we use the [HAL (Hypermedia Application Language)](https://stateless.group/hal_specification.html) to meet the [HATEOAS (Hypermedia as the engine of application state)](https://en.wikipedia.org/wiki/HATEOAS) constraint for REST. This means we use `_links` and `_embedded` fields to facilitate navigation across the API space. 

More details of our HAL implementation, as well as precise behaviour we expect including guidance on field names, timestamps, pagination and responses are [given in our structure guide](api-standards/structure.md).

### Linked Data
While we use RESTful architecture to structure our responses, the content of those responses is intended to adhere to a number of Linked Data principles to help users programatically understand our data and be able to operate with it.

We use [JSON-LD](https://json-ld.org/) as a means of structuring and describing data available via the API. This is evident in the `@context` field in many of our JSON responses, as well as the use of `@id` for a URL of the resource being represented. More details on how we manage vocabularies and our approach to JSON-LD are [given in our implementation document](api-standards/ons-api.md#application-profile)

Our Linked Data ambitions also lead us towards better use of [Content Negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation) to access different "distributions" of the same "resource". This means that for a URI like `/datasets/cpih01` the user may have options between an HTML, JSON or CSV response and they would indicate their preference via headers on their request. In this example the CPIH dataset is the resource, but HTML, JSON and CSV are all distributions of it. 

### Auditing
All API requests to access unpublished content must be tracked for auditing purposes, for this reason we recommend routing traffic through custom router services or API Gateways with relevant middleware/add-ons.

This allows us to satisfy several internal security and operational procedures, as well as supporting our partnership with UK Statsitics Authority with any breach investigations as needed.

Specifics on how this is achieved for api.ons.gov.uk can be found in our [ONS API Implementation](api-standards/ons-api.md) guidance. This is an important guide to read before developing any APIs on this domain.


#### TODO

* etags and If-Match headers
* Options requests
* Consider versioning / base path
* Consider licensing
* Resources (or rather, database items) should contain a `last_updated` field, which might not be exposed via the public interface
