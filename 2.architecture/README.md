# Architecture

### API Layer

- **entity/controller** - folder with the responsibility of store the request controllers.
- **entity/dto** folder with the responsibility of mapping requests and validating them.

### Service Layer

- **entity/entities** folder with the reponsibility of manage core entities of the microservice, like another layer of validation and transforming data to output or persistence.
- **entity/use-cases** folder with the responsibility of execute business logic and create resources in database, cache, etc.
- **external** folder with the responsibility of integrating with external services (if needed),

### Database Layer:

- **entity/repositories** folder with the responsibility of abstract database calls (like select, update, create, upsert, etc).

#### I chose PostgreSQL as database because of SQL data normalization, relational schema and capabilities of data sharding.