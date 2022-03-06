# Maven for Anylogic

1. Download and install the [JDK](https://www.oracle.com/java/technologies/downloads/).

    > **Important**: Make sure the **JAVA_HOME** variable is defined and pointing to the JDK directory, also that the Java bin path is included in the **PATH** variable.

2. [Download](https://maven.apache.org/download.cgi) and [install](https://maven.apache.org/install.html) Maven.    

3. Create a new Anylogic model. For this example, I am using the "External JAR files" found at:

    > **Example Models** > **Models from 'The Big Book of Simulation'** > **Java for Anylogic users**

4. Open the model directory from your favorite IDE, such as VSCODE and INTELLIJ.

5. Here, you can use your IDE to set a new MAVEN project. Alternativelly, you can use the following **pom.xml** configuration file. This config file must be placed on your project`s root directory.

    ```
    <?xml version="1.0" encoding="UTF-8"?>

    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>external.jar.files</groupId>
    <artifactId>model</artifactId>
    <version>1.0</version>

    <dependencies>

        <dependency>
        <groupId>gov.nist.math</groupId>
        <artifactId>jama</artifactId>
        <version>1.0.2</version>
        </dependency>

    </dependencies>

    <build>
        <plugins>
            <plugin>
            <artifactId>maven-dependency-plugin</artifactId>
            <executions>
                <execution>
                    <phase>install</phase>
                    <goals>
                        <goal>copy-dependencies</goal>
                    </goals>
                    <configuration>
                        <outputDirectory>${basedir}/libs</outputDirectory>
                    </configuration>
                </execution>
            </executions>
            </plugin>
        </plugins>
    </build>
    </project>
    ```

    In this file, the only section that needs your attention is the dependencies definition section. List here all the necessary dependencies to run your model, as below:

    ```
    <dependencies>

        <dependency>
            <groupId>gov.nist.math</groupId>
            <artifactId>jama</artifactId>
            <version>1.0.2</version>
        </dependency>

    </dependencies>
    ```

    For more details take a look on this **[link](https://maven.apache.org/plugins/maven-dependency-plugin/usage.html#dependency:copy-dependencies)**.

6. With everything set up, run the command:
    
    `mvn clean install`
    
    This command will make sure that any previous build directories are deleted before the installation of the dependencies. All dependencies will be pulled and moved to the "./libs" folder. 

7. Now, back to Anylogic, add all your JAR dependencies to your model.

    > **Important:** Make sure that Anylogic accesses the JAR files from their **relative path**.

8. Click on the **Compile** button and verify if everything is ok. At this point, you are done and might be able to run your model without any issues.