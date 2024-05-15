pipeline {
    agent any

    stages {
        stage('List Branches') {
            steps {
                script {
                    // Get the list of branches from Git
                    def branches = sh(script: 'git ls-remote --heads origin', returnStdout: true).trim().split('\n')

                    // Filter branches based on the search query
                    def searchTerm = 'b' // Change this to your search query
                    def filteredBranches = branches.findAll { it.contains(searchTerm) }

                    // Print out the branches and commit IDs
                    for (branch in filteredBranches) {
                        def branchName = branch.tokenize('refs/heads/')[1].trim()
                        def commitId = branch.tokenize('\t')[0].trim()
                        echo "Branch: ${branchName}, Commit ID: ${commitId}"
                    }
                }
            }
        }
    }
}
