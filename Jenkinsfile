pipeline{
  agent {
   docker { image 'node:18'
            args '-e npm_config_cache=./.npm'
          }
    
   }

  stages{
    stage('Checkout'){
        steps{
           git branch:'main',
                url: 'https://github.com/rana7862/jenkins-CICD.git'
           }
      }
    stage('Install Dependencies') {
       steps {
          sh 'npm install'
         }
      }
     stage('Test') {
        steps {
           sh 'npm run test'
      }
      }
     stage('Package with docker'){
       steps {
          sh 'docker build -t my-node-app .'
            }
       }
    }

post { 
   always {
       echo 'Pipeline completed!'
    }
  }
}

        
    
