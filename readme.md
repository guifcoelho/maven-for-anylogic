# Maven for Anylogic

A quick tutorial on how to setup Maven to manage Anylogic dependencies.

## Steps


1. Download and install the [JDK](https://www.oracle.com/java/technologies/downloads/).

    > **Important**: Make sure the **JAVA_HOME** variable is defined and pointing to the JDK directory, also that the Java bin path is included in the **PATH** variable.

2. [Download](https://maven.apache.org/download.cgi) and [install](https://maven.apache.org/install.html) Maven.    

3. Create a new Anylogic model. For this example, I am using the "External JAR files" found at:

    > **Example Models** > **Models from 'The Big Book of Simulation'** > **Java for Anylogic users**

4. Open the model directory from your favorite IDE, such as VSCODE and INTELLIJ.

5. Here, you can use your IDE to set a new MAVEN project. Alternativelly, you can use the **pom.xml** configuration file of this repository as an initial boilerplate (the config file must be placed on your project`s root directory). 

    The only section that needs your attention is the dependencies definition section. List here all the necessary dependencies to run your model, as below:

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