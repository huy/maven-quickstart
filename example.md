## Examples running maven phases

Create project

    $mvn -B archetype:generate -DarchetypeGroupId=org.apache.maven.archetypes -DgroupId=org.interview -DartifactId=coding
    ...
    [INFO] BUILD SUCCESS
    [INFO] ------------------------------------------------------------------------

Add exec plugin to pom.xml

    <build>
      <plugins>
        <plugin>
          <groupId>org.codehaus.mojo</groupId>
          <artifactId>exec-maven-plugin</artifactId>
          <version>1.1</version>
          <configuration>
            <mainClass>com.foo.MainApp</mainClass>
          </configuration>
        </plugin>
      </plugins>
    </build>

Run main class
     
    mvn exec:java
    [INFO] --- exec-maven-plugin:1.1:java (default-cli) @ coding ---
    Hello World!
    [INFO] ------------------------------------------------------------------------
    [INFO] BUILD SUCCESS
    [INFO] ------------------------------------------------------------------------

Clean

    C:\huy\gitrepos\rubyjobbuilder\groovy>mvn clean
    [INFO] Scanning for projects...
    ...
    [INFO] ------------------------------------------------------------------------
    [INFO] BUILD SUCCESS
    [INFO] ------------------------------------------------------------------------

Test

    C:\huy\gitrepos\rubyjobbuilder\groovy>mvn test
    [INFO] Scanning for projects...
    ...
    -------------------------------------------------------
     T E S T S
     -------------------------------------------------------
     Tests run: 20, Failures: 0, Errors: 0, Skipped: 0

Test single class 

     C:\huy\gitrepos\rubyjobbuilder\groovy>mvn -Dtest=AddConsoleScriptTest test
     [INFO] Scanning for projects...
     ...
     -------------------------------------------------------
      T E S T S
      -------------------------------------------------------
      Tests run: 3, Failures: 0, Errors: 0, Skipped: 0

Test single method

      C:\huy\gitrepos\rubyjobbuilder\groovy>mvn -Dtest=AddConsoleScriptTest#testAddWorkerConsoleUrl test
      [INFO] Scanning for projects...
      ...
      -------------------------------------------------------
       T E S T S
       -------------------------------------------------------
       Running com.wonga.techops.jenkins.AddConsoleScriptTest
       Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.727 sec
       Results :
       Tests run: 1, Failures: 0, Errors: 0, Skipped: 0

Compile

       $ mvn compile
        ...
       [INFO] ------------------------------------------------------------------------
       [INFO] BUILD SUCCESS
       [INFO] ------------------------------------------------------------------------

Compile test classes

       $ mvn test-compile
       [INFO] Scanning for projects...
       [INFO]                                                                         
       [INFO] ------------------------------------------------------------------------
       [INFO] Building lca 1.0-SNAPSHOT
       [INFO] ------------------------------------------------------------------------
       [INFO] 

Show dependency tree

      sh-3.1$ mvn dependency:tree -Dverbose
      [INFO] com.example:simple-service:jar:1.0-SNAPSHOT
      [INFO] +- org.glassfish.jersey.containers:jersey-container-grizzly2-http:jar:2.16:compile
      [INFO] |  +- org.glassfish.hk2.external:javax.inject:jar:2.4.0-b09:compile
      [INFO] |  +- org.glassfish.grizzly:grizzly-http-server:jar:2.3.16:compile
      ...

