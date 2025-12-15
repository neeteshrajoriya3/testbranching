pipeline {
    agent any

    environment {
        ALL_EMAILS = 'neetesh.rajoriya3@gmail.com,neetesh.rajoriya2@gmail.com'
    }

    stages {

        stage('Checkout Source') {
            steps {
                checkout scm
            }
        }

        stage('Show Workspace Files') {
            steps {
                echo '===== Listing workspace files ====='
                bat '''
                dir
                '''
            }
        }

        stage('Read TXT Files') {
            steps {
                echo '===== Reading TXT files ====='
                bat '''
                if exist *.txt (
                    for %%f in (*.txt) do (
                        echo.
                        echo ===== %%f =====
                        type %%f
                    )
                ) else (
                    echo No TXT files found in workspace
                )
                '''
            }
        }
    }

    post {
        always {
            echo 'Sending email notification'

            mail(
                to: env.ALL_EMAILS,
                subject: "BUILD ${currentBuild.currentResult}: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
Job Name   : ${env.JOB_NAME}
Build No  : ${env.BUILD_NUMBER}
Status    : ${currentBuild.currentResult}
Build URL : ${env.BUILD_URL}

This email was sent regardless of build result.
"""
            )
        }
    }
}