pipeline {
    agent any

    environment {
        SONAR_SCANNER_HOME = tool name: 'SonarScanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
    }

    stages {
        stage("Clone") {
            steps {
                git url: "https://github.com/Abrar944/Python-Jenkins-CICD.git", branch: "main"
            }
        }

        stage("SonarQube Analysis") {
            steps {
                echo "Running SonarQube Analysis"
                withSonarQubeEnv('MySonar') {
                    sh "${SONAR_SCANNER_HOME}/bin/sonar-scanner"
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
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
