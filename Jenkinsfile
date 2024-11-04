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
          // Run the Semgrep scan without --config parameter since we are logged into Semgrep App
          sh '/var/lib/jenkins/.local/bin/semgrep ci --json --no-suppress-errors -o results.json'
          
          // Run supply chain analysis explicitly (if not included by default) and append to results.json
          sh '/var/lib/jenkins/.local/bin/semgrep supply-chain --json >> results.json'
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
