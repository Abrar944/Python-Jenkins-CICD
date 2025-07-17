pipeline {
    agent any

    environment {
        // Optional: Add DOCKER_HOST if needed
    }

    stages {
        stage("Clone") {
            steps {
                echo "Cloning Stage"
                git url: "https://github.com/Abrar944/Python-Jenkins-CICD.git", branch: "main"
            }
        }

        stage("SonarQube Analysis") {
            steps {
                echo "Running SonarQube Analysis"
                withSonarQubeEnv('MySonar') {
                    sh "sonar-scanner"
                }
            }
        }

        stage("Build Docker Image") {
            steps {
                echo "Building Docker Image"
                sh "docker build -t ahmedbhai/todoapp ."
            }
        }

        stage("Deploy with Docker Compose") {
            steps {
                echo "Deploying Application"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
