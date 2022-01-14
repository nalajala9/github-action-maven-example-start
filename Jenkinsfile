pipeline {
    agent any
    environment{

    }
    tools { 
        maven 'Maven 3.8.6' 
        jdk 'JDK 1.8.*' 
    }
    stages{
        stage('git checkout'){
            steps{
                git branch: 'master',
                credentialsId: 'git_hub',
                url: 'https://github.com/nalajala9/github-action-maven-example-start.git'
            sh "ls -la"
            }
        }
        stage('Build'){
            steps{
            sh 'mvn clean package -Dmaven.test.skip=true' 
            sh '**/target/*.jar${env.Build_Number}'
            sh "ls -al"
              
            }
        }
    }    
}    

