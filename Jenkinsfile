pipeline {
    agent any

    stages {
        stage('---------------- Checkout -------------') {
            steps {
                git url: 'https://github.com/SERMSN/sdvps-materials.git', branch: 'main'
            }
        }
        
        stage('----------- Test Go ----------') {
            steps {
                sh 'go test .'
            }
        }

        stage('---------- Build Docker Image -------------') {
            steps {
                script {
                    docker.build("sdvps-app:${env.BUILD_ID}")
                }
            }
        }
    }

    post {
        success {
            echo '----------- Build and tests completed successfully! --------------'
            sh 'docker images'
        }
        failure {
            echo '------- Build or tests failed! ---------------'
        }
    }
}
