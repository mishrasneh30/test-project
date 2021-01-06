pipeline {
    agent { label 'master' }
    stages {
        stage('Build') {
            steps('Build Steps'){
                    git 'https://github.com/mishrasneh30/test-repo2.git'
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
                        synopsys_detect '--detect.project.name="Declarative_Pipeline_SCM"'
                        
                    }
            }
            
        }    
        
    }
}
