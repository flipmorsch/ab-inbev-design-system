# Microservice Design

### I chose to use `NestJS` with `Fastify` due to `NodeJS` non-blocking IO nature, `NestJS` builtin tools, like `class-validator` and the capacity of Fastify of dealing with a high number of requests.

#### *POST* /data

- The request payload will be treated by the NestJS validator pipe, if all the fields validated follow the rules, the request will be forwarded to the controller, if not, an exception will be raised.
- The controller will call the use case.
- The use case verifies if the data already exists on the database, if yes, an exception will be thrown, if no, we can proceed.
- The use case will call a queue system (to ensure the data will be persisted, even over high load)
- The queue will try to persist the data on the database, if it fails, the data will be inserted in retry queue, until be inserted in DLQ (dead letter queue). In case of success, the data will be persisted in the database and in the caching system (with a TTL, depending of the case).

#### *GET* /data

- The request payload will be treated by the NestJS validator pipe, if all the fields validated follow the rules, the request will be forwarded to the controller, if not, an exception will be raised.
- The controller will call the use case.
- The use case will try to find the data in the cache, if it is found, return to the user, if not, find for it in the database.
- If found, return to the user, otherwise, return a not found exception.

### PS:

- Database in configured to work with sharding in horizontal scaling.
- Caching layer is a cluster.