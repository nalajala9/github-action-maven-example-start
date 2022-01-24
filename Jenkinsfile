pipeline {
    agent any
    environment{
    dockerImage = "20152282/javaapp_$JOB_NAME:$BUILD_NUMBER"
    dockerContainerName = 'javaapp_$JOB_NAME_$BUILD_NUMBER'
    }
    tools { 
        maven 'Maven' 
        jdk 'JDK 1.8.*' 
    }
    stages{
        stage('git checkout'){
            steps{
                git branch: 'master',
                url: 'https://github.com/nalajala9/github-action-maven-example-start.git'
            sh "ls -al"
            }
        }
        stage('Build'){
            steps{
            sh 'mvn clean package -Dmaven.test.skip=true'
            sh "ls -al" 
              
            }
        }
      
      stage('Sonar Testing  '){
          steps{
              mvn clean verify sonar:sonar \
              -Dsonar.projectKey=sonar \
              -Dsonar.host.url=http://3.145.10.0:9000 \
              -Dsonar.login=c5df0189f593e4d34a7e9f59122687fa08b6583a
 
            }
        }  
      stage('Build Docker Image '){
          steps{
              sh "docker build  -t ${dockerImage} ." 
            }
        }
        
      stage('Docker Run'){
          steps{
              sh "docker run -dit --name ${dockerContainerName} ${dockerImage}" 
            }
        }  
      stage('Docker Push'){
          steps{
              withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerPWD')]) {
              sh "docker login -u 20152282 -p ${dockerPWD}"
              }
              sh "docker push ${dockerImage}"
            }
        }
    }    
}    

