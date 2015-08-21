# Maven version

We can specify the version of maven to be used in `pom.xml` file e.g.

    <prerequisites>
      <maven>3.0.5</maven>
    </prerequisites>

Other option is to install maven version manager the create a file `mvnvm.properties` in the same folder as `pom.xml`

    $ cat mvnvm.properties
    mvn_version=2.2.1

maven version manager has it own version of `mvn` script that takes into account `mvnvm.properties` and run 
specified version of maven.

Reference

* http://mvnvm.org/
