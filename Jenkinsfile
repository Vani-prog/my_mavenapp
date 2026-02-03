pipeline {
      agent any

     triggers{
	   cron("* * * * *")
     }
  
     environment {
	     DOCKERHUB_CRED = credentials('dockerhub')
	     IMAGE_NAME = "vanireddy2025/my_mavenapp"
     }
	
     stages {
	  stage('checkout'){
	     steps{
                 script{
		      git url: "https://github.com/Vani-prog/my_mavenapp.git",
		      branch: 'main'
		}
	    }
	 }

	stage('Build With Maven'){
	    steps{
		script{
		     sh 'mvn clean package -DskipTests'
		}
	    }
        }

	stage('Build with docker'){
	    steps{
		script{
		     dockerImage=docker.build("${IMAGE_NAME}:latest")
		}
	    }
        }

	stage('Push'){
	    steps{
		script{
		     docker.withRegistry("https://index.docker.io/v1/', 'dockerhub'){
		     dockerImage.push()
								 }
		}
            }
        }
     }
}
