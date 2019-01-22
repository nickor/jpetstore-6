pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Building'
        sh 'mvn clean install -Dlicense.skip=true'
        echo 'Build finished'
      }
    }
    stage('Testing Stage') {
      parallel {
        stage('Testing Stage') {
          steps {
            sh 'mvn sonar:sonar -Dsonar.host.url=http://54.255.229.154:8081 -Dlicense.skip=true'
          }
        }
        stage('Print Tester Credentials') {
          steps {
            echo "The tester is ${TESTER}"
            sleep 10
          }
        }
        stage('Print build number') {
          steps {
            echo "This is build number ${BUILD_ID}"
            sleep 20
          }
        }
      }
    }
  }
  tools {
    maven 'maven'
  }
}