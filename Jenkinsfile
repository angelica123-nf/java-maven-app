pipeline{
  agent any

  tools{
    maven 'maven-3.9'

  stages{
    stage('Build jar'){
      steps{
        sh 'mvn package'
      }
    }
    
    stage('Build Image'){
      steps{
        script {
          echo "Building the Docker image..."
          withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usenameVariable: 'USER')]){
            sh 'docker build -t sitiberkah25/demo-app:jma-2.0 .'
            sh "echo \$PASS | docker login -u \$USER --password-stdin"
            sh 'docker push sitiberkah25/demo-app:jma-2.0'
          }
        }
      }
    }
    
    stage('Deploy'){
      steps{
        echo 'Deploying the application...'
      }
    }
  }
}
}
