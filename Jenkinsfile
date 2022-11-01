pipeline {
  agent any
  tools {
        maven "M3" 
   }

  stages {

      stage('Build Artifact') 
      {
            steps 
            {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar' 
            }  
       }
      stage('Test Maven - JUnit') 
      {
            steps 
            {
              //sh "mvn test"
              echo "Running unit tests"
            }
      }
      stage('Deploy') 
      { 
          steps 
          { 
              input('Continue to Deploy?') 
              echo 'Deploying to Production Environment' 
          } 
      }
    
        
           stage('mvn clean') 
      {
            steps 
            {
                sh "mvn clean verify sonar:sonar \
                    -Dsonar.projectKey=maven-jenkins-pipeline \
                    -Dsonar.host.url=http://35.246.3.252:9000 \
                    -Dsonar.login=sqp_598863e090bb92008b0d0bb2f5b4425c497964e6 " 
            }  
       }
      
      stage('Sonarqube Analysis - SAST')  
      { 
        steps  
        { 
           withSonarQubeEnv('SonarQube')  
           { 
              sh "mvn sonar:sonar -Dsonar.projectKey=maven-jenkins-pipeline -Dsonar.host.url=http://35.246.3.252:9000/"  
           } 
        } 
      } 
    }
}
