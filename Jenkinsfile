pipeline {
    // We will define the agent for each stage individually
    agent none

    stages {
        stage('Install Dependencies') {
            // Use the node:18 Docker container ONLY for this stage
            agent {
                docker {
                    image 'node:18'
                    args '-e npm_config_cache=./.npm'
                }
            }
            steps {
                sh 'npm install'
            }
        }

        stage('Build Image') {
            // Use any available Jenkins agent that has Docker installed (the host)
            agent any
            steps {
                sh 'docker build -t my-todolist-app .'
            }
        }

        stage('Deploy') {
            // Also run this stage on the host agent
            agent any
            steps {
                sh '''
                    docker stop my-todolist-container || true
                    docker rm my-todolist-container || true
                    docker run --name my-todolist-container -d -p 8080:8000 my-todolist-app
                '''
            }
        }
    }
    post {
        always {
            echo 'Pipeline completed!'
        }
    }
}
        
    
