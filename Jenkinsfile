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
  //       stage('Sonar-Report') {
  //           steps {
  //           sh 'mvn sonar:sonar \
  // -Dsonar.projectKey=jenkins_project \
  // -Dsonar.host.url=http://localhost:9000 \
  // -Dsonar.login=sqa_814bcfcd61e3f081215c428528953d4e53e78a41
  //           }
  //       }
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
