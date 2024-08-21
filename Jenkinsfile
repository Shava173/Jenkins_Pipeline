pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Виконуємо перевірку версій з SCM (Git)
                git url: 'https://github.com/Shava173/Jenkins_Pipeline.git', branch: 'main'
            }
        }

        // Додавання етапу перевірки файлів
        stage('Verify Files') {
            steps {
                echo 'Перевіряємо наявність файлів у робочій директорії Jenkins:'
                sh 'ls -la'
                echo 'Перевіряємо наявність файлів у директорії my-app:'
                sh 'ls -la my-app/'
            }
        }

        // Додавання етапу перевірки наявності Maven
        stage('Check Maven') {
            steps {
                sh 'mvn --version'  // Перевірка наявності Maven та його версії
            }
        }

        stage('Build') {
            steps {
                dir('my-app') {
                    sh 'mvn clean package -X'  // Виконання Maven з деталізованим виводом
                }
            }
        }

        stage('Test') {
            steps {
                dir('my-app') {
                    sh 'mvn test'
                }
            }
            post {
                always {
                    dir('my-app') {
                        junit '**/target/surefire-reports/*.xml'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                // Додайте тут команди для деплою вашого застосунку
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
