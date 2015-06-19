## Basic concepts

Maven is predominant build tool for java ecosystem. It is significant different compare to traditional build tools such as make, ant, rake. 

I highlight here some differences Maven phase and goal is more less same as task in other tools. 

**phase and goal**

When running Maven command line `mvn`, we specify either `phase` or `goal` a input parameter. Number of `phase`s are fixed for each life cycle. See [http://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html#Lifecycle_Reference]

Life cycles are either `default`, `clean` or `site`. As `phase`s are unique among all life cycles, we don't care about a life cycle and just work with `phase` and `goal`. Phases are executed sequentially,  dependencies between phases are implicit.

A phase is by convention a single name e.g. `compile`, `test`, `test-compile` while a goal is combination of 2 or more names separated by `:` in form of  `<plugin-prefix>:<goal>` or `<plugin-group-id>:<plugin-artifact-id>[:<plugin-version>]:<goal>`

In order to have `phase` to do a meaningful stuff (compile, run test,  create package) we need to bind  `goal`(s) to a `phase`. A `goal` is a piece of code implement in Maven Plugin that get executed to produce artifacts. 

**binding**

Many `goal`s can be bound to a `phase`. When running Maven command line `mvn` with `phase` as input, bound `goal`s get executed in the same order as they get attached to the `phase`. 

When running Maven command line `mvn` with goal in form of `plugin:goal` as input, maven execute a specified `goal` implemented in the `plugin` goals are implemented in Maven Plugins e.g. java compiler plugins, test runner plugin.

Maven provides core `plugin`s and default binding to support most typical java project, which is specified using tag `packaging` in `pom.xml` file. 
    
     </project>
     ...  
       <packaging>war</packaging>
     ...
     </project>

E.g  bindings when we specifies `pom` as packaging (in POM file) is

 Phase         | Goal(s)                | Notes 
 ------------- |------------------------| --------------------------------------------------
 package       | site:attach-descriptor | run attach-descriptor goal provided by plugin site
 install	   | install:install	    | run install goal provided by plugin install
 deploy	       | deploy:deploy	        | run deploy goal provided by plugin deploy

**pom.xml**

Maven is driven by `pom.xml` file. POM file specifies how goals are bound to each phase. A plugin may also specify default binding (using `@phase` notation) for it goals. See [http://maven.apache.org/pom.html].

POM stands for Project Object Model. POM can be inherited. A child POM inherits all setting from its parent then enrich or override certain behavior following the 
same OOP paradigm. The effective POM can be showed using 

    mvn org.apache.maven.plugins:maven-help-plugin:2.2:effective-pom

If a project uses libraries, they should be specified as project dependencies with version and repository from which maven downloads when needed

**plugin**

Plugins can be written in Java or any of a number of scripting languages. Plugins consists of one or more `mojos`, each one being the implementation for one of the plugin's goals. To make use of a plugin and the plugin goals, we need to specify it in `pom.xml`. E.g.

    <project>
    ...
      <build>
        <plugins>
          <plugin>
            <artifactId>maven-myquery-plugin</artifactId>
            <version>1.0</version>
            <configuration>
              <url>http://www.foobar.com/query</url>
              <timeout>10</timeout>
              <options>
                <option>one</option>
                <option>two</option>
                <option>three</option>
              </options>
            </configuration>
          </plugin>
        </plugins>
      </build>
    ...
    </project>

**running**

We run maven by type `mvn` and one of phases defined by maven [here](http://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html#Lifecycle_Reference) or a goals implemented by a plugin specified in `pom.xml`. If it is a phase then depending on goal to phase binding defined in plugins, appropriate goals will be executed . Some typical examples are [here](example.md).

**references**

* http://tutorials.jenkov.com/maven/maven-tutorial.htm
