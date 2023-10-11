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

mvn install == it will compile the code and run the test and also create the artifacts

