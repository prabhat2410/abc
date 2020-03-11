pipeline {
    agent any   
    tools { 
        git 'Default'
        maven 'MAVEN_HOME' 
        jdk 'JAVA_HOME' 
    }
    stages {
	    stage ('clone') {
            steps {
                git 'https://github.com/edureka-git/DevOpsClassCodes'   
            }
        }
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                ''' 
            }
        }
        
     stage('Archive') {
            steps {
                archiveArtifacts artifacts: '**/target/*.war', fingerprint: true 
            }
        }
        
       stage('Email') {
          steps {
              emailext attachLog: true, body: 'The status of the build can be obtained from the build log attached', subject: 'The build update is ', to: 'prabhat1307@gmail.com'
}
}


		stage('Deployment') {
             steps {
                echo "deployment"
				sh 'sudo chmod 777 /home/centos/workspace/addressbook.war'
                sh 'cp /home/centos/workspace/addressbook.war /opt/tomcat/webapps/'
            }
		}
   }
}
