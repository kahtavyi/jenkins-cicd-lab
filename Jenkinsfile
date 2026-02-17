pipeline {
    agent any

    tools {
        nodejs 'node'
    }

    stages {
        stage('Install') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Перевіряємо, яка це гілка, і даємо різні імена образам
                    if (env.BRANCH_NAME == 'main') {
                        echo 'Building for MAIN...'
                        sh 'docker build -t nodemain:v1.0 .'
                    } else if (env.BRANCH_NAME == 'dev') {
                        echo 'Building for DEV...'
                        sh 'docker build -t nodedev:v1.0 .'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Логіка запуску: зупиняємо старий контейнер і запускаємо новий на потрібному порту
                    if (env.BRANCH_NAME == 'main') {
                        echo 'Deploying MAIN on port 3000...'
                        sh 'docker rm -f node-app-main || true' // Видаляємо старий, якщо є
                        sh 'docker run -d -p 3000:3000 --name node-app-main nodemain:v1.0'
                    } else if (env.BRANCH_NAME == 'dev') {
                        echo 'Deploying DEV on port 3001...'
                        sh 'docker rm -f node-app-dev || true'
                        sh 'docker run -d -p 3001:3000 --name node-app-dev nodedev:v1.0'
                    }
                }
            }
        }
    }
}
