pipeline {
    agent any
    stages {
        stage("Build & Run") {
            steps {
                sh '''
                    # Збираємо образ локально на сервері
                    docker build -t mihajlo1357/site:latest .
                    
                    # Зупиняємо старий контейнер, якщо він був
                    docker stop site || true
                    docker rm site || true
                    
                    # Запускаємо на порту 8085 (щоб не було конфліктів)
                    docker run -d --name site -p 8085:80 mihajlo1357/site:latest
                    
                    # Перевіряємо, чи він з'явився у списку запущених
                    docker ps | grep site
                '''
            }
        }
    }
}
