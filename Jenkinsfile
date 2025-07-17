pipeline {
    agent any
    tools {
        sonarQube 'SonarScanner'
    }
    stages {
        stage("clone") {
            steps {
                echo "Cloning Stage"
                git url: "https://github.com/Abrar944/Python-Jenkins-CICD.git", branch: "main"
            }
        }

        stage("sonarqube-analysis") {
            steps {
                echo "Running SonarQube Analysis"
                withSonarQubeEnv('MySonar') {
                    sh "sonar-scanner"
                }
            }
        }

        stage("build") {
            steps {
                echo "Building image Stage"
                sh "docker build -t ahmedbhai/todoapp ."
            }
        }

        stage("deploy") {
            steps {
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
