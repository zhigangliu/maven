```
mvn clean
mvn compile
mvn test
mvn package
mvn install -DskiptTests=true
mvn install -DskipTests
mvn -P <active-profiles>
mvn --activate-profiles <active-profiles>
mvn -B install
mvn help:effective-pom
mvn help:effective-settings
mvn dependency:analyze
mvn dependency:tree
mvn dependency:tree -Dverbose -Dincludes=junit
mvn exec:java -Dexec.mainClass=codetest.Main -Dexec.args="mbp vga"
mvn eclipse:eclipse
mvn install:install-file -Dfile=non-maven-proj.jar -DgroupId=some.group -DartifactId=non-maven-proj -Dversion=1 -Dpackaging=jar
```

* compiler java version (old way)
```
<project>
  <build>
    <plugins>
      <plugin>
        <artifactId>maven-compiler-plugin</artifactId>
        <configuration>
          <source>1.8</source>
          <target>1.8</target>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

* compiler java version (new way)
```
<project>
  <properties>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>
</project>
```