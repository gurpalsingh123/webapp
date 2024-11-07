pipeline {
    agent {
        label 'master'
    }
    environment {
        SONAR_TOKEN = 'f2f77007eb8d414357a507b7818d8266f737bcf6'
    }

    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') { 
            steps {
                bat 'mvn test' 
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml' 
                }
            }
        }
        stage('Sonar-Report') {
            steps {
                bat 'mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=gurpalsingh123_webapp'
            }
        }
    }
}
