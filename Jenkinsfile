pipeline {
    agent any

    environment{
	ALL_EMAILS='neetesh.rajoriya3@gmail.com,neetesh.rajoriya3@gmail.com'
    }

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
            mail to: "$(ALL_EMAILS)",
                 subject:"BUILD ${currentBuild.currentResult}: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
	    body: """\
Job Name   : ${env.JOB_NAME}
Build No  : ${env.BUILD_NUMBER}
Status    : ${currentBuild.currentResult}
Build URL : ${env.BUILD_URL}
        }
    }
}