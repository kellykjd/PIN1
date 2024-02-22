pipeline {
  agent any

  options {
    timeout(time: 2, unit: 'MINUTES')
  }

  environment {
    ARTIFACT_ID = "elbuo8/webapp:${env.BUILD_NUMBER}"
  }
   stages {
   stage('Building image') {
      steps{
          sh '''
          docker build -t testapp .
             '''  
        }
    }
  
  
    stage('Run tests') {
      steps {
        sh "docker run testapp npm test"
      }
    }
   stage('Deploy Image') {
      steps{
        sshagent(credentials: ['REGISTRY_CREDENTIALS']) {
         sh '''
          docker tag testapp kellykjd/testapp:latest
          docker push kellykjd/testapp:latest
        ''' 
        }
        }
      }
    }
}


    
  

