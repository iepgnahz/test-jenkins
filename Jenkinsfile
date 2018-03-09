pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID     = '123456'
        AWS_SECRET_ACCESS_KEY = '211111'
    }

    stages {
        stage('build') {
            steps {
                echo AWS_ACCESS_KEY_ID
                sh './gradlew --version'
            }
        }

        stage('deploy') {
            when {
                expression {
                    currentBuild.result == null || currentBuild.result == 'SUCCESS'
                }
            }

            steps {
                echo currentBuild.result
                input "Does the build look ok?"
            }
        }

    }

    post {
        always {
            echo 'This will always run'
            deleteDir()
        }

        success {
            echo 'This will run only if successful'
        }

        failure {
            echo 'This will run only if failed'
        }

        unstable {
            echo 'This will run only if the run was marked as unstable'
        }

        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}