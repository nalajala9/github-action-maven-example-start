pipeline {
    agent any
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
    }    
}    

