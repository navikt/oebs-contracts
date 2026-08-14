# oebs-contracts

Shared contracts for the OEBS domain — Avro schemas for Kafka topics and OpenAPI specifications.

## Repository structure

```
oebs-contracts/
├── src/
│   └── main/
│       ├── avro/
│       │   └── no/nav/oebs/ordre/
│       │       ├── Ordre.avsc          # Avro schema for the Ordre Kafka topic
│       │       └── OrdreType.avsc
│       └── resources/
│           └── static/
│               └── openapi/
│                   └── okonomimodell/
│                       └── openapi.yaml  # OpenAPI spec, served as static resource
├── pom.xml                               # Builds and publishes JAR to GitHub Packages
└── .github/
    └── workflows/
        └── publish.yml                   # Publishes on push to main
```

## How to consume

### 1. Add the GitHub Packages repository to your `pom.xml`

```xml
<repositories>
    <repository>
        <id>github</id>
        <name>GitHub Packages</name>
        <url>https://maven.pkg.github.com/navikt/oebs-contracts</url>
    </repository>
</repositories>
```

### 2. Add the dependency

```xml
<dependency>
    <groupId>no.nav.oebs</groupId>
    <artifactId>oebs-contracts</artifactId>
    <version>1.0-SNAPSHOT</version>
</dependency>
```

### Avro schemas

The JAR contains generated Java classes from the Avro schemas. Use them directly in your Kafka producers/consumers.

### OpenAPI specifications

The YAML files are included as static resources in the JAR and served automatically by Spring Boot at `/openapi/<service>/openapi.yaml`.

Configure springdoc to use the spec:

```yaml
springdoc:
  swagger-ui:
    url: /openapi/okonomimodell/openapi.yaml
```
