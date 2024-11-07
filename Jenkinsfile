pipeline {
    agent {
        label 'master'
    }
    environment {
        SONAR_TOKEN = '70abe24aab016cff55784f10f38d51e652981507'
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
