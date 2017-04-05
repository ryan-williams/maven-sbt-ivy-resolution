# maven-sbt-ivy-resolution
Example of differing ivy resolution between Maven and SBT

Maven resolves Guava 11.0.2 based on [the "nearest-wins" heuristic](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html#Transitive_Dependencies):

```bash
$ mvn dependency:tree -Dincludes=":guava:"
…
[INFO] org.foo:bar:jar:1.0-SNAPSHOT
[INFO] \- com.google.guava:guava:jar:11.0.2:compile
…
```

SBT resolves 19.0 based on [the "latest wins" heuristic](http://www.scala-sbt.org/0.13/docs/Library-Management.html#Conflict+Management):

```bash
$ sbt 'show dependencyClasspath' | grep guava
[info] * Attributed(/Users/ryan/.ivy2/cache/com.google.guava/guava/bundles/guava-19.0.jar)
```

Thanks to [**@jodersky**](https://github.com/jodersky) and [**@eed3si9n**](https://github.com/eed3si9n) for helpful discussion and links on the topic:
- [sbt/sbt#2291](https://github.com/sbt/sbt/issues/2291#issuecomment-270495227)
- [Maven dependency resolution](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html)
- [SBT conflict managers](http://www.scala-sbt.org/0.13/docs/Library-Management.html#Conflict+Management)
