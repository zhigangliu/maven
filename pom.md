# Setup
```
<installation folder>/conf/settings.xml
<home directory>/.m2/conf/settings.xml
<home directory>/.m2/repository
```

* Standard directory layout
```
src/main/java
src/main/resources
src/main/webapp
src/test/java
src/test/resources
```


# Super POM
* parent of all POM, contains
  * central remote repository for dependencies and plugins, which can be overridden by settings.xml
  * default values for directories in the Maven standard directory layout
    * src/main/java
    * src/main/resources
    * src/test/java
    * src/test/resources
    * target/classes
    * target/test-classes
  * default package name: ${project.artifactId}-${project.version}
* standard plugins

# Effective POM
```
mvn help:effective-pom
```

# Project Version
```
<major version>.<minor version>.<incremental version>-<qualifier>
```
qualifier could be alpha, beta, etc

SNAPSHOT is used for projects under active development

SNAPSHOT will not be checked in remote repository, unless explicitly enabled in `repository` or `pluginRepository`
```
<snapshots>
  <enabled>true</enabled>
</snapshots>
```

# Predefined properties
* shell environments --- ${env.PATH}
* POM project --- ${project.groupId}, ${project.artifactId}
* settings.xml --- ${settings.offline}
* java System properties --- ${user.name}, ${user.home}, ${java.home}, and ${os.name}

# Defining properties
```
<maven.compiler.source>1.8</maven.compiler.source>
<maven.compiler.target>1.8</maven.compiler.target>
```

# Dependency scope
* compile (by default)

  used in all classpaths and will be packaged
* provided

  should be supplied by container, and used in compile, but not package
* test

  used in test compilation and test execution
* runtime

  used in execution and test execution, but not compile
* system

  similar to provided, but can't be found in central repository and has to supplied in `systemPath`

# Conflict resolution
* nearest wins (in terms of dependency tree level)
* first wins (if they are on the same level)
* resolving conflicts using the dependency tree
```
mvn dependency:tree -Dverbose -Dincludes=commons-collections
```

* excluding a transitive dependency
```
<dependencies>
  <dependency>
    <groupId>org.sonatype.mavenbook</groupId>
    <artifactId>project-a</artifactId>
    <version>1.0</version>
    <exclusions>
      <exclusion>
        <groupId>org.sonatype.mavenbook</groupId>
        <artifactId>project-b</artifactId>
      </exclusion>
    </exclusions>
  </dependency>
</dependencies>
```

* excluding and replacing a transitive dependency
```
<dependencies>
  <dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate</artifactId>
    <version>3.2.5.ga</version>
    <exclusions>
      <exclusion>
        <groupId>javax.transaction</groupId>
        <artifactId>jta</artifactId>
      </exclusion>
    </exclusions>
  </dependency>
  <dependency>
    <groupId>org.apache.geronimo.specs</groupId>
    <artifactId>geronimo-jta_1.1_spec</artifactId>
    <version>1.1</version>
  </dependency>
</dependencies>
```