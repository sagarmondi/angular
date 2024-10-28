pipeline {
  agent any
  environment {
    // Required for Semgrep AppSec Platform-connected scan:
    SEMGREP_APP_TOKEN = credentials('SEMGREP_APP_TOKEN')
  }
  stages {
    stage('Checkout Code') {
      steps {
        // Explicitly checkout code from a specific repository
        git url: 'https://github.com/sagarmondi/angular.git', branch: 'main'
      }
    }
    stage('Semgrep-Scan') {
      steps {
        // Install Semgrep tool
        sh 'pip3 install semgrep'

        // Run the Semgrep scan on the checked-out code
        sh 'semgrep ci'
      }
    }
  }
}
