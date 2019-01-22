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
  }
  tools {
    maven 'maven'
  }
}