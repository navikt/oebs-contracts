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

### Generating a client from the OpenAPI spec

Instead of writing HTTP client code manually, you can generate a typed client using [openapi-generator](https://openapi-generator.tech/docs/generators),
se the documentation for available generators. The spec is resolved directly from the `oebs-contracts` JAR. 

#### Using the Maven plugin

Add the plugin to your `pom.xml`

```xml
<plugin>
    <groupId>org.openapitools</groupId>
    <artifactId>openapi-generator-maven-plugin</artifactId>
    <version>latest-version</version>
    <executions>
        <execution>
            <goals>
                <goal>generate</goal>
            </goals>
            <configuration>
                <inputSpec>classpath:static/openapi/okonomimodell/openapi.yaml</inputSpec>
                <!-- See https://openapi-generator.tech/docs/generators for available generators -->
                <generatorName>your-generator</generatorName>
                <!-- Replace with your own package names -->
                <apiPackage>your.package.name.api</apiPackage>
                <modelPackage>your.package.name.model</modelPackage>
                <generateApiTests>false</generateApiTests>
                <generateModelTests>false</generateModelTests>
            </configuration>
        </execution>
    </executions>
    <dependencies>
        <dependency>
            <groupId>no.nav.oebs</groupId>
            <artifactId>oebs-contracts</artifactId>
            <version>1.0-SNAPSHOT</version>
        </dependency>
    </dependencies>
</plugin>
```

Client classes are generated under `target/generated-sources/openapi` during `mvn compile`.

> **Auth:** All endpoints require a Bearer token. Contact the OEBS team to confirm the correct token mechanism for your use case.
