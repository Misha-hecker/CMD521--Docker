pipeline {
    // ЗМІНИ ТУТ: замість 'any' пишемо лейбл твого агента
    agent { label 'docker-node' } 

    stages {
        stage('Checkout') {
            steps {
                echo '🚚 Клонування репозиторію...'
                git 'https://github.com/Misha-hecker/CMD521--Docker.git'
            }
        }

        stage("Create Site image") {
            steps {
                echo '🧱 Building Site image on Agent...'
                // Додаємо --no-cache, щоб образ завжди оновлювався
                sh "docker build --no-cache -t mihajlo1357/site ."
            }
        }

        stage("Deploy Site on Agent") {
            steps {
                echo "🌐 Deploying Site container on remote agent..."
                sh '''
                    echo "🧹 Cleaning up old containers..."
                    docker stop site || true
                    docker rm site || true

                    echo "🚀 Starting new Site container..."
                    # Запускаємо на порті 8081 (або 80, якщо він вільний на агенті)
                    docker run -d --name site --restart=always -p 8081:80 mihajlo1357/site
                '''
            }
        }
    }
    
    post {
        success {
            echo '✅ Успіх! Сайт запущено на віддаленому агенті.'
        }
        failure {
            echo '❌ Помилка! Перевір Console Output.'
        }
    }
}
