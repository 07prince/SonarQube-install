 # SonarQube install 

 ### Configure a Sonar Server locally



apt install unzip

sudo su -   (this will take u to root user)

adduser sonarqube

sudo su - sonarqube

wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.4.0.54424.zip

unzip *

chmod -R 755 /home/sonarqube/sonarqube-9.4.0.54424

chown -R sonarqube:sonarqube /home/sonarqube/sonarqube-9.4.0.54424

cd sonarqube-9.4.0.54424/bin/linux-x86-64/

./sonar.sh start

# Hurray !! Now you can access the SonarQube Server on http://<ip-address>:9000




# jenkins use

# now if u want to use this into jenkins then follow steps


# steps to generate the token 
step 1 : open sonarqube(http://<ip-address>:9000)
step 2 : my account (top right)
step 3 : security
step 4 : generate tokens (u can use jenkins)
step 5 : generate token and  # copy it

# copy token into jenkins
 mangae jenkins --> credentials --> system --> global credentials  --> add credentials

 kind    = secret text
 secret  = copy token
 id      = sonarqube

 click on create button



open jenkins at port 8080

# download sonarqube sacnner plugins
mangae jenkins --> plugins ----> available plugins ---> search ---> sonarQube scanner

 #### every time u download any plugins or do some changes u should restart the jenkins 



 # code for sonarqube in jenkins 

 stage('Static Code Analysis') {
      environment {
        SONAR_URL = "http://34.201.116.83:9000"
      }
      steps {
        withCredentials([string(credentialsId: 'sonarqube', variable: 'SONAR_AUTH_TOKEN')]) {
          sh 'cd java-maven-sonar-argocd-helm-k8s/spring-boot-app && mvn sonar:sonar -Dsonar.login=$SONAR_AUTH_TOKEN -Dsonar.host.url=${SONAR_URL}'
        }
      }
    }



# commands for the sonarqube (used to in the code)

1. Java with Maven
Command: mvn sonar:sonar

2.Java with Gradle
Command: ./gradlew sonarqube

3.Python
Command: sonar-scanner -Dsonar.projectKey=my-python-project -Dsonar.sources=.


4. JavaScript / Node.js
Command: sonar-scanner


5.C# / .NET
Command: dotnet sonarscanner begin /d:sonar.host.url=${SONAR_URL} /d:sonar.login=$SONAR_AUTH_TOKEN && dotnet build && dotnet sonarscanner end /d:sonar.login=$SONAR_AUTH_TOKEN





6.PHP
Command: sonar-scanner


7.Ruby
Command: sonar-scanner




8.Go
Command: sonar-scanner
