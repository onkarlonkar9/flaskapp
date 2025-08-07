pipeline {
    agent any
    stages {
        stage("Code Clone") {
            steps {
                git url: "https://github.com/onkarlonkar9/flaskapp.git", branch: "master"
            }
        }

        stage("Build") {
            steps {
                sh "docker build -t my-app ."
            }
        }

        stage("Test") {
            steps {
                echo "Developer will test the application"
            }
        }

        stage("Push to DockerHub") {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerHubCreds',
                    passwordVariable: 'PASS',
                    usernameVariable: 'USERNAME'
                )]) {
                    sh "docker login -u $USERNAME -p $PASS"
                    sh "docker tag my-app $USERNAME/my-app:latest"
                    sh "docker push $USERNAME/my-app:latest"
                }
            }
        }

        stage("Deploy") {
            steps {
                sh "docker compose up -d"
            }
        }
    }
}
