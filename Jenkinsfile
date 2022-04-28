pipeline{
   agent { docker { image 'maven:3.6.3'} }
   environment{
      dockerHome = tool 'myDocker'
      mavenHome = tool 'myMaven'
      PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
   }
// { docker { image 'maven:3.6.3'} }
   tools { 
      maven 'myMaven' 
         }
     stages {	
          stage('Checkout') {
  	    steps {
              sh  'mvn --version'
              sh  'docker version'
	      echo "Build"
              echo "PATH - $PATH"
	      echo "BUILD_NUMBER - $env.BUILD_NUMBER"
	      echo "BUILD_ID - $env.BUILD_ID"
              echo "JOB_NAME - $env.JOB_NAME"
              echo "BUILD_TAG - $env.BUILD_TAG"
              echo "BUILD_URL - $env.BUILD_URL"
	}
       }
	 stage ('Compile') {
	   steps {
	    echo 'mvn clean compile'
          }
         }
          stage('Test') {
            steps {
             echo 'mvn test'
        }
       }
          stage('Integration Test') {
            steps {
              echo  'mvn failsafe:integration-test failsafe:verify'   
       }	
      }	
 	 stage ('Build Docker Image') {
	   steps {
      	   // docker build -t mehtachirag186/currency-exchange-devops:$env.BUILD.TAG  
	      script{
 		  dockerImage = docker.build("mehtachirag186/currency-exchange-devops:${$env.BUILD.TAG}")
		}
            }
       }
      	stage ('Build Docker Image') {
           steps {
	      script {
		  docker.withRegistry('', 'dockerhub') {
                  dockerImage.push();
		  dockerImage.push('latest');
	      }	
	   }
       }
      }

     } 
      post {
	  always{
	      echo 'I am awesome. I run always'
          }
          success{
              echo 'I run when you are succesful'
          }
          failure{
              echo 'I run when you fail'
          }
     }
  
}
