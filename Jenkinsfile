pipeline {
  agent any

  stages {
      stage('clean workspace'){
            steps{
                cleanWs()
            }
      }
      stage('Checkout from Git') {
            steps {
                git branch: 'main', url: 'https://github.com/Veeresh2708/webapp.git'
            }
      }
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.war' 
            }
        }
      stage('Unit Tests') {
            steps {
              sh "mvn test jacoco:report"
            }
            post {
                always {
                junit 'target/surefire-reports/*.xml'
                jacoco execPattern: 'target/jacoco.exec'
                junit allowEmptyResults: true, testResults: '**/test-results/*.xml
                }
            }
        }   
    }
}
