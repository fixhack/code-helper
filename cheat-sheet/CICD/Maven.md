## Maven Configuration

- [pom.xml](http://maven.apache.org/pom.html)
- [settings.xml](http://maven.apache.org/settings.html)
- [Sonatype Nexus](http://www.sonatype.org/nexus/): self-hosting a Maven repository

## Maven CLI Commands

General command structure

    mvn -P<profile> <command> <scope>

Simple stuff

    mvn help
    mvn compile
    mvn validate
    mvn verify
    mvn test
    mvn clean 
    mvn clean package
    mvn clean install
    mvn clean deploy

#### Artifacts

    mvn archetype:create                    # Create pom.xml

    mvn archetype:create -DgroupId=<group> \     # Create JAR
                         -DartifactId=<new id>

    mvn archetype:create -DgroupId=<group> \     # Create WAR
                         -DartifactId=<new id> \
                         -DarchetypeArtifactId=maven-archetype-webapp

    mvn install:install-file <params>            # Install dependencies

#### Releasing

    mvn deploy:deploy-file <params ...>

    # Useful release options:
    #
    #    -P <profile>
    #    -Dusername=<user>
    #    -Dpassword=<password>
    #
    mvn release:prepare
    mvn release:clean
    mvn release:perform

#### Tomcat Plugin

    mvn tomcat:deploy
    mvn tomcat:redeploy
    mvn tomcat:undeploy
    mvn tomcat:stop
    mvn tomcat:start

#### IDE integration

    mvn -Declipse.workspace=<path> eclipse:add-maven-repo
    mvn eclipse:eclipse

#### Jenkins Maven Plugin

-   [Jenkins Maven Plugin](https://github.com/davidmoten/aws-maven-plugin)

#### Disable SSL Certificate
You can disable SSL certificate checking by adding one or more of these command line parameters:

```
-Dmaven.wagon.http.ssl.insecure=true - enable use of relaxed SSL check for user generated certificates.
-Dmaven.wagon.http.ssl.allowall=true - enable match of the server's X.509 certificate with hostname. If disabled, a browser like check will be used.
-Dmaven.wagon.http.ssl.ignore.validity.dates=true - ignore issues with certificate dates.
Dmaven.resolver.transport=wagon - In Maven 3.9.0 and newer, they've switched to using Apache HttpClient 4 by default. You need to use this to switch back to wagon for the above flags to work.
````

Official documentation: http://maven.apache.org/wagon/wagon-providers/wagon-http/

Here's the oneliner for an easy copy-and-paste:

```
-Dmaven.wagon.http.ssl.insecure=true -Dmaven.wagon.http.ssl.allowall=true -Dmaven.wagon.http.ssl.ignore.validity.dates=true
Ajay Gautam suggested that you could also add the above to the ~/.mavenrc file as not to have to specify it every time at command line:
```

```
$ cat ~/.mavenrc 
MAVEN_OPTS="-Dmaven.wagon.http.ssl.insecure=true -Dmaven.wagon.http.ssl.allowall=true -Dmaven.wagon.http.ssl.ignore.validity.dates=true"
```

#### 
The answer above is a good working solution, but here's how to do it if you want to use the SSL repo:

Use a browser (I used IE) to go to https://repo.maven.apache.org/
Click on lock icon and choose "View Certificate"
Go to the "Details" tab and choose "Save to File"
Choose type "Base 64 X.509 (.CER)" and save it somewhere
Now open a command prompt and type (use your own paths):

```
keytool -import -file C:\temp\mavenCert.cer -keystore C:\temp\mavenKeystore
````

Now you can run the command again with the parameter

```
-Djavax.net.ssl.trustStore=C:\temp\mavenKeystore
```

Under linux use absolute path

```
-Djavax.net.ssl.trustStore=/tmp/mavenKeystore
```

otherwise this will happen

Like this:

```
mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false -Djavax.net.ssl.trustStore=C:\temp\mavenKeystore
```

Optional:

You can use the MAVEN_OPTS environment variable so you don't have to worry about it again. See more info on the MAVEN_OPTS variable [here](https://maven.apache.org/guides/mini/guide-repository-ssl.html)