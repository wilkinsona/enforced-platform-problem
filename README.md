### Enforced Platform Problem

Sample project to demonstrate a problem when declaring an `enforcedPlatform`
using a `project` dependency.

The problem can be reproduced by running the following command:

```
$ ./gradlew generatePomFileForMavenPublication
```

The generated pom for the `library` module will be invalid:

```
$ cat library/build/publications/maven/pom-default.xml
<?xml version="1.0" encoding="UTF-8"?>
<project xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd" xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>library</artifactId>
  <version>1.0-SNAPSHOT</version>
  <dependencies>
    <dependency>
      <groupId>com.example</groupId>
      <artifactId>bom</artifactId>
      <version>1.0-SNAPSHOT</version>
      <scope>runtime</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <scope>runtime</scope>
    </dependency>
  </dependencies>
</project>
```

Note that the bom has been declared as a regular dependency and that the
`spring-core` dependency has no version.