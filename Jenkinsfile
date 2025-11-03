pipeline {
  agent any
  tools { nodejs 'Node 18' }
  stages {
    stage('Checkout') { steps { checkout scm } }
    stage('Install')  { steps { sh 'npm ci || npm install' } }
    stage('Build')    { steps { sh 'npm run build' } }
    stage('Test')     { steps { sh 'npm test' } }
    stage('Archive')  {
      steps {
        sh 'mkdir -p dist && echo artifact > dist/artifact.txt'
        archiveArtifacts artifacts: 'dist/**', fingerprint: true
      }
    }
  }
  post { success { echo 'Node build OK' } failure { echo 'Node build failed' } }
}
