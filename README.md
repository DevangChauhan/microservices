# EasyBank Microservices

This project is a Maven multi-module microservices application for EasyBank, featuring various services for managing accounts, loans, cards, and more.

## Project Structure

The project is organized as a multi-module Maven project with a centralized BOM (Bill of Materials) for dependency management.

- **`microservices-parent` (Root)**: The aggregator and parent POM for all modules.
- **`easybank_bom`**: Contains the Bill of Materials and build requirements.
- **`accounts`**: Microservice for managing customer accounts.
- **`loans`**: Microservice for managing loans.
- **`cards`**: Microservice for managing cards.
- **`customer`**: Microservice for managing customer details.
- **`gatewayserver`**: API Gateway for routing requests.
- **`configserver`**: Centralized configuration management using Spring Cloud Config.
- **`eurekaserver`**: Service discovery using Netflix Eureka.
- **`message`**: Messaging service for handling notifications.

## Prerequisites

- **Java 21** or later
- **Maven 3.9** or later
- **Docker** (for containerization)

## Build and Compilation

### Full Project Build
To build the entire project and install all modules to the local repository (skipping tests):
```bash
mvn clean install -DskipTests
```

### Individual Module Compilation
To compile a specific module from the root directory:
```bash
mvn compile -pl <module-name>
```
Example: `mvn compile -pl accounts`

## Running the Application

### Using Maven Profiles (Recommended)
Specific profiles are configured in the root `pom.xml` for each service:

| Service | Run Command |
| :--- | :--- |
| Accounts | `mvn spring-boot:run -P run-accounts` |
| Loans | `mvn spring-boot:run -P run-loans` |
| Cards | `mvn spring-boot:run -P run-cards` |
| Message | `mvn spring-boot:run -P run-messages` |
| Customer | `mvn spring-boot:run -P run-customers` |
| Gateway Server | `mvn spring-boot:run -P run-gatewayserver` |
| Config Server | `mvn spring-boot:run -P run-configserver` |
| Eureka Server | `mvn spring-boot:run -P run-eurekaserver` |

### Using Project List flag
Alternatively, you can run a module using the `-pl` flag:
```bash
mvn spring-boot:run -pl <module-name>
```

## Containerization

### Google Jib (Recommended)
Build Docker images without a Dockerfile using Google Jib:
```bash
mvn compile jib:dockerBuild -pl <module-name>
```

### Spring Boot Buildpacks
```bash
mvn spring-boot:build-image -pl <module-name>
```

## Continuous Integration

A GitHub Actions CI pipeline is configured to automatically build the project whenever a commit is pushed to the `main` or `master` branches. This includes changes to any of the microservice source files, the parent POM, or when submodule references are updated in the parent repository.

- **Workflow File**: `.github/workflows/ci.yml`
- **Triggers**:
  - Push to `main` or `master` branches.
  - Path filters include all microservice source files (`**/src/**`), `pom.xml` files, and `.gitmodules`.
- **Key Features**:
  - **Recursive Submodule Checkout**: Ensures all dependent microservices are available for the build.
  - **Concurrency Control**: Automatically cancels older runs if a new push is made to the same branch.
  - **Optimized Maven Execution**: Uses batch mode and suppressed progress logs for cleaner CI output.
  - **Artifact Archiving**: Build logs are uploaded as artifacts for troubleshooting.
- **Actions**:
  - Sets up Java 21 environment.
  - Builds all modules using `mvn clean install -DskipTests`.

## Useful Maven Commands

| Goal | Command | Description |
| :--- | :--- | :--- |
| **Dependency Tree** | `mvn dependency:tree -pl <module>` | Visualize dependency hierarchy and resolve conflicts. |
| **Effective POM** | `mvn help:effective-pom -pl <module>` | View the final merged POM after inheritance and interpolation. |
| **Check Updates** | `mvn versions:display-dependency-updates` | Check for newer versions of dependencies in the project. |
| **Specific Test** | `mvn test -Dtest=<TestClassName>` | Run a single test class across the project. |
| **Module Tests** | `mvn test -pl <module>` | Run tests only for a specific module. |
| **Force Update** | `mvn clean install -U` | Force update of snapshots and releases from remote repositories. |
| **Verify Project** | `mvn verify` | Run all checks (tests, ITs, etc.) and verify project integrity. |

## Important Links
- Spring Boot - https://spring.io/projects/spring-boot
- Create SpringBoot project - https://start.spring.io
- DTO pattern blog - https://martinfowler.com/eaaCatalog/dataTransferObject.html
- Model Mapper - http://modelmapper.org/
- Map Struct - https://mapstruct.org/
- Spring Doc - https://springdoc.org/
- Open API - https://www.openapis.org/
- Lucidchart Blog - https://www.lucidchart.com/blog/ddd-event-storming
- Docker website - https://www.docker.com
- Docker hub website - https://hub.docker.com
- Buildpacks website - https://buildpacks.io
- Google Jib website - https://github.com/GoogleContainerTools/jib
- Docker compose website - https://docs.docker.com/compose/
- Twelve-Factor methodology - https://12factor.net
- Beyond the Twelve-Factor App book - https://www.oreilly.com/library/view/beyond-the-twelve-factor/9781492042631/
- Spring Cloud website - https://spring.io/projects/spring-cloud
- Spring Cloud Config website - https://spring.io/projects/spring-cloud-config
- Spring Cloud Bus website - https://spring.io/projects/spring-cloud-bus
- RabbitMQ website - https://www.rabbitmq.com
- Hookdeck website- https://hookdeck.com
- Spring Cloud Netflix website - https://spring.io/projects/spring-cloud-netflix
- Spring Cloud OpenFeign - https://spring.io/projects/spring-cloud-openfeign
- Netflix Blog - https://netflixtechblog.com/netflix-oss-and-spring-boot-coming-full-circle-4855947713a0
- Resilience4j website - https://resilience4j.readme.io
- Spring Cloud Gateway website - https://spring.io/projects/spring-cloud-gateway
- Stripe RateLimitter pattern blog - https://stripe.com/blog/rate-limiters
- Apache Benchmark website - https://httpd.apache.org
- Grafana website - https://grafana.com
- Grafana Loki setup - https://grafana.com/docs/loki/latest/getting-started/
- Micrometer website - https://micrometer.io
- Prometheus website - https://prometheus.io/
- Grafana Dashboards - https://grafana.com/grafana/dashboards/
- OpenTelemetry website - https://opentelemetry.io/
- OpenTelemetry automatic instrumentation - https://opentelemetry.io/docs/instrumentation/java/automatic/
- Keycloak website - https://www.keycloak.org/
- Apache Kafka website - https://kafka.apache.org
- Docker compose file for Kafka - https://github.com/bitnami/containers/blob/main/bitnami/kafka/docker-compose.yml
- Local Kubernetes Cluster with Docker Desktop - https://docs.docker.com/desktop/kubernetes/
- Kubernetes Dashboard - https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/
- Helm website - https://helm.sh
- Chocolatey website - https://chocolatey.org/
- Bitnami Helm charts GitHub repo - https://github.com/bitnami/charts
- Spring Cloud Kubernetes website - https://spring.io/projects/spring-cloud-kubernetes
- Spring Cloud Kubernetes Blog - https://spring.io/blog/2021/10/26/new-features-for-spring-cloud-kubernetes-in-spring-cloud-2021-0-0-m3
- GCP website - https://cloud.google.com
- GCP SDK installation - https://cloud.google.com/sdk/docs/install
- Kubernetes Ingress - https://kubernetes.io/docs/concepts/services-networking/ingress/
- Ingress Controllers - https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/
- Istio (Service mesh) - https://istio.io

## Apache Benchmark commands for reference

|     Apache Benchmark command      |     Description          |
| ------------- | ------------- |
| `ab -n 10 -c 2 -v 3 http://localhost:8072/eazybank/cards/api/contact-info` | To perform load testing on API by sending 10 requests |
