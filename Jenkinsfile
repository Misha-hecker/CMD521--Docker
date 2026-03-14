#!groovy

pipeline {
    agent any

    stages {
        stage("Create Site image") {
            steps {
                echo '🧱 Building Site image ...'
                sh "docker build --no-cache -t mihajlo1357/site ."
            }
        }

        stage("Deploy Site on remote server") {
            steps {
                echo "🌐 Deploying Site container on remote server ..."
                sh '''
                    echo "🧹 Cleaning up old Site container and image..."
                    docker stop site || true
                    docker rm site || true

                    echo "🚀 Starting new Site container..."
                    docker run -d --name site --restart=always -p 0.0.0.0:80:80   macnaer/site
                '''
            }
        }
    }
}
