pipeline {
    agent any
    
    stages {
        stage('Git Checkout') {
            steps {
                script {
                    git branch: 'main', url: 'https://github.com/loki-4321/demo-counter-app.git'
                }
            }
        }
        
        stage('UNIT testing') {
            steps {
                script {
                    sh 'mvn test'
                }
            }
        }
        
        stage('Integration testing') {
            steps {
                script {
                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }
        
        stage('Maven build') {
            steps {
                script {
                    sh 'mvn clean install'
                }
            }
        }
        
        stage('Static code analysis') {
            steps {
                script {
                    withSonarQubeEnv('Sonar-api-key') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
        
        stage('Quality Gate Status') {
            steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'
                }
            }
        }
    }
}
