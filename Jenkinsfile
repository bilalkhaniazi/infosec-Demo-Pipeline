pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build demo-app'
        sh 'sh run_build_script.sh'
      }
    }
    stage('Snyk Scan') {
      steps {
        echo 'Snyk Scan'
        snykSecurity failOnError: true, failOnIssues: true, projectName: 'Synk Test', severity: 'medium', snykInstallation: 'Snyk', snykTokenId: '31c7247a-b712-44e0-9df8-9c8168fc1b84'
      }
    }

    stage('Linux Tests') {
      parallel {
        stage('Linux Tests') {
          steps {
            echo 'Run Linux tests'
            sh 'sh run_linux_tests.sh'
          }
        }

        stage('Windows Tests') {
          steps {
            echo 'Run Windows tests'
          }
        }

      }
    }

    stage('Deploy Staging') {
      steps {
        echo 'Deploy to staging environment'
        input 'Ok to deploy to production?'
      }
    }

    stage('Deploy Production') {
      post {
        always {
          archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
        }

        failure {
          emailext(subject: 'Demoapp build failure', to: 'bvazcosta@gmail.com', body: 'Build failure for demoapp Build ${env.JOB_NAME} ')
        }

      }
      steps {
        echo 'Deploy to Prod'
      }
    }

  }
}
