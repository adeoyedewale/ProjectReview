pipeline {
    agent any
  
     //create dockerhub credential in github with your dockerhub Username and Password/Token
    environment {
      DOCKERHUB_CREDENTIALS=credentials('dockerhub')
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/adeoyedewale/ProjectReview.git'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Dockerize') {
            steps {
                sh "docker build -t eruobodo/frontend_app:${BUILD_NUMBER} ."
            }
        }
        //stage('Publish') {
        //    steps {
         //       sh "docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD"
         //       sh "docker tag your-nodejs-app $DOCKER_USERNAME/your-nodejs-app:$BUILD_NUMBER"
         //       sh "docker push $DOCKER_USERNAME/your-nodejs-app:$BUILD_NUMBER"
            //}
        stage('Login') {
		
              steps {
                 sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login --username eruobodo --password-stdin'    
              }
		    }

        stage('Push') {

              steps {
                 sh 'docker push eruobodo/frontend_app:${BUILD_NUMBER}'
              }
        }
		}
	
    post {
        always {
      sh 'docker logout'
        }
   }
}
