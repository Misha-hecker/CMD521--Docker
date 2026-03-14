pipeline {
    agent any
    stages {
        stage('Deploy to Host') {
            steps {
                sh '''
                    # Збираємо образ прямо на хості
                    docker -H unix:///var/run/docker.sock build -t mihajlo1357/site:latest .
                    
                    # Видаляємо старий контейнер на хості
                    docker -H unix:///var/run/docker.sock rm -f site-worker || true
                    
                    # Запускаємо на хості (порт 8085)
                    docker -H unix:///var/run/docker.sock run -d --name site-worker -p 8085:80 mihajlo1357/site:latest
                    
                    # Перевіряємо запуск на хості
                    docker -H unix:///var/run/docker.sock ps | grep site-worker
                '''
            }
        }
    }
}
