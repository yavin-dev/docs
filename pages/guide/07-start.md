---
layout: guide
group: guide
title: Programmatic API
---

Yavin leverages [elide](https://elide.io) for its semantic layer and also its programmatic API.  Elide supports two API standards:

1. [JSON-API](https://jsonapi.org/) - JSON-API is a REST API standard that makes it simple to construct queries in the browser URL or with curl.  
2. [GraphQL](https://graphql.org/) - GraphQL is a more feature rich API that must be embedded in a POST body.  

Both API formats support the following features:

1. Rich filter support for measures and dimensions including complex predicates, logical conjunction (and), and logical disjunction (or).
2. Sorting by both measures and dimensions.
3. Pagination of results - including fetching the total size of the unpaginated result.
4. Schema introspection tools ([Swagger](https://swagger.io/tools/swagger-ui/) for JSON-API and [Graphiql](https://github.com/graphql/graphiql) for GraphQL).
5. Synchronous and Asynchronous query support.

## API Documentation

API Documentation is broken out by topic:

1. **Analytic Queries** - Example analytic queries can be found [here](https://elide.io/pages/guide/v5/04-analytics.html#analytic-queries).
2. **Metadata Queries** - All of Yavin's semantic model can be accessed programmatically.  Details can be found [here](https://elide.io/pages/guide/v5/04-analytics.html#metadata-queries).
3. **JSON-API Documentation** - The [JSON-API standard](https://jsonapi.org/) is a good place to start to understand the specification.  Elide has further documentation [here](https://elide.io/pages/guide/v5/10-jsonapi.html).
4. **GraphQL Documentation** - The [GraphQL Specification](https://graphql.org/) provides an overview of querying with GraphQL.  Elide exposes opinionated GraphQL APIs documented [here](https://elide.io/pages/guide/v5/11-graphql.html).
5. **Asynchronous Queries** - Queries that take longer than a minute should ideally be run asynchronously leveraging [Elide's asynchronous API support](https://elide.io/pages/guide/v5/11.5-asyncapi.html).

## Schema Introspection

The Yavin service includes a [landing page](http://localhost:8080/api/index.html) where you can browse the API documentation and run queries using either Swagger (JSON-API) or Graphiql (GraphQL). 

### Swagger 
![](/assets/images/API_Swagger.png)

### Graphiql 
![](/assets/images/API_Graphiql.png)
