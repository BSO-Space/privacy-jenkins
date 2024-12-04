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
                expression { "${env.PIPELINE_TYPE}" == 'develop' }
            }
            steps {
                echo 'Testing.. ${env.PIPELINE_TYPE}'
            }
        }
        stage('Deploy') {
            when {
                expression { "${env.PIPELINE_TYPE}" == 'main'}
            }
            steps {
                echo 'Deploying.... ${env.PIPELINE_TYPE}'
            }
        }
    }
     post {
        always {
            echo "Cleaning up workspace..."
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
