pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Building'
        sh 'mvn clean install -Dlicense.skip=true'
      }
    }
  }
  tools {
    maven 'maven'
  }
}