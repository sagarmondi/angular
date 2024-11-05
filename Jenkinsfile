pipeline {
  agent any
  environment {
    SEMGREP_APP_TOKEN = credentials('SEMGREP_APP_TOKEN') // Token for Semgrep
  }
  stages {

    stage('Build') {
      steps {
        echo 'Building application...'
         // Example for a Node.js application
      }
    }

    stage('SCA - Software Composition Analysis') {
      steps {
        echo 'Running SCA scan...'
        
        // Capture rules with a dry run before scanning
        sh '/var/lib/jenkins/.local/bin/semgrep --config=auto --dryrun > sca_rules_list.txt'
        
        // Run Semgrep for actual SCA scan
        sh '/var/lib/jenkins/.local/bin/semgrep --config=auto --json -o sca_results.json'
      }
    }

    stage('SAST - Static Application Security Testing') {
      steps {
        echo 'Running SAST scan...'

        // Capture rules with a dry run before scanning
        sh '/var/lib/jenkins/.local/bin/semgrep ci --dryrun > sast_rules_list.txt'
        
        // Run Semgrep for actual SAST scan
        sh '/var/lib/jenkins/.local/bin/semgrep ci --json --no-suppress-errors -o sast_results.json'
      }
    }

    stage('DAST - Dynamic Application Security Testing') {
      steps {
        echo 'Running DAST scan...'
        // Placeholder for DAST tool (e.g., OWASP ZAP)
        // Example: sh 'zap-cli quick-scan http://your-app-url'
      }
    }

    stage('IAST - Interactive Application Security Testing') {
      steps {
        echo 'Running IAST scan...'
        // Placeholder for IAST tool
        // Example: sh 'some_iast_tool --scan'
      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploying application...'
        // Example deployment command
      }
    }

    stage('Monitor') {
      steps {
        echo 'Setting up monitoring...'
        // Placeholder for monitoring setup
      }
    }
  }

  post {
    always {
      // Archive JSON results and the rule lists
      archiveArtifacts artifacts: '*.json, *_rules_list.txt', allowEmptyArchive: true
    }
  }
}
