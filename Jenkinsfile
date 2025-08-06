pipeline{
  agent {
   docker { image 'node:18'
            args '-e npm_config_cache=./.npm'
          }
    
   }


stages {
    stage('Install Dependencies') {
        steps {
            // Installs dependencies, same as before
            sh 'npm install'
        }
    }

    stage('Build Image') { // This is your build stage
        steps {
            // Builds the Docker image from your Dockerfile
            sh 'docker build -t my-todolist-app .'
        }
    }

    stage('Deploy') { // This is your new deploy stage
        steps {
            sh '''
                # Stop any container running with the same name, if it exists
                docker stop my-todolist-container || true

                # Remove the stopped container, if it exists
                docker rm my-todolist-container || true

                # Run the new Docker image as a container
                # Maps port 8080 on the Jenkins server to port 8000 inside the container
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

        
    
