# Mutiple modules

Maven project can be structured into mutiple modules following parent children tree structure. A module corresponds a folder containing a `pom.xml` file. 

**Parent**

Parent module's packaging type is `pom` and specifies list of submodules.

    <groupId>org.sonatype.mavenbook.multi</groupId>
    <artifactId>simple-parent</artifactId>
    <packaging>pom</packaging>
    <version>1.0</version>
    <name>Multi Chapter Simple Parent Project</name>
    
    <modules>
        <module>simple-weather</module>
        <module>simple-webapp</module>
    </modules>


**Child**

Submodule refers to parent in its `pom.xml`

    <parent>
        <groupId>org.sonatype.mavenbook.multi</groupId>
        <artifactId>simple-parent</artifactId>
        <version>1.0</version>
    </parent>
    <artifactId>simple-weather</artifactId>
    <packaging>jar</packaging>

A Submodule can has dependency as other submodule

    <dependencies>
        <dependency>
            <groupId>org.sonatype.mavenbook.multi</groupId>
            <artifactId>simple-weather</artifactId>
            <version>1.0</version>
        </dependency>
    </dependencies>
    
**Execution**

When Maven is executed against a project with submodules, Maven first loads the parent POM and locates all of the submodule POMs. 

Maven then puts all of these project POMs into something called the Maven Reactor which analyzes the dependencies between modules. The Reactor takes care of ordering components to ensure that interdependent modules are compiled and installed in the proper order.

Once the Reactor figures out the order in which projects must be built, Maven then executes the specified goals for every module in the multi-module build.

References

* https://maven.apache.org/guides/mini/guide-multiple-modules.html
