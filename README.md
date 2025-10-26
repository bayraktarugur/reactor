# Reactor (Maven multi-module parent)

This repository is configured as a Maven Reactor (multi-module) project so you can load and build multiple modules from a single parent.

## How to add modules
1. Create a directory per module at the repository root (same level as this README and the parent pom.xml), for example:
   - `module-a`
   - `module-b`
2. Inside each module directory, create its own `pom.xml` and set this project as the parent:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <parent>
        <groupId>com.example</groupId>
        <artifactId>reactor-parent</artifactId>
        <version>1.0.0-SNAPSHOT</version>
        <relativePath>..</relativePath>
    </parent>

    <artifactId>module-a</artifactId>
    <version>1.0.0-SNAPSHOT</version>

    <dependencies>
        <!-- Add module dependencies here -->
    </dependencies>
</project>
```

3. Register each module in the root `pom.xml`:

```xml
<modules>
    <module>module-a</module>
    <module>module-b</module>
</modules>
```

4. Import the root `pom.xml` into IntelliJ IDEA (or re-import if already opened). IDEA will automatically detect and load all listed modules.

## Build all modules
- From the root folder, run:

```
mvn -q -DskipTests clean install
```

This builds all listed modules in the correct order.

## Notes
- Java version is controlled via `maven.compiler.release` in the parent POM (currently `17`).
- Manage plugin versions and common dependency versions in the parent POM to keep module POMs small and consistent.
