pipeline {
    agent any

    stages {
        stage('Proof') {
            steps {
                echo '🔥 Jenkinsfile is executing correctly 🔥'
            }
        }
    }

    post {
        always {
            echo "Build completed with status: ${currentBuild.currentResult}"
        }
    }
}
