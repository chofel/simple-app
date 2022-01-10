pipeline {
    agent any
    
    tools {
        maven 'Maven'
    }
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    
    
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stage('Upload War To Nexus'){
            steps{
                 nexusArtifactUploader artifacts: [[artifactId: 'simple-app', classifier: '', 
                                                    file: 'target/simple-app/version-3.0.0',
                                                    type: 'war']], credentialsId: 'nexus-user-credentials',
                     groupId: 'in.javahome', nexusUrl: '172.19.9.28', nexusVersion: 'nexus3',
                     protocol: 'http', repository: 'http://172.19.9.28:8081/repository/maven-nexus-sonam/', version: '3.0.0'
            }
        }
    }
}
