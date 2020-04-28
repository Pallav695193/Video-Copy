pipeline {
  agent {
    node {
      label 'nodejs'
    }

  }
  stages {
     stage ('preamble'){
      steps{
        script{
          echo 'Preamble Stage - Environment info'
 
          openshift.withCluster() {
            openshift.withProject() {
              echo "Using project: ${openshift.project()}"
            }
          }
 
          sh 'npm version'
        }
      }
     }
    stage('Node Check') {
      steps {
        sh 'node -v'
      }
    }
    stage('NPM Check') {
      steps {
        sh 'npm -version'
      }
    }
    stage('Config Check') {
      steps {
        sh 'npm config get registry'
      }
    }
    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }
    stage('Build') {
      steps {
        sh 'npm run --ng build'
        sh 'npx nodeshift'
      }
    }
    stage('Test') {
      steps {
        sh 'npm run --ng test'
      }
    }
  }
}