pipeline {
    agent any
    environment {
        DIRECTORY_PATH = "/Users/teclaire/.jenkins/workspace/my_first_pipeline"
        TESTING_ENVIRONMENT = "test-env"
        PRODUCTION_ENVIRONMENT = "my_first_pipeline"
        RECIPIENT_EMAIL = 'recipient@example.com' // Replace with the actual email address
    }
    stages {
        stage('Build') {
            steps {
                echo "Fetching the source code from the directory path: ${env.DIRECTORY_PATH}"
                echo "Compiling the code and generating artifacts"
            }
        }
        stage('Test') {
            steps {
                echo "Running unit tests"
                echo "Running integration tests"
            }
        }
        stage('Code Quality Check') {
            steps {
                echo "Check the quality of the code"
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploy the application to a testing environment: ${env.TESTING_ENVIRONMENT}"
            }
        }
        stage('Approval') {
            steps {
                script {
                    echo "Waiting 10 seconds for approval..."
                }
                sleep time: 10, unit: 'SECONDS'
            }
        }
        stage('Deploy to production') {
            steps {
                echo "Deploy the code to the production environment: ${env.PRODUCTION_ENVIRONMENT}"
            }
            post {
                always {
                    script {
                        emailext subject: "Pipeline ${currentBuild.result}: ${env.JOB_NAME}",
                                  body: "Pipeline ${currentBuild.result}: ${env.BUILD_URL}",
                                  to: env.RECIPIENT_EMAIL, // Use variable
                                  attachmentsPattern: '**/build.log'
                    }
                }
            }
        }
    }
}
