Registering Health Checkers
===========================

To register a health checker for an application health endpoint/route, please see [healthcheck specification doc](./HEALTH_CHECK_SPECIFICATION.md) and for implementation of code, see the [dp-healthcheck library](https://github.com/ONSdigital/dp-healthcheck#dp-healthcheck).

### Which checkers should I be registering?

Before answering this question remember the main function of the health check is to enable an app to signal to the platform whether or not it is functional. To extend on this slightly, if the app is partially functioning then consideration is needed to understand if the platform needs to know this as the platform will end up taking down the app, resulting in the loss of all functionality.

#### Frontend and API Router

Both of these applications proxy requests to various frontend web apps or REST APIs. If these two applications were to register health checkers for every application that it proxies request to, and 1 application fails then the knock on effect is that the routers themselves fail and all functionality is lost. This means the website, publishing services and/or the API service will be unavailable.

##### So what health checkers should we be registering in these two applications, which are crucial in our services running seamlessly?

The only checkers that should be registered are those that affect the routers ability to proxy requests. 

Example, auditting of every http requests takes place in the API router on publishing subnet: 

The API router uses kafka a distributed event streaming technology to send events of the http requests being made to a kafka topic (queue) so another service can then consume this information for audit purposes. 

If Kafka became unavailable or the connection to kafka was lost then the API router would have to cease to function and start returning 500 internal server error messages, "as we can't have requests being made to our API applications if the requests are not auditted". So for kafka we would register a health checker to check that the connection to kafka is open.

#### Frontend Applications

<TODO>

#### Backend Applications

##### APIs

<TODO>

##### Event Driven Apps

<TODO>
