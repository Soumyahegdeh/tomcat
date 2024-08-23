pipeline {
  agent {
    docker {
       image 'abhishekf5/maven-abhishek-docker-agent:v1'
       args '--user root -v /var/run/docker.sock:/var/run/docker.sock' // mount Docker socket to access the host's Docker daemon
    }
  }
  stages {
    stage('Checkout') {
      steps {
        sh 'echo passed'
        git branch: 'master', url: 'https://github.com/Soumyahegdeh/tomcat.git'
      }
    }
    stage('Build and Test') {
      steps {
        sh 'ls -ltr'
        sh 'mvn clean package'
        archiveArtifacts artifacts: 'target/*.war', followSymlinks: false, onlyIfSuccessful: true
        echo "build and test done"
      }
    }
    stage('Code Deployment'){
      steps{
        deploy adapters: [tomcat9(credentialsId: 'TomcatCreds', path: '', url: 'http://18.199.98.239/:8080/')], contextPath: 'myapp', onFailure: false, war: 'target/*.war'
       }
		
   }
     
   }
  
}
