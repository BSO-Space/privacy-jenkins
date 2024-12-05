    pipeline {
        agent any

       
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
