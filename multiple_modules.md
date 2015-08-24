# Mutiple modules

Maven project can be structured into mutiple modules following parent children tree structure. A module corresponds a folder containing a `pom.xml` file. Parent module's packaging type is `pom` and specifies list of submodules.

    <groupId>org.sonatype.mavenbook.multi</groupId>
    <artifactId>simple-parent</artifactId>
    <packaging>pom</packaging>
    <version>1.0</version>
    <name>Multi Chapter Simple Parent Project</name>
    
    <modules>
        <module>simple-weather</module>
        <module>simple-webapp</module>
    </modules>



References

* https://maven.apache.org/guides/mini/guide-multiple-modules.html
