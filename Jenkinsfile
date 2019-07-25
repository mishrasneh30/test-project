pipeline {
    agent { dockerfile true }
    stages {
        stage('Git'){
           
			steps{
               
               git 'https://github.com/madhusudhan481/test-project'
			}
		}
       
		stage('Maven'){
			steps{
                sh "mvn clean install"
                }
		}
       
       stage('BD in Post Build') {
           steps {
                synopsys_detect '--detect.project.name="DockerFileInDeclarativePipeline1" --detect.tools.excluded=DETECTOR'
               
           }
       }   
        
    }
}
