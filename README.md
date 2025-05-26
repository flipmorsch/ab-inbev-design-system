# AB-Inbev System design

### System design of a microservice that needs to deal with high user concurrency.

#### Every part of the design is in it's own folder

#### Goals
- Ensure API read/write operations respond within 500ms.
- Support scalability to millions or billions of records with no more than a 10% degradation in performance.
- Support unique user high scalability

### How to run

- Docker and Docker Compose have to be installed on your system
- Create a `.env` file with the needed environment variables

Run `docker compose -f 3.containerization/docker-compose.yml up --build`