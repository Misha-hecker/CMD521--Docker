pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Вказуємо твій форк
                git 'https://github.com/Misha-hecker/CMD521--Docker.git'
            }
        }

        stage("Create Site image") {
            steps {
                echo '🧱 Building Site image ...'
                // Збираємо образ локально
                sh "docker build --no-cache -t mihajlo1357/site ."
            }
        }

        stage("Deploy Site locally") {
            steps {
                echo "🌐 Deploying Site container on this server ..."
                sh '''
                    echo "🧹 Cleaning up old containers..."
                    docker stop site || true
                    docker rm site || true

                    echo "🚀 Starting new Site container..."
                    # Запускаємо на порту 8081, щоб не "битися" з самим Jenkins (8080)
                    docker run -d --name site --restart=always -p 8081:80 mihajlo1357/site
                '''
            }
        }
    }
    
    post {
        success {
            echo '✅ Все працює! Перевіряй http://IP_СЕРВЕРА:8081'
        }
    }
}
