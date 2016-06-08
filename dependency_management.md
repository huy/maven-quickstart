# dependency management

Maven automatically treats dependency as transitive. So if our project P depends on library A, which in turns depends 
on others libraries B and C. Then it is suffice to declare that P depends on A. Maven will automatically incluldes B and C 
into classpath.

That convenience however comes with a cost, which is the version conflict. Let say if A depends on one version 1 of D and C 
depends on version 2 of D, then maven has to decide which version of D it is going to add to the class path. Maven treats
dependencies as a tree and simply chooses the one closest to the root. In our example, D version 1 will be chosen. 

This behaviour leads to common practice to declare version of all dependencies in `dependencyManagement` section of 
the root `pom.xml`  e.g.

     <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.flywaydb</groupId>
                <artifactId>flyway-core</artifactId>
                <version>${flywaydb.version}</version>
            </dependency>
