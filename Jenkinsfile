pipeline {
  agent any

  stages {
      stage('clean workspace'){
            steps{
                cleanWs()
            }
        }
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar' //so that they can be downloaded later
            }
        }
      stage('Unit Tests') {
            steps {
              sh "mvn test"
            }
            post {
                always {
                junit 'target/surefire-reports/*.xml'
                jacoco execPattern: 'target/jacoco.exec'
                }
            }
        }   
    }
}
