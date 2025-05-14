pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-cicd-app"
        CONTAINER_NAME = "my-cicd-container"
        PORT_HOST = "8080"
        PORT_CONTAINER = "80"
    }

    stages {
        stage('Clone Repo') {
            steps {
                echo 'Cloning the repo...'
                // Sudah otomatis oleh Declarative Checkout SCM
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $IMAGE_NAME ."
            }
        }

        stage('Stop and Remove Old Container') {
            steps {
                sh """
                if [ \$(docker ps -a -q -f name=$CONTAINER_NAME) ]; then
                    echo "Stopping existing container..."
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                fi
                """
            }
        }

        stage('Run Docker Container') {
            steps {
                sh "docker run -d -p $PORT_HOST:$PORT_CONTAINER --name $CONTAINER_NAME $IMAGE_NAME"
            }
        }
    }
}
