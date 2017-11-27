# Project coordinates
* groupId

  resemble a Java package name, paths in the Maven Repository

  usually separated by `.`
* artifactId

  jar named with artifactId and version

  usually separated by `-`
* version

  `major.minor.incremental-qualifier`
  `major.minor-SNAPSHOT`
* type

  jar, war, pom

  packaging type required to be `pom` for parent and aggregation (multi-module) projects

# Inheritance
  child project inherit everything

  groupId and version can be ignored in child project
```
<project>
  <parent>
    <groupId>com.training.killerapp</groupId>
    <artifactId>parent</artifactId>
    <version>1.0-SNAPSHOT</version>
    <relativePath>../parent/pom.xml</relativePath>
  </parent>
  <artifactId>project-a</artifactId>
    ...
</project>
```

# Grouping dependencies
rather than putting depedencies into a parent project (inheritance disadvantage, only 1 parent, behaviour inherited by all children), using pom dependency

For the project grouping dependencies
```
<project>
  <groupId>org.sonatype.mavenbook</groupId>
  <artifactId>persistence-deps</artifactId>
  <version>1.0</version>
  <packaging>pom</packaging>
  <dependencies>
    <dependency>
      <groupId>org.hibernate</groupId>
      <artifactId>hibernate</artifactId>
      <version>${hibernateVersion}</version>
    </dependency>
  </dependencies>
</project>
```
for the project deriving dependencies
```
<dependencies>
  ...
  <dependency>
    <groupId>org.sonatype.mavenbook</groupId>
    <artifactId>persistence-deps</artifactId>
    <version>1.0</version>
    <type>pom</type>
  </dependency>
</dependencies>
```
this will push those grouped dependencies one level down, so please note `nearest wins`

# Managing versions in central parent POM
```
<project>
	<properties>
		<revision>2.0.0.BUILD-SNAPSHOT</revision>
	</properties>
	<dependencyManagement>
		<dependencies>
			<dependency>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot</artifactId>
				<version>${revision}</version>
			</dependency>
			<dependency>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-test</artifactId>
				<version>${revision}</version>
			</dependency>
			<dependency>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-test-autoconfigure</artifactId>
				<version>${revision}</version>
			</dependency>
    </dependencies>
  </dependencyManagement>
</project>
```

child project would use version defined in parent POM, unless explicitly specified
```
<project>
  <dependencies>
	  <dependency>
		  <groupId>org.springframework.boot</groupId>
		  <artifactId>spring-boot</artifactId>
    </dependency>
  </dependencies>
</project>
```

# Multiple modules
simply telling a project that its build should include the specified modules
```
<project>
...
  <modules>
	  <module>spring-boot-starter</module>
	  <module>spring-boot-starter-activemq</module>
  </modules>
</project>
  ```