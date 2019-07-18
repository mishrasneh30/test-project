pipeline {
    agent { label 'master' }
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
                        synopsys_detect '--detect.project.name="DeclarativePipelineNew"'
                        //String args ="--blackduck.url='https://qa-hub37.dc1.lan' --blackduck.username=sysadmin --blackduck.password=blackduck --blackduck.trust.cert=true --detect.project.name=Mattersight" synopsys_detect args 
                    }
            }
            
        }    
        
    }
}