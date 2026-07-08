# oebs-contracts

Shared contracts for the OEBS domain — Avro schemas for Kafka topics and (later) OpenAPI specifications.

## Repository structure

```
oebs-schemas/
├── src/main/avro/
│   └── no/nav/oebs/ordre/
│       └── Ordre.avsc          # Avro schema for the Ordre Kafka topic
├── openapi/                    # OpenAPI specifications (coming soon)
├── pom.xml                     # Builds and publishes JAR to GitHub Packages
└── .github/
    └── workflows/
        └── publish.yml         # Publishes on push to main
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
