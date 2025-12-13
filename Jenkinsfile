pipeline {
    agent any

    stages {
        stage('Show Files') {
            steps {
                echo "Listing workspace files"
                sh 'ls -la'
            }
        }

        stage('Read TXT') {
            steps {
                script {
                    def files = sh(script: "ls *.txt || echo ''", returnStdout: true).trim()
                    if (files) {
                        echo "TXT files found: ${files}"
                        sh "cat ${files}"
                    } else {
                        echo "No txt files found"
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline finished successfully"
        }
    }
}