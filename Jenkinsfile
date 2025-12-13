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
        always {
            emailext(
                to: 'anyone@example.com',   // any address; Mailtrap will capture it
                subject: "Build ${currentBuild.currentResult}: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """Build result: ${currentBuild.currentResult}
Job: ${env.JOB_NAME}
URL: ${env.BUILD_URL}"""
            )
        }
    }
}