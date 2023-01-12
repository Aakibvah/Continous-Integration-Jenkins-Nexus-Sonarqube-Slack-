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
                    docker build -f Docker-files/app/Dockerfile -t aakibvah/vprofileapp .
                    docker build -f Docker-files/db/Dockerfile -t aakibvah/vprofileadb .
                    docker build -f Docker-files/web/Dockerfile -t aakibvah/vprofileweb .
                    
                
                '''
            }
        }
    }
}