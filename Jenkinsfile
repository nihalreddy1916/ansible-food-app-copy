pipeline {
    agent any
    
    parameters {
        string(name: 'COMMIT_REGEX', defaultValue: '', description: 'Regex to filter commit history (e.g., "^b" to match commits starting with "b")')
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Filter Commits') {
            steps {
                script {
                    def commitRegex = params.COMMIT_REGEX
                    sh """
                        if [ -z "${commitRegex}" ]; then
                            echo "No regex pattern provided. Displaying all commits."
                            git log --pretty=format:'%h %s'
                        else
                            echo "Commit History Filtered by Regex: ${commitRegex}"
                            git log --pretty=format:'%h %s' | grep -E '${commitRegex}'
                        fi
                    """
                }
            }
        }
    }
}
