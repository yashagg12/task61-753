pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'yashagg00001@gmail.com' // Change to your email
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Run the Python application (or any build command you have)
                sh 'python app.py' // Adjust as needed
            }
        }
        stage('Notify') {
            steps {
                script {
                    emailext(
                        to: EMAIL_RECIPIENT,
                        subject: "Build ${currentBuild.fullDisplayName}",
                        body: "Build status: ${currentBuild.currentResult}\n\nCheck the build ${env.BUILD_URL} for more details.",
                        attachLog: true // Attach the build log
                    )
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline finished with status: ${currentBuild.currentResult}"
        }
    }
}
