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
            sh "cd target"
            sh "ls -al" 
              
            }
        }
      stage('Docker Image'){
          steps{
              sh "docker build  -t ${env.dockerImage} ."   
              sh "docker run -p 8082:8080 -e EXTERNAL_PORT=8082 -d --name ${dockerContainerName} ${dockerImage}"
            }
        }
     
    }    
}    

