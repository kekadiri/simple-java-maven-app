pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/kekadiri/simple-java-maven-app.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                 sh 'mvn sonar:sonar'
            }
            
        }
        
        stage('Deploy to Nexus') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: 'http://18.215.156.65:8081',
                    groupId: 'pom.org.sonarqube',
                    version: 'pom.1.0-SNAPSHOT',
                    repository: 'maven-releases',
                    credentialsId: 'nexus',
                    artifacts: [
                        [artifactId: 'sonarscanner-maven-aggregate',
                         file: 'target/my-app-1.0-SNAPSHOT.jar',
                         type: 'jar']
                      
                    ]
                )
            }
        }
