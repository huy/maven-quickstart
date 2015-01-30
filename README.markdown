## Basic concepts

Maven is predominant build tool for java ecosystem. It is significant different compare to traditional build tools such as make, ant, rake. 
I highlight here some differences Maven phase and goal is more less same as task in other tools. 

When running Maven command line mvn, we specify phase or goal a input parameter. Number of phases are fixed for each life cycle see 
[http://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html#Lifecycle_Reference]

Life cycles are either default, clean or site. As phases are unique among all life cycles, we don't care about a life cycle and just refer to a phase
Phases are executed sequentially,  dependencies between phases are implicit.

In order to have phase to do a meaningful stuff (compile, run test,  create package) we need to bind  goal(s) to a phase. A goal is a piece of code 
implement in Maven Plugin that get executed to produce artifacts. 

Many goals can be bound to a phase. When running Maven command line mv with phase as input, bound goals get executed in the same order as they get attached 
to the phase. 

When running Maven command line mvn with goal in form of plugin:goal as input, maven execute a specified goal implemented in the plugin Goals are implemented 
in Maven Plugins e.g. java compiler plugins, test runner plugin. 

Maven provides core plugins and default binding to support most typical java project. E.g  bindings when we specifies 'pom' as packaging (in POM file) is

    Phase	Goal(s)	Note
    package	site:attach-descriptor	run attach-descriptor goal provided by plugin site
    install	install:install	run install goal provided by plugin install
    deploy	deploy:deploy	run deploy goal provided by plugin deploy

Maven is driven by pom.xml file. POM file specifies how goals are bound to each phase. A plugin may also specify default binding (using @phase notation) for it goals. 
See [http://maven.apache.org/pom.html].

POM stands for Project Object Model. POM can be inherited. A child POM inherits all setting from its parent then enrich or override certain behavior following the 
same OOP paradigm. The effective POM can be showed using 

    mvn org.apache.maven.plugins:maven-help-plugin:2.2:effective-pom

If a project uses libraries, they should be specified as project dependencies with version and repository from which maven downloads when needed

## Examples running maven phases

Clean

    C:\huy\gitrepos\rubyjobbuilder\groovy>mvn clean
    [INFO] Scanning for projects...
    ...
    [INFO] --- maven-clean-plugin:2.5:clean (default-clean) @ build-flow-scripts ---
    [INFO] Deleting C:\huy\gitrepos\rubyjobbuilder\groovy\target
    [INFO] ------------------------------------------------------------------------
    [INFO] BUILD SUCCESS
    [INFO] ------------------------------------------------------------------------
    Compile
    C:\huy\gitrepos\rubyjobbuilder\groovy>mvn compile
    [INFO] Scanning for projects...
    ...
    [INFO] --- gmaven-plugin:1.4:compile (default) @ build-flow-scripts ---
    [INFO] Compiled 35 Groovy classes
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
     Running com.wonga.techops.jenkins.AddConsoleScriptTest
     Tests run: 3, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.728 sec
     Running com.wonga.techops.jenkins.CheckScriptTest
     Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.064 sec
     Running com.wonga.techops.jenkins.GateScriptTest
     Tests run: 10, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.395 sec
     Running com.wonga.techops.jenkins.VerifyScriptRunTest
     Tests run: 3, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.17 sec
     Running com.wonga.techops.jenkins.VerifyScriptTestResultTest
     Tests run: 3, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.005 sec
     Results :
     Tests run: 20, Failures: 0, Errors: 0, Skipped: 0

Test single class 

     C:\huy\gitrepos\rubyjobbuilder\groovy>mvn -Dtest=AddConsoleScriptTest test
     [INFO] Scanning for projects...
     ...
     -------------------------------------------------------
      T E S T S
      -------------------------------------------------------
      Running com.wonga.techops.jenkins.AddConsoleScriptTest
      Tests run: 3, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.791 sec
      Results :
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
       [INFO] ------------------------------------------------------------------------
       [INFO] BUILD SUCCESS
       [INFO] ------------------------------------------------------------------------

