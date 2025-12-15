pipeline {
    agent any

    environment {
        ALL_EMAILS = 'neet.kumar3@gmail.com,mehul.raj233@gmail.com'
    }

    stages {

        stage('Show Files') {
            steps {
                echo 'Listing workspace files'
                bat '''
                echo ===== Workspace Content =====
                dir
                '''
            }
        }

        stage('Read TXT Files') {
            steps {
                script {
                    def files = bat(
                        script: 'dir /b *.txt 2>nul',
                        returnStdout: true
                    ).trim()

                    if (files) {
                        echo "TXT files found:"
                        echo files
                        bat """
                        for %%f in (${files}) do (
                            echo ===== %%f =====
                            type %%f
                        )
                        """
                    } else {
                        echo 'No TXT files found'
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Sending email notification'

            mail to: env.ALL_EMAILS,
                 subject: "BUILD ${currentBuild.currentResult}: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: """\
Job Name   : ${env.JOB_NAME}
Build No  : ${env.BUILD_NUMBER}
Status    : ${currentBuild.currentResult}
Build URL : ${env.BUILD_URL}
"""
        }
    }
}
