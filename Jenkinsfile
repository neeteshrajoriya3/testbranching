pipeline {
    agent any

    environment {
        ALL_EMAILS = 'neet.kumar3@gmail.com,mehul.raj233@gmail.com'
    }

    stages {
        stage('Sanity Check') {
            steps {
                echo '✅ Jenkinsfile from GitHub is executing'
            }
        }
    }

    post {
        always {
            mail to: "${ALL_EMAILS}",
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
