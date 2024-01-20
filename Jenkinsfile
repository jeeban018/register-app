pipeline {
    agent { label 'Jenkins-Agent' }
    tools {
        jdk 'Java17'
        maven 'Maven3'
    }
   
    stages{
        stage("Cleanup Workspace"){
                steps {
                cleanWs()
                }
        }

        stage("Checkout from SCM"){
                steps {
                     git branch: 'main', credentialsId: 'github', url: 'https://github.com/jeeban018/register-app.git'
                }
        }
	    
        stage("Build Application"){
            steps {
                sh "mvn clean package"
            }

       }
	    stage("Test Application"){
                steps {
                    sh "mvn test"
		   }
	       }

	    stage("Sonar Analysis"){
		    steps{
		       scripts{
			   withSonarQubeEnv('sonaqube-server'){
			   sh "mvn sonar:sonar		    
			   } 
   
		       }	    
		    }
	    }
           }
       }
