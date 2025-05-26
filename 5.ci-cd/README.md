# CI/CD Process

### If the pipeline in some of the steps, the process will be interrupted.

- Event trigger: Code is merged in the main branch, so the CI/CD starts.
- Clone code into CI/CD server and install production dependencies.
- Run ESLint to check code formatting and syntax errors.
- Run TSC to check possible type errors and build the code.
- Run unit tests, integrated tests with mocks using Jest. Ensure a 80% code coverage.
- Run load tests using K6 to ensure a p95 <= 500ms with no lost requests.
- Build the Docker image.
- Push the image to a private container registry (like Google Cloud Artifact Registry).
- Apply the Kubernetes Manifest files with `kubectl apply -f filename`.
- Pull the new image from the registry
- Verify if everything is OK with the new image and ensure the old pods are ready to be swapped for the new ones.