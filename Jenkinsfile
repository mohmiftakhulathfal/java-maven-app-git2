pipeline {
    agent any

    tools {
        maven 'maven-3.9.1'
    }

    stages {
        stage('Build jar') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Build image') {
            steps {
                script {
                    echo "Building the Docker image..."
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-credential', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh 'docker build -t azenhion21/demo-app:1.0 .'
                        sh 'echo $PASS | docker login -u $USER --password-stdin'
                        sh 'docker push azenhion21/demo-app:1.0'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo "Deploying the application..."
                }
            }
        }
    }
}
