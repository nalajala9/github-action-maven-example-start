pipeline {
    agent any
    environment{
    dockerImage = "20152282/javaapp_$JOB_NAME:$BUILD_NUMBER"
    dockerContainerName = 'javaapp_$JOB_NAME_$BUILD_NUMBER'
    }
    tools { 
        maven 'Maven' 
        jdk 'JDK 1.11.*' 
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
      
     
        stage('SonarQube analysis') {
            tools {
                jdk "JDK 1.11.*" // the name you have given the JDK installation using the JDK manager (Global Tool Configuration
            }
            environment {
                scannerHome = tool 'SonarQube Scanner' // the name you have given the Sonar Scanner (Global Tool Configuration
            }
            steps {
                withSonarQubeEnv(installationName: 'SonarServer') 
                sh 'mvn sonar:sonar -Dsonar.login=bee80c82793fc89d11329cd51a4e71ec03c3cc27'
                }
            }
        }
      stage('Build Docker Image '){
          steps{
              sh "docker build  -t ${dockerImage} ." 
            }
        }
        
      stage('Docker Run'){
          steps{
              sh "docker run -dit --name ${dockerContainerName} -p 8000:8080 ${dockerImage}" 
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

