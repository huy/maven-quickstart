# Build profile

Maven build profile is the way to conditionally bind a goal to a phase, e.g.

    <profiles>
        <profile>
          <id>integ</id>
          <activation>
            <activeByDefault>false</activeByDefault>
          </activation>
          <build>
            <plugins>
              <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-failsafe-plugin</artifactId>
              </plugin>
            </plugins>
          </build>
        </profile>
      </profiles>

If the profile is not activated by default, then we can activate it explicitly by using `-P` option when running `mvn` command e.g.

     $mvn install -P integ

There are in facts many other ways to activate profile such as

* Through Maven settings
* Based on environment variables
* OS settings
* Present or missing files

References

* http://maven.apache.org/guides/introduction/introduction-to-profiles.html
