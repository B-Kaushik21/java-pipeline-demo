pipeline{
    agent any

    stages{
        stage('Checkout'){
            steps{
                echo 'Checking out source code...'
            checkout scm
            }
        }
        stage('install Dependencies'){
            steps{
                echo 'Installing dependencies...'
            bat 'mvn clean install -DskipTests'
            }
        }
        stage('Build'){
            steps{
                echo 'Building the application...'
            bat 'mvn package -DskipTests'
            }
        }
        stage('Test'){
            steps{
                echo 'Running tests...'
            bat 'mvn test'
            }
        }
        stage('archive Artifacts'){
            steps{
            echo 'Archiving build artifacts...'
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post{
        success{
            echo 'Build completed successfully!'
        }
        failure{
            echo 'Build failed. Please check the logs.'
        }
    }
}