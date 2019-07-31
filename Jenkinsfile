pipeline {
    agent {
        kubernetes {
            label "mypod-${UUID.randomUUID().toString()}"
              
                defaultContainer 'jnlp'
                containerTemplate {
                    name 'mavenapline'
                    image 'maven:3.6.0-jdk-8-alpine'
                    ttyEnabled true
                    command 'cat'
                    privileged true
                    alwaysPullImage false
                    resourceRequestCpu '50m'
                    resourceRequestMemory '128Mi'
                }
        }
    }
    environment {
       /* Known issue that this is needed for Alpine, we can't use the java bundled with the Signature Scanner so we have to use the Alpine java home */
       BDS_JAVA_HOME="/usr/lib/jvm/java-1.8-openjdk"
    } 
   
   stages{
        stage('Git'){
            steps{
                container('mavenapline'){
                    sh 'apk add git'
                    git 'https://github.com/FasterXML/jackson-core.git'
                }
            }
        }
        stage('Maven'){
            steps{
                container('mavenapline'){
                    sh "mvn clean install"
                }
            }
        }
        stage('BD Post Build'){
            steps('Synopsys Detect'){
                container('mavenapline'){
                    synopsys_detect '--detect.project.name="CB_DP_SCM_Kubernetes_1"'
                }
            }
        }
       
   }
    
}