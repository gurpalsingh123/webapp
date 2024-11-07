pipeline {
    agent {
        label 'master'
    }
    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
        stage('Sonar-Report') {
            steps {
            sh 'mvn sonar:sonar \
  -Dsonar.projectKey=jenkins_project \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login=squ_d1cceb3000b71ea0fc5da8efcb9e229e0263b4bb'
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
                bat 'mvn clean install sonar:sonar -Dsonar.host.url=http://localhost:9000 -Dsonar.analysis.mode=publish'
            }
        }
    }
}
