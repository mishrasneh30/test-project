pipeline {
    agent { dockerfile true }
    stages {
        stage('Build') {
            steps('Build Steps'){
                    git 'https://github.com/madhusudhan481/test-project.git'
                
                    script{
                        def mvn_version = 'maven3'
                        sh 'echo mvn_version'
                        withEnv( ["PATH+MAVEN=${tool mvn_version}/bin"] ) 
                		{
                			 sh "mvn clean install"
                		}
                    }
                }
              
        }
        stage('Post Build') {
            steps('Synopsys Detect'){
                
                script{
                        synopsys_detect '--detect.project.name="DeclarativeWithDocker1"'
                         
                    }
            }
            
        }    
        
    }
}