pipeline {
    agent any
    parameters {
        string(name: 'BRANCH_NAME', defaultValue: '', description: 'Enter the branch name (e.g., m, develop, feature)')
        string(name: 'COMMIT_ID', defaultValue: '', description: 'Enter the commit ID starting with commit_id_start')
    }
    environment {
        FINAL_BRANCH = "${params.BRANCH_NAME == 'm' ? 'master' : params.BRANCH_NAME}"
        FINAL_COMMIT_ID = "${params.BRANCH_NAME == 'm' && !params.COMMIT_ID ? 'commit_id_start' : params.COMMIT_ID}"
    }
    stages {
        stage('Checkout') {
            steps {
                script {
                    // Print the final values
                    echo "Branch selected: ${params.BRANCH_NAME}"
                    echo "Using branch: ${env.FINAL_BRANCH}"
                    echo "Using commit ID: ${env.FINAL_COMMIT_ID}"
                    
                    // Example git checkout
                    checkout([$class: 'GitSCM', branches: [[name: "*/${env.FINAL_BRANCH}"]],
                              doGenerateSubmoduleConfigurations: false,
                              extensions: [[$class: 'CleanCheckout']],
                              submoduleCfg: [],
                              userRemoteConfigs: [[url: 'https://your-repository-url.git']]])
                    
                    // Reset to specific commit ID if provided
                    if (env.FINAL_COMMIT_ID) {
                        sh "git reset --hard ${env.FINAL_COMMIT_ID}"
                    }
                }
            }
        }
    }
}
