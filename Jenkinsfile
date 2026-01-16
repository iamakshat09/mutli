pipeline {
    agent none   // we will decide agent dynamically

    stages {

        stage('Checkout') {
            agent any
            steps {
                checkout scm
                echo "Checked out branch: ${env.BRANCH_NAME}"
            }
        }

        stage('Build') {
            agent {
                label getAgent()
            }
            steps {
                echo "Building application for ${env.BRANCH_NAME}"
                sh '''
                  echo "Simulating build..."
                  sleep 5
                '''
            }
        }

        stage('Deploy') {
            agent {
                label getAgent()
            }
            steps {
                echo "Deploying to ${getEnvironment()} environment"
                sh '''
                  echo "Deploying application..."
                  sleep 5
                '''
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully for ${env.BRANCH_NAME}"
        }
        failure {
            echo "Pipeline failed for ${env.BRANCH_NAME}"
        }
    }
}

/* ---------- Helper Functions ---------- */

def getAgent() {
    if (env.BRANCH_NAME == 'dev') {
        return 'dev'
    } else if (env.BRANCH_NAME == 'qa') {
        return 'qa'
    } else if (env.BRANCH_NAME == 'main') {
        return 'prod'
    } else {
        error "No agent configured for branch: ${env.BRANCH_NAME}"
    }
}

def getEnvironment() {
    if (env.BRANCH_NAME == 'dev') {
        return 'Development'
    } else if (env.BRANCH_NAME == 'qa') {
        return 'QA'
    } else if (env.BRANCH_NAME == 'main') {
        return 'Production'
    }
}
