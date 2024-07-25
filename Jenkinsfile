pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/faraz9993/my-java-app.git', branch: env.BRANCH_NAME
            }
        }

        stage('Build') {
            steps {
                script {
                    echo "Building production branch: ${env.BRANCH_NAME}"
                    withMaven(maven: 'Maven-3.9.0') {
                        sh 'mvn clean package'
                    }
                }
            }
        }

        stage('Run') {
            steps {
                script {
                    echo "Running Java application"
                    sh 'java -cp target/my-java-app-1.0-SNAPSHOT.jar com.example.App'
                }
            }
        }

        stage('Deploy') {
            when {
                branch 'feature-branch-1'
            }
            steps {
                script {
                    echo "Deploying to production from branch: ${env.BRANCH_NAME}"
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

