pipeline {
  agent any
  environment {
    // Required for Semgrep AppSec Platform-connected scan
    SEMGREP_APP_TOKEN = credentials('SEMGREP_APP_TOKEN')
  }
  stages {
    stage('Install Semgrep') {
      steps {
        // Install Semgrep tool
        sh 'pip3 install semgrep'
      }
    }
    
    stage('Run Semgrep Scan') {
      steps {
        script {
          // Run the Semgrep scan with CI mode, which includes both code and supply chain scans
          sh '/var/lib/jenkins/.local/bin/semgrep ci --json --no-suppress-errors -o results.json'
        }
      }
    }

    stage('Archive Results') {
      steps {
        // Archive the results.json file as an artifact in Jenkins
        archiveArtifacts artifacts: 'results.json', allowEmptyArchive: true
      }
    }
  }
}
