# DevOps for Web Development
This is the code repository for [DevOps for Web Development](https://www.packtpub.com/networking-and-servers/devops-web-development?utm_source=github&utm_medium=repository&utm_content=9781786465702), published by Packt. It contains all the supporting project files necessary to work through the book from start to finish.

## Instructions and Navigation

All of the code is organized into folders. Each folder starts with a number followed by the application name. For example, `Chapter 2`. 

Code Snippet:
```
 <properties>
        <jpa.database>MYSQL</jpa.database>
        <jdbc.driverClassName>com.mysql.jdbc.Driver</jdbc.driverClassName>
        <jdbc.url>jdbc:mysql://localhost:3306/petclinic?useUnicode=true</jdbc.url>
        <jdbc.username>root</jdbc.username>
        <jdbc.password>petclinic</jdbc.password>
    </properties>
```
#### Chapter 1:
You can find all the necessary code **[here](https://github.com/spring-projects/spring-petclinic)** for the chapter 1.

#### Chapter 2:

```
java -jar jenkins.war --httpPort=9999
java -jar jenkins.war --httpsPort=8888
java -jar slave.jar -jnlpUrl http://192.168.1.34:8080/computer/TestServer/slave-agent.jnlp -secret 65464e02c58c85b192883f7848ad2758408220bed2f3af715c01c9b01cb72f9b
```
#### Chapter 3:

**Sonar.properties**
*Required metadata *
```
sonar.projectKey=java-sonar-runner-simple 
sonar.projectName=Simple Java project analyzed with the SonarQube Runner 
sonar.projectVersion=1.0
```
**Comma-separated paths to directories with sources (required)**
`onar.sources=src`

**Language**
`sonar.language=java`
**Encoding of the source files **
`sonar.sourceEncoding=UTF-8`

#### Chapter 4:
```
echo 'Hello from Pipeline Demo'
stage 'Compile'
build 'PetClinic-Compile'
stage 'Test'
build 'PetClinic-Test'
```
---------------

```
echo 'Hello from Pipeline Demo'
stage 'Compile'
node {
  git url: 'https://github.com/mitesh51/spring-petclinic.git'
  def mvnHome = tool 'Maven3.3.1'
  sh "${mvnHome}/bin/mvn -B compile"
}
stage 'Test'
node('WindowsNode') {
  git url: 'https://github.com/mitesh51/spring-petclinic.git'
  def mvnHome = tool 'WindowsMaven'
  bat "${mvnHome}\\bin\\mvn -B verify"
  step([$class: 'ArtifactArchiver', artifacts: '**/target/*.war', fingerprint: true])  
  step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])
}
```
----------------
```
Create a user with name admin and assign password and roles as below. 
<role rolename="manager-gui"/>
<role rolename="manager-script"/>
<user username="admin" password="cloud@123" roles="manager-script" />
Now, we need to add Tomcat's admin user that we created in the Maven setting file.
<servers>
<server>
  <id>tomcat-development-server</id>
  <username>admin</username>
  <password>password</password>
</server>
</servers>
```
-----------------

Find *Tomcat* Plugin block in `Pom.xml` and add following details. Make sure that **Server Name** is same that we provided in `settings.xml` of Maven as **Id**:

<plugin>
                <groupId>org.apache.tomcat.maven</groupId>
                <artifactId>tomcat7-maven-plugin</artifactId>
                <version>2.2</version>
                <configuration>
                    <server>tomcat-development-server</server>
			<url>http://192.168.1.35:9999/manager/text</url>
			<warFile>target\petclinic.war</warFile>
			<path>/petclinic</path>
                </configuration>
 </plugin>

-------------------


