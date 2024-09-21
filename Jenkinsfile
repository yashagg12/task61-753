pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'yashagg00001@gmail.com' // Change to your email
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                // Assuming you're just running the Python file directly, adjust as needed
                sh 'python app.py' // Replace with your build command if needed
            }
        }
        stage('Unit Tests') {
            steps {
                echo 'Running unit tests...'
                // Assuming you have tests defined, otherwise this can be omitted
                sh 'pytest' // If using pytest, make sure it's installed
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
