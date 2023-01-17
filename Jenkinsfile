pipeline {
  agent any
  environment {
    CI = 'true'
  }
  stages {
    stage('Build') {
      steps {
        echo 'Build demo-app'
        sh 'sh run_build_script.sh'
        sh 'npm install'
      }
    }
    stage('Snyk Scan') {
      steps {
        echo 'Snyk Scan'
        snykSecurity failOnError: false, failOnIssues: false, projectName: 'SynkTest', severity: 'medium', snykInstallation: 'InfoSec', snykTokenId: '31c7247a-b712-44e0-9df8-9c8168fc1b84'}
    }
      steps {
        echo 'Deploying...'}}}

pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        echo 'Building...'
      }
    }
    stage('Test') {
      steps {
        echo 'Testing...'
        snykSecurity( failOnError: false, failOnIssues: false, projectName: 'SynkTest', severity: 'medium', snykInstallation: 'InfoSec', snykTokenId: '31c7247a-b712-44e0-9df8-9c8168fc1b84')
      }
    }
    stage('Deploy') {
      steps {
        echo 'Deploying...'
      }
    }
  }
}
