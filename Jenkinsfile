pipeline{
   agent any  
// { docker { image 'maven:3.6.3'} }
   tools { 
      maven 'MAVEN_HOME' 
      jdk 'JAVA_HOME' 
    }
     stages {	
          stage('Build') {
  	    steps {
              sh  'mvn --version'
	      echo "Build"
	}
       }
          stage('Test') {
            steps {
              echo "Test"
        }
       }
          stage('Integration Test') {
            steps {
              echo "Integration Test"   
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
