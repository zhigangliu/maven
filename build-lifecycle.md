# Build Life cycle
* run with plugin name and goal
```
mvn help:effective-pom
mvn compile:compile
```

* run with phase
```
mvn install
```

* plugin goals are bound to phase

  executing a phase will first execute all proceeding phases
in order, ending with the phase specified on the command line
```
mvn install
```
equals to
```
mvn resources:resources \
compiler:compile \
resources:testResources \
compiler:testCompile \
surefire:test \
jar:jar
```