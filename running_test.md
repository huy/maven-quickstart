# Running test

There are in general 2 types of test 

* unit test and 
* integration test. 

## unit test

Unit tests are executed as default by maven surefire plugin. The `default` means that whenever we `pom.xml` it inherit the maven default pom, which has already binding test phase to maven surefire plugin test goal. We can confirm it by creating this bare `pom.xml`

    $ cat pom.xml
    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
      <modelVersion>4.0.0</modelVersion>
      <groupId>com.acme</groupId>
      <artifactId>sample</artifactId>
      <packaging>jar</packaging>
      <version>1.0-SNAPSHOT</version>
      <name>sample</name>
    </project>
    
then look at effective pom

    $bash-3.2$ mvn help:effective-pom  | grep -A 10 -B 1 surefire
    [MVNVM] Using maven: 3.2.5
      <plugin>
        <artifactId>maven-surefire-plugin</artifactId>
        <version>2.12.4</version>
        <executions>
          <execution>
            <id>default-test</id>
            <phase>test</phase>
            <goals>
              <goal>test</goal>
            </goals>
          </execution>
        </executions>
    
The surefire plugin by default runs all test classes with the following wildcard patterns
By default, the Surefire Plugin will automatically include all test classes with the following wildcard patterns
`**/Test*.java`, `**/*Test.java`, `**/*TestCase.java`. This can be changed as described [here](https://maven.apache.org/surefire/maven-surefire-plugin/examples/inclusion-exclusion.html)

## Integration test

Integration tests are usually executed by maven failsafe plugin. This plugin needs to be explicitly added in to our `pom.xml` as 

        <plugins>
          <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-failsafe-plugin</artifactId>
          </plugin>
        </plugins>        

The plugin provides the following goals

    $mvn help:describe -Dplugin=org.apache.maven.plugins:maven-failsafe-plugin
    Name: Maven Failsafe Plugin
    Description: Surefire is a test framework project.
    Group Id: org.apache.maven.plugins
    Artifact Id: maven-failsafe-plugin
    Version: 2.18.1
    Goal Prefix: failsafe

    This plugin has 3 goals:

    failsafe:help
      Description: Display help information on maven-failsafe-plugin.
      Call mvn failsafe:help -Ddetail=true -Dgoal=<goal-name> to display
      parameter details.

    failsafe:integration-test
      Description: Run integration tests using Surefire.

    failsafe:verify
      Description: Verify integration tests ran using Surefire.

The test classes to be executed are those of the following wildcard patterns `**/IT*.java`, `**/*IT.java`, `**/*ITCase.java`. Inclusion/exclusion is possible via a instruction [here](https://maven.apache.org/surefire/maven-failsafe-plugin/examples/inclusion-exclusion.html)

References

* https://maven.apache.org/surefire/maven-surefire-plugin/
* https://maven.apache.org/surefire/maven-failsafe-plugin/
