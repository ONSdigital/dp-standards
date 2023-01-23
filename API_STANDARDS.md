API standards
=============

## Core Principles

### Formats
We use HTTP APIs to represent our data in machine-readable, predictable ways.

User research shows that our API users are still most comfortable with RESTful APIs, so they are our recommended primary offering, but other API formats such as SPARQL and GraphQL are acceptable additional options or for internal only APIs where relevant.

### RESTful
Our primary public APIs follow [RESTful principles](https://restfulapi.net/) which are worth understanding more fully but highlights we're particularly focussed on are:
- Endpoints must return JSON responses and correct/meaningful HTTP status codes
- Endpoints must use appropriate requests methods (GET/PUT/POST etc). Changes must not be made via GET requests.
- Concrete path elements must be pluralised e.g. datasets not dataset in /datasets/<id>
- Endpoints must be documented using the Swagger/OpenAPI standard
- Updates to data must be idempotent

More details of precise behaviour we expect including guidance on field names, timestamps, pagination and responses are [given in our structure guide](api-standards/structure.md).

### Auditing
All API requests to access unpublished content must be tracked for auditing purposes, for this reason we recommend routing traffic through custom router services or API Gateways with relevant middleware/add-ons.

This allows us to satisfy several internal security and operational procedures, as well as supporting our partnership with UK Statsitics Authority with any breach investigations as needed.

Specifics on how this is achieved for api.ons.gov.uk can be found in our [ONS API Implementation](api-standards/ons-api.md) guidance. This is an important guide to read before developing any APIs on this domain.


#### TODO

* Consider versioning / base path
* Consider licensing
* Resources (or rather, database items) should contain a `last_updated` field, which might not be exposed via the public interface
