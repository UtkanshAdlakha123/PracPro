pipeline{
     agent any
     
     stages{
          stage('Code'){
              steps{
                 git url: 'https://github.com/UtkanshAdlakha123/PracPro.git', branch: 'master'
                 echo 'cloning the code'
             }
         }
         
	  stage('Build'){
              steps{
                     sh 'docker build -t adlakhautkansh22/websiteimg .'
                     //sh 'docker run --name utkansh123 -p 8084:80 adlakhautkansh22/websiteimg'
             }
         }
          
	  stage('Push'){
             steps{
                 script{
                     withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKERHUB_TOKEN')]) {
                         
			def dockerhubToken = env.DOCKERHUB_TOKEN
                        // Login to Docker Hub using the access token
                        sh "echo ${dockerhubToken} | docker login -u adlakhautkansh22 --password-stdin"
                        // Build and push your Docker image 
                        sh "docker push adlakhautkansh22/websiteimg"
                     }
                 }
              }
         }
          
	  stage('Deploy'){
             steps{
                     sh 'docker-compose down'
		     sh 'docker-compose up -d --no-deps --build web'
             }
         }
     }
 }
