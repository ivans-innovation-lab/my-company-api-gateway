# my-company-api-gateway-backingservice [![CircleCI](https://circleci.com/gh/ivans-innovation-lab/my-company-api-gateway-backingservice.svg?style=svg)](https://circleci.com/gh/ivans-innovation-lab/my-company-api-gateway-backingservice)

Implementation of an API gateway that is the single entry point for all clients. The API gateway handles requests by simply proxying/routing them to the appropriate service. 

```
zuul:
  routes:
    my-company-blog-domain-microservice:
      path: /command/blog/**
    my-company-blog-materialized-view-microservice:
      path: /query/blog/**
    my-company-project-domain-microservice:
      path: /command/project/**
    my-company-project-materialized-view-microservice:
      path: /query/project/**

```

## Running instructions

Make sure that services are running:

 - [my-company-configuration-backingservice](https://github.com/ivans-innovation-lab/my-company-configuration-backingservice)
 - [my-company-registry-backingservice](https://github.com/ivans-innovation-lab/my-company-registry-backingservice)
 

```bash
$ cd my-company-api-gateway-backingservice
$ ./mvnw spring-boot:run
```

Application will be available on port 9000 (http://localhost:9000)

## Explore

### curl

```
$ curl -H "Content-Type: application/json" -X POST -d '{"title":"xyz","rawContent":"xyz","publicSlug": "publicslug","draft": true,"broadcast": true,"category": "ENGINEERING", "publishAt": "2038-12-23T14:30:00+00:00"}' http://127.0.0.1:9000/command/blog/blogpostcommands
```
```
$ curl http://127.0.0.1:9000/query/blog/blogposts
```
```
$ curl -H "Content-Type: application/json" -X POST -d '{"name":"Name","repoUrl":"URL","siteUrl": "siteUrl","description": "sdfsdfsdf"}' http://127.0.0.1:9000/command/project/projectcommands
```
```
$ curl http://127.0.0.1:9000/query/project/projects
```

### WebSocket on the gateway

All the events will be sent to browser via WebSocket and displayed on http://127.0.0.1:9000/socket/index.html


### rambittmq

Open RabbitMQ management web console at http://localhost:15672/ and explore exchanges, queues and messages.

### registry backing service

Open Registry (Eureka) web console at http://localhost:8761/ and find 'my-company-api-gateway-backingservice' registered.
