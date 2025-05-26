# Testing Strategy

## Unit Tests

- **Goal:** Test API components in isolation.
  - **Validation:** Test DTOs to ensure the type, length, format and other validations are being executed correctly.
  - **Use Case:** Test business rules of the use cases, mocking database/cache calls and responses.

## Integrated Tests

- **Data Persistence:** Test repository methods for database, ensuring data is being retrieved and persisted correctly.
- **Use Case**: Test use case business rules without mock database, queue and cache.
- **Tools:**
  - **Test Runner/Framework:** Jest (as specified in the CI/CD process).

## Performance Tests

- **Goal:** Assure microservice speed, endurance, and scalability under high load conditions. This aligns with the CI/CD goal of p95 <= 500ms with no lost requests.
  - **High Load:** Simulate a large number of concurrent users accessing `GET /data` and `POST /data` endpoints.
  - **Identify bottlenecks:** Identify which parts of the system that are slow.
  - **Endurance Tests:** Evaluate the application's stability over a prolonged period of typical load.
- **Metrics to Collect:**
  - Response Time (median, p90, p95, p99).
  - RPS (requests per second).
  - Error Rates.
  - CPU and memory utilization of the service and database/cache.
- **Tools:**
  - **Load Generation:** K6 (as specified in the CI/CD process).