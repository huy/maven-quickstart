# Help plugin

As mentioned, a lot of maven behaviours is implicit (hidden), it is quite difficult to have an idea what happens if we run a maven phase. Our life line is in the [maven help plugin](http://maven.apache.org/plugins/maven-help-plugin/describe-mojo.html) which provides handy goals to reveal what happen behind the scene. 

    mvn help:help
    
    INFO] Maven Help Plugin 2.2
      The Maven Help plugin provides goals aimed at helping to make sense out of the
      build environment. It includes the ability to view the effective POM and
      settings files, after inheritance and active profiles have been applied, as
      well as a describe a particular plugin goal to give usage information.

    This plugin has 9 goals:
    ...    

    help:describe
      Displays a list of the attributes for a Maven Plugin and/or goals (aka Mojo -
      Maven plain Old Java Object).
    ...

**effective-pom**

maven pom inherits properties from parent pom, which in turn inherits from parent of parent, the [build profiles](build_profile.md) makes even more complicated. `effective-pom` goal gives us what are exact properties of current `pom.xml`.

    $mvn help:effective-pom

**describe**

A plugin goal may has various parameters, the `describe` goal give us details of a specified goal

    $mvn help:describe -Ddetail -Dplugin=failsafe
    
    failsafe:help
      Description: Display help information on maven-failsafe-plugin.
      Call mvn failsafe:help -Ddetail=true -Dgoal=<goal-name> to display
      parameter details.

    failsafe:integration-test
      Description: Run integration tests using Surefire.

    failsafe:verify
      Description: Verify integration tests ran using Surefire.

For more information, run 'mvn help:describe [...] -Ddetail'
