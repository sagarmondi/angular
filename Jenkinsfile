pipeline {
    agent any
    environment {
        SEMGREP_API_TOKEN = credentials('semgrep-api-token') // Store your Semgrep API token securely
        DEPLOYMENT_SLUG = 'your-deployment-slug' // Replace with your deployment slug
        SEMGREP_POLICIES = 'rule-board-block,rule-board-pr-comments' // Comma-separated policies
        SEMGREP_RULES = 'typescript.react.security.audit.react-no-refs.react-no-refs,ajinabraham.njsscan.hardcoded_secrets.node_username' // Comma-separated rules
    }
    stages {
        stage('Semgrep Scan') {
            steps {
                script {
                    // Convert the environment variables into arrays for inclusion in the API call
                    def policies = SEMGREP_POLICIES.split(',').collect { it.trim() }
                    def rules = SEMGREP_RULES.split(',').collect { it.trim() }
                    
                    // Formulate the API request
                    def apiUrl = "https://semgrep.dev/api/v1/deployments/${DEPLOYMENT_SLUG}/findings"
                    def policyParams = policies.collect { "policies=${it}" }.join('&')
                    def ruleParams = rules.collect { "rules=${it}" }.join('&')
                    
                    // Combine all parameters into the query string
                    def queryParams = "${policyParams}&${ruleParams}"

                    // Execute the API call
                    sh """
                    curl -X GET "${apiUrl}?${queryParams}" \
                        -H "Authorization: Bearer ${SEMGREP_API_TOKEN}" \
                        -H "Content-Type: application/json"
                    """
                }
            }
        }
    }
}
