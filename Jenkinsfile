pipeline {
  agent none
  stages {
    stage('Build & Test') {
      agent {
        node {
          label 'docker'
        }

      }
      steps {
        sh 'git clone https://github.com/notfrannco/hello-world.git'
        sh 'pwd'
        sh 'cd hello-world'
        sh 'pwd'
        sh 'mvn clean package'
        sh 'ls -l'
        stash(name: 'build-test-artifacts', includes: 'target/*.war')
      }
    }

    stage('Report & Publish') {
      agent {
        node {
          label 'docker'
        }

      }
      steps {
        unstash 'build-test-artifacts'
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts(onlyIfSuccessful: true, artifacts: 'target/*.war')
      }
    }

  }
}