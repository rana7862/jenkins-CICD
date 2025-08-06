pipeline{
  agent any 

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
     stage('Build') {
        steps {
           sh 'npm run build'
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

        
    
