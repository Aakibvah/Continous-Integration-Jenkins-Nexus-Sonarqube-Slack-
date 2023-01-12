pipeline {
    
	agent any
	
	tools {
        maven "MAVEN3"
        jdk "JAVA_HOME"
    }

 
    stages{
        
        stage('BUILD'){
            steps {
                sh 'mvn clean install -DskipTests'
            }
            // post {
            //     success {
            //         echo 'Now Archiving...'
            //         archiveArtifacts artifacts: '**/target/*.war'
            //     }
            //}
        }

	    stage('UNIT TEST'){
            steps {
                sh 'mvn test'
            }
        }

        stage('Building images'){
            steps {
                sh '''
                    docker build -t aakibvah/vprofileapp /Docker-files/app/.
                    docker build -t aakibvah/vprofiledb /Docker-files/db/.
                    docker build -t aakibvah/vprofileweb /Docker-files/web/.
                
                '''
            }
        }
    }
}
