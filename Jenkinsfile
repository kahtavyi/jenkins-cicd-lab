pipeline {
    agent any

    tools {
        // Тут ми вказуємо назву інструменту, яку ти задав у налаштуваннях ('node')
        nodejs 'node'
    }

    stages {
        stage('Install') {
            steps {
                echo 'Installing dependencies...'
                // Команда для встановлення бібліотек
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                // Запуск тестів (вони є в проекті)
                sh 'npm test'
            }
        }
    }
}
