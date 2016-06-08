# dependency management

Maven automatically treats dependency as transitive. So if our project P depends on library A, which in turns depends 
on others libraries B and C. Then it is suffice to declare that P depends on A. Maven will automatically incluldes B and C 
into classpath.

**dependency management**

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

**exclusion**

Sometime, it is not possible to specify version in the `dependecyManagement`, e.g. when the same package are bundled in 2 different artifacts in the dependency tree. We can solve that problem by excluding an un wanted artifact when including a dependency. e.g.

         <dependency>
             <groupId>com.google.apis</groupId>
             <artifactId>google-api-services-vision</artifactId>
             <exclusions>
               <exclusion>
                   <groupId>com.google.guava</groupId>
                   <artifactId>guava-jdk5</artifactId>
               </exclusion>
              </exclusions>
         </dependency>

**references**

* https://maven.apache.org/guides/introduction/introduction-to-optional-and-excludes-dependencies.html

