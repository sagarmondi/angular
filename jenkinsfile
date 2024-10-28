pipeline {
    agent any
    environment {
        SEMGREP_TOKEN = credentials('SEMGREP_APP_TOKEN')  // Replace with your Jenkins secret ID for the Semgrep API token
        SEMGREP_API_URL = 'https://semgrep.dev'  // Base URL for Semgrep API
    }
    stages {
        stage('List Semgrep Projects') {
            steps {
                script {
                    def response = sh (
                        script: """
                            curl -s -H "Authorization: Bearer $SEMGREP_TOKEN" \
                            "$SEMGREP_API_URL/orgs/sagarmondi917_personal_org/projects"
                        """,
                        returnStdout: true
                    ).trim()
                    
                    echo "Semgrep Projects:"
                    echo "${response}"
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline completed.'
        }
        failure {
            echo 'Failed to retrieve projects from Semgrep platform. Check token or network access.'
        }
    }
}
