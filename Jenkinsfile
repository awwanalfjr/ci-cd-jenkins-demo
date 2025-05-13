pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                echo 'Cloning the repo...'
                // Ini otomatis dilakukan Jenkins pas pakai Git SCM, jadi bisa di-skip juga
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-cicd-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 8080:80 --name my-cicd-container my-cicd-app'
            }
        }
    }
}
 
