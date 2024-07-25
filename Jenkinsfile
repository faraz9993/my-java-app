pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/faraz9993/my-java-app.git', branch: env.CHANGE_BRANCH
            }
        }

        stage('Build') {
            steps {
                script {
                    echo "Building pull request branch: ${env.CHANGE_BRANCH}"
                    withMaven(maven: 'Maven-3.9.0') {
                        sh 'mvn clean package'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo "Running tests on pull request branch: ${env.CHANGE_BRANCH}"
                    withMaven(maven: 'Maven-3.9.0') {
                        sh 'mvn test'
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Pipeline succeeded.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
