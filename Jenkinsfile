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
    stage('JFrogPush') {
      steps {
        echo 'Starting JFrogPush'
        script {
          def server = Artifactory.server "artifactory"
          def buildInfo = Artifactory.newBuildInfo()
          def rtMaven = Artifactory.newMavenBuild()

          rtMaven.tool = 'maven'
          rtMaven.deployer server: server, releaseRepo: 'libs-release-local', snapshotRepo: 'libs-snapshot-local'

          buildInfo = rtMaven.run pom: 'pom.xml', goals: "clean install -Dlicense.skip=true"
          buildInfo.env.capture = true
          buildInfo.name = 'jpetstore-6'
          server.publishBuildInfo buildInfo
        }

        echo 'JFrogPush Finished'
      }
    }
    stage('Deploy Prompt') {
      steps {
        input 'Deploy to production?'
      }
    }
  }
  tools {
    maven 'maven'
  }
  environment {
    TESTER = 'Nick'
  }
}