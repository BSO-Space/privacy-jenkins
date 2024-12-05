pipeline {
    agent any

    parameters {
        string(name: 'BRANCH', defaultValue: 'main', description: 'Branch to build')
        choice(name: 'PIPELINE_TYPE', choices: ['main', 'develop', 'release'], description: 'Type of pipeline to execute')
    }

    environment {
        PROJECT_NAME = "private-jenkins"
        ARTIFACTS_DIR = "artifacts"
    }

    stages {
        stage('Build') {
            steps {
                echo "Building.... ${env.PIPELINE_TYPE}"
            }
        }

        stage('Test') {
            when {
                branch 'develop'
            }
            steps {
                echo "Testing.. ${env.BRANCH_NAME}"
            }
        }
        
        stage('Deploy') {
            when {
                anyOf {
                    branch 'main'
                    branch 'release'
                }
            }
            steps {
                echo "Deploying.... ${env.BRANCH_NAME}"
            }
        }
    }

     post {
        always {
            echo "Cleaning up workspace... ${env.BRANCH_NAME}"
            cleanWs()
        }
        success {
            echo "Pipeline succeeded!"
        }
        failure {
            echo "Pipeline failed."
        }
        unstable {
            echo "Pipeline is unstable."
        }
    }
}
