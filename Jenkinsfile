pipeline {
    agent { dockerfile true }
	environment {
       /* Known issue that this is needed for Alpine, we can't use the java bundled with the Signature Scanner so we have to use the Alpine java home */
       BDS_JAVA_HOME="/usr/lib/jvm/java-1.8-openjdk"
	}
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
