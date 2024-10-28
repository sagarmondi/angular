pipeline {
  agent any
  environment {
    // Required for Semgrep AppSec Platform-connected scan:
    SEMGREP_APP_TOKEN = credentials('SEMGREP_APP_TOKEN')
  }
  stages {
    stage('Semgrep-Scan') {
      steps {
        // Install Semgrep tool
        sh 'sudo pip3 install semgrep'

        // Run the Semgrep scan with default rules
        sh 'semgrep ci'
        
        // Optionally save the output in a JSON file
        // Uncomment the following line if you want to capture the output in a file
        sh 'semgrep --output-path results.json'
      }
    }
  }
}
