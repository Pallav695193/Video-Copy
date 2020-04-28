pipeline {
  agent {
    node {
      label 'nodejs'
    }

  }
  stages {
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
        sh 'npx nodeshift --strictSSL=false --dockerImage=bucharestgold/centos7-s2i-web-app --imageTag=10.x --build.env OUTPUT_DIR=dist/your-angular-app-name --expose'
      }
    }
    stage('Test') {
      steps {
        sh 'npm run --ng test'
      }
    }
  }
}