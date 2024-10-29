An extension of the [API Standards](../API_STANDARDS.md), with implementation details specific to development of api.ons.gov.uk based APIs.

## The ONS API (api.ons.gov.uk) Landscape

Our [API training](https://github.com/ONSdigital/dp/blob/main/training/architecture/API.md#api-architecture) lays this out in more detail, but in order to allow each microservice API to focus on managing its data well some behaviour has been abstracted from the API services. This behaviour instead sits at the [API router](https://github.com/ONSdigital/dp-api-router).

Every request coming in on our api.ons.gov.uk domain must pass through our API router, which will perform a number of common checks and then determine which microservice to route traffic through to. When this API router is running internally, these checks include checking for relevant authentication headers and ensuring the request is audited for security reasons.

All API requests must travel through the API router, including app-to-app traffic. This is referred to as 'eating our own dog food' in our [Architecture Standards](ARCHITECTURE_STANDARDS.md). Not only does this ensure that all internal traffic is subject to the same security checks, it serves as quality assurance that our APIs are usable.

We use feature flags to limit what behaviour is available on our public facing API microservices. Typically, only GET endpoints are exposed on public APIs, though user transaction services such as filter and flex data journeys are an exception to this.

To add a new API microservice [follow our guide](https://github.com/ONSdigital/dp/blob/main/guides/NEW_API.md#creating-a-new-api-microservice) to ensure the API router is updated correctly.

---
## Elasticsearch example of performance issues using large offsets

An API accepting large offset values to paginate data returned from elasticsearch will result in slow responses. This is due to data being spread across multiple shards in an Elasticsearch cluster.

The processing in Elasticsearch requires it to sort the data on each shard based on the request (search query) and store the requested hits and hits for previous pages into memory; then accumulate all the information from each shard to work out the actual hits (search document) to return. This gets more resource intensive as one pages deeper and can result in slower responses between the requesing service (API) to Elasticsearch, [to read more on Elasticsearch pagination here](https://www.elastic.co/guide/en/elasticsearch/reference/current/paginate-search-results.html#paginate-search-results).