Why Maven?
- Build management
- Dependency
- Repository
- Reuse plugin -- surefire plugin of unit testing


Maven installation
---------------------
download the Maven and set the path variable 
setting.xml is to customize the behavior of maven

Notes:
  - mvn archetype:generate == this is goal where group id is the java package
  - artifactid is the name of the project
  - 
Explain Pom.xml
  - in the begining it has model version
  - group id, artifact id , version , packaing information, name , url ect.
  - <properties> tag which like <maven.compiler.source> which tells the maven compiler which version of the jre should be use
  - then comes to dependency under which there would be couple of dependency will be there

mvn install == it will compile the code ,run the test and also create the artifacts

![image](https://github.com/sunilcet488/My-Learning/assets/18717063/e15d7765-482c-4d54-b2f5-271b4d034dc3)

Maven plugin and goals
-------------------------
plugin is nothing but a component or extension that can be integrated to maven build
plugin has single or multiple goals.

Goal is nothing but a specific task for example compile, test, package, generate 
goal also takes parameters

example : mvn pluginid:goalId parameters
          mvn archetype:generate -DgroupId=com.skill


![image](https://github.com/sunilcet488/My-Learning/assets/18717063/91f75191-6d13-42bd-b2d2-8586d661ae0c)

maven coordinates there are 4 coordinates
---------------------------
group id - com.sunil reverse name of the domain
artifactid - project name e.g helloworld
version - helloworld.1.0-snapshot.jar == here snapshot is nothing but we are still   
          developing something but once it is release then it helloword.1.0.jar
packaging - jar , ward 


maven repositories
------
default maven location/central repository - https://repo.maven.apache.org/maven2/

enterprise repository - sap has its own for internal use

local repository -- developer machine .m2.repository folder in the user directory
                    all the packages are place in the local repository during the maven build process, also your snapshort.jar will be also be stored over here

Maven dependency
---
  - to skip the test `mvn install -DskipTests` will skip the test
  - By default the packing jar/war file are build using the artifact id + version but this can be changed by using the
    ```
      <build>
        <finalname></finalname>
      </build>
    ```
  -  

Multi module project
---  
  - Multi module project is build based on the parent child pom
    parent pom contains
    `coordinates` with packing type as pom and along with
    `<module></module>`
  -  in the child pom
     ```
       <parent>
          <groupid>parent group id</groupid>
          <artifactid> parent artifact id </artifactid>
          <version> version of the parent</version>
       </parent>
      ```
  - in child pom no need to define the all the coordinates only define the artifact id
  - How to add one submodule dependency in another submodule
    `<dependency></dependency>

  folder organisation in case multimodule project
  ```
    Parent      pom.xml
          child 1   pom.xml
          child 2   pom.xml
  ```
     
**Note:** in the target folder all the compiled code that .class files along the jar dependency libraries are present inside the lib folder

scope
---
there are six scope in Maven like
  - compile: dependency will be available during build, test , and run by default if you don't define any scope then   
    compile will be the scope
  - provided: during test, run then are not needed for deployment example tomcat or servers dependency
  - runtime: test, run
  - test : compile and run the test
  - System : if want to point to path of a library which is not a part of maven dependency or not available in the maven repo then it can be used `<systemPath>` with possible values as a directory
  - import: used for dependenyManagement

     
Dependency Management
---
In a project there could be multiple projects going on, and there might be the case where there version missmatch in the dependency used by different different project. to handle such scenario we have dependeny management in place

so parent pom -- junit version 3.3
    child 1 pom  junit version 3.4 
    child 2 pom  junit version 4.4 

    so to handle this kind of version mismatch issue in case of multi module project
    ```
    maintain dependency in the parent pom
    <dependencyManagement>
        <dependency>
          <version></version>
        </dependency>
    </dependencyManagement>
    ```
    No need to maintain the version the child pom but **still** has to add the dependency in the child pom
    
Just like dependency management, there is also `pluginManagement`-- if you want to make same version or configuration across the multi-module project then use pluginManagement same as dependency management


Profile
---
application should be run across the env. dev, testing, prod -- this can be done using profile
for example database for the dev is H2 for testing and prod it will be HANA 
then you will have two profile for connecting the database for dev and prod profile in pom 

one way to do that created a profile folder in the src/main/profile then have sub folder like dev, test, prod 
inside each subfolder there should be different application.properties files

```
<profiles>
  <profile>
      <id>dev</id>
      <properties>
          <build.profile.id>dev</build.profile.id>
      </properties>
      <build>
          <resources>
              <resource>
                  <directory> </directory>
              </resource>
          </resources
      </build>    
  </profile>
</profiles>
```

how to use the profile while building `mvn install -pdev`


    





          

