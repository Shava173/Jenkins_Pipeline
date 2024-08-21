pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Shava173/Jenkins_Pipeline.git'
            }
        }
        stage('Build') {
            steps {
                dir('my-app') {  // Зміна для виконання команди всередині директорії my-app
                    sh 'mvn clean package'
                }
            }
        }
        stage('Test') {
            steps {
                dir('my-app') {  // Зміна для виконання команди всередині директорії my-app
                    sh 'mvn test'
                }
            }
            post {
                always {
                    dir('my-app') {  // Зміна для того, щоб Jenkins шукав звіти тестування всередині my-app
                        junit 'target/surefire-reports/*.xml'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying to server...'
                // Додайте команди для деплою, якщо необхідно
            }
        }
    }
    post {
        success {
            echo 'Build and tests completed successfully!'
        }
        failure {
            echo 'Build or tests failed!'
        }
    }
}
