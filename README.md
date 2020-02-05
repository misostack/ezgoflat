# EZGO : Structure Your Go Apps

## Sample project : A book review service

- Users can add a new book
- Users can list all books
- Users can review a book
- Users can list all review of a books
- Ability to store data in memory or in a json file or in mongodb
- Ability to create sample data

( Skip update, delete, error handles and testing to simplify the sample )

## Sample Structures

- Flat
- Layered ( Group by function )
- Modular ( Group by module )
- Context
- Domain Drivent Delopment
- Hexagonal Archiecture ( "ports and adapters")

### Flat structure

```md
- data.go
- handlers.go
- main.go
- model.go
- storage.go
- storage_json.go
- storage_mem.go
- storage_mongo.go
```

### Layered

- presentation / user interface
- business logic
- external dependencies / infrastructure

```md
- handlers/
  - books.go
  - reviews.go
- models/
  - books.go
  - reviews.go
  - storage.go
- storage/
  - json.go
  - memory.go
  - mongo.go
- main.go
- data.go
```

### Modular

```md
- books/
  book.go
  handler.go
- database/
  database.go
  data.go
  memory.go
  json.go
- reviews/
  handler.go
  review.go
- main.go
```

### Context

**Context** : an HTTP API for adding book reviews
**Language** : book, review, book repository
**Entities** : HTTP Server
**Service** : Add Book, Add Review, List Books, List Reviews
**Value Objects** : Book, Review
**Possible Events** : Book already exists, Book not found
**Repository** : Book Repository, Review Repository
**Aggregates** : Book adder, Review adder, Book lister, Review lister

### Domain Drivent Delopment (DDD)

- Establish your domain and business logic
- Define your bounded context(s), the models within each context and the uiquitous language
- Categories the building blocks of your system:

Entity
Value Object
Domain Event
Aggregate
Service
Repository
Factory

```md
- adding/
  - endpoint.go
  - service.go
- listing/
  - endpoint.go
  - service.go
- reviewing/
  - review.go
  - service.go
- books/
  - book.go
  - sample_books.go
- reviews/
  - review.go
  - sample_reviews.go
- storage/
  - json.go
  - memory.go
  - type.go
- main.go
```

### Hexagonal Archiecture (DD Hex)

- https://fideloper.com/hexagonal-architecture

- Core domain surrounded by interfaces to external inputs and ouputs
- Dependencies only points forward

![Hexagonal Architecture][img1]
![Hexagonal Architecture][img2]

```md
- cmd/
  - data/
    - main.go
  - server/
    - main.go
- pkg/
  - adding/
  - books/
  - listing/
  - reviewing/
  - reviews/
- storage/
  - json/
  - json.go
  - memory.go
  - type.go
```

### Actors with Gogoroutine

- https://www.slideshare.net/weaveworks/an-actor-model-in-go-65174438
- https://medium.com/@teivah/an-introduction-to-gosiris-an-actor-framework-for-go-e0e3ad15b3c7

## Attachments

[img1]: ./assets/the-hexagonal-architecture.png
[img2]: ./assets/dependencies.png

## Refs

- https://www.brianstorti.com/the-actor-model/
- https://fideloper.com/hexagonal-architecture
- https://en.wikipedia.org/wiki/Domain-driven_design
- https://doc.akka.io/docs/akka/current/typed/guide/actors-intro.html