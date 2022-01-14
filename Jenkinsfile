pipeline {
    agent any
    environmet{
        dockerImage = '20152282/javaapp_$JOB_NAME:$BUILD_NUMBER'
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
              sh "docker build  -t ${dockerImage} ."   
            }
        }
     
    }    
}    

