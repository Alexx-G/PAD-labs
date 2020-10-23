# Web-proxy - transparently distributed HTTP services

## Prerequisites

- HTTP;
- RESTful APIs / GraphQL;
- Data representation and serialization/de-serialization;

## Objectives

- Implement a service (or several services) that expose an API over HTTP;
- Implement a "smart-proxy" service that acts API gateway, overriding caching and load balancing;

## Background

In the wild a distributed system is just a collection of services that either communicate with each other or are exposed to the end customer.
Thus, in order to ensure that the system stays robust it's important to:
- define strong contracts/APIs between services (including internal services);
- expose consistent public APIs;
- ensure transparent public API, especially when multiple services are behind it;

This is what this lab is going to focus on:
- implementing an API-driven distributed system;
- expose public APIs transparently using a proxy;

## Tasks

- [**Mandatory** - Implement a single horizontally scalable service](#mandatory---implement-a-single-horizontally-scalable-service)
- [Implement a smart proxy](#implement-an-api-gateway)
- [Implement sharding](#implement-sharding)
- [Implement adapter layer](#implement-adapter-layer)

### Mandatory - Implement a single horizontally scalable service

One of the simplest variations of distributed systems is a service, scaled horizontally, behind a reverse-proxy that transparently distributes traffic across all instances.
This approach implies that either all instances use the same database or there's a mechanism to keep data in sync across all instances.

**Requirements:**
- Implement a web service that exposes a RESTful API over HTTP;
- Use a (R)DBMS to access/store data from that service;
- Scale the service horizontally (run 2+ instances);
- Use a reverse-proxy to load balance traffic across all instances transparently;

**Note:** The maximum grade for this task is 7, depending on implementation and presentation.

### Implement an API Gateway

API Gateway (or smart proxy) is an intermediary component often used to transparently expose public APIs of multiple services.
This approach allows changing the way incoming traffic is handled, without changing services behind the API Gateway, 
also it offers a single, transparent entry point of the system.
Some reasons to use an API Gateway / smart-proxy
- load balancing (including non-trivial algorithms);
- caching;
- API access layer (throttling, authorization/authentication etc);
- adapter layer (e.g. to expose an older API in a consistent way with other public APIs);

**Requirements:**
- Implement a "smart proxy" service that transparently redirects requests to internal services;
- Use Redis to cache some responses at proxy level;
- Implement a load balancing algorithm;

**Note:** This task may add up to 2 points to the grade, depending on the implementation.

### Implement sharding

Sharding is the process of logical (or physical) partitioning of the distributed system (or some of its components), depending on some partitioning criteria.
Sharding is often used to fix different side-effects of non-uniform data access patterns:
- noisy neighbors - an example would be a SaaS (Software-as-a-Service) system. A spike in traffic for a single tenant, can affect performance for other tenants, even if their traffic has the same pattern;
- horizontal scalability overhead - scaling the system for a single poorly performing tenant isn't cost-efficient;
- better reliability and tenant isolation;

There are multiple ways of implementing sharding:
- data sharding - allows partitioning data across different databases;
- service sharding - allows partitioning traffic to a specific set of service instances;

Also, there are multiple sharding methods:
- key based sharding (or hash based sharding) - it uses a specific field of the given entity to determine what shard the entity belongs to.
  Usually key based sharding is used with a hash function and its result must be deterministic;
- Range based sharding - in this case a shard handles data from a specific range determined by a field (e.g. products that have price between 1000$ and 20000$ are assigned to the shard C);
- Directory based sharding - it implies keeping a mapping between a specified entity and the shard it belongs to;

**Requirements:**

Choose one of the following options:
- Option 1: Implement data sharding
- Option 2: Implement service sharding

What sharding method is going to be implemented is up to you.

### Implement adapter layer

One of API Gateway/Smart-proxy use cases is being able to offer an API in a different format, without changing services themselves.

**Requirements:**
- Keep API of the service implemented in the first task unchanged;
- Add another entity to your data model that has a relationship with the entity exposed by the first service;
- Add a service that exposes RESTful API for the entity added at previous step;
- Implement a [GraphQL](https://graphql.org/) API at the smart-proxy level that aggregates data from both services;