pipeline {
    agent any

    stages {
        stage('Cleanup') {
            steps {
                echo '🧹 Видаляємо старі контейнери...'
                // Видаляємо старий контейнер, якщо він є. '|| true' не дасть білду впасти, якщо контейнера нема.
                sh 'docker rm -f site-worker || true'
            }
        }

        stage('Build Image') {
            steps {
                echo '🔨 Збірка образу...'
                // Збираємо образ локально на хості
                sh 'docker build -t my-jenkins-site:latest .'
            }
        }

        stage('Run Site') {
            steps {
                echo '🚀 Запуск сайту...'
                // Запускаємо на порту 8085 (або будь-якому іншому вільному)
                sh 'docker run -d --name site-worker -p 8085:80 my-jenkins-site:latest'
                
                echo '✅ Перевірка чи піднявся процес:'
                sh 'docker ps | grep site-worker'
            }
        }
    }
}
